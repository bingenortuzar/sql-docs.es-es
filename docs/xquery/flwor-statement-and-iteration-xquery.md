---
title: FLWOR instrucción e iteración (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- return clause
- FLWOR statement
- effective Boolean value [XQuery]
- multiple variable binding
- order by clause [XQuery]
- for clause [XQuery]
- where clause [XQuery]
- iterations [XQuery]
- XQuery, FLWOR statement
- EBV
ms.assetid: d7cd0ec9-334a-4564-bda9-83487b6865cb
author: rothja
ms.author: jroth
ms.openlocfilehash: 9deb87d506e167d3de3439e0a07cfbb8bc040fac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038904"
---
# <a name="flwor-statement-and-iteration-xquery"></a>FLWOR (instrucción e iteración de XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery define la sintaxis de iteración FLWOR. FLWOR es el acrónimo de `for`, `let`, `where`, `order by` y `return`.  
  
 Una instrucción FLWOR está formada por cuatro partes:  
  
-   Una o varias cláusulas FOR que enlazan una o varias variables de iteración a secuencias de entrada.  
  
     Las secuencias de entrada pueden ser otras expresiones XQuery como expresiones XPath. Se trata de secuencias de nodos o de valores atómicos. Las secuencias de valores atómicos se pueden construir con literales o funciones constructoras. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no admite los nodos XML construidos como secuencias de entrada.  
  
-   Una cláusula opcional `let`. Esta cláusula asigna un valor a la variable para una iteración concreta. La expresión asignada puede ser una expresión XQuery, como una expresión XPath, y puede devolver una secuencia de nodos o una secuencia de valores atómicos. Las secuencias de valores atómicos se pueden construir con literales o con funciones constructoras. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no admite los nodos XML construidos como secuencias de entrada.  
  
-   Una variable de iteración. Esta variable puede tener una aserción de tipo opcional mediante la palabra clave `as`.  
  
-   Una cláusula opcional `where`. Esta cláusula aplica un predicado de filtro en la iteración.  
  
-   Una cláusula opcional `order by`.  
  
-   Una expresión `return`. La expresión de la cláusula `return` construye el resultado de la instrucción FLWOR.  
  
 Por ejemplo, la consulta siguiente recorre en iteración el <`Step`> elementos en la primera ubicación de fabricación y devuelve el valor de cadena de la <`Step`> nodos:  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $step in /ManuInstructions/Location[1]/Step  
   return string($step)  
')  
```  
  
 Éste es el resultado:  
  
```  
Manu step 1 at Loc 1 Manu step 2 at Loc 1 Manu step 3 at Loc 1  
```  
  
 La consulta siguiente es parecida a la anterior, a diferencia de que se especifica en la columna Instructions, una columna xml con tipo, de la tabla ProductModel. La consulta recorre en iteración todos los pasos de fabricación, <`step`> elementos en la primera ubicación de centro de trabajo para un producto específico.  
  
```sql
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in //AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   `$Step` es la variable de iteración.  
  
-   El [expresión de ruta de acceso](../xquery/path-expressions-xquery.md), `//AWMI:root/AWMI:Location[1]/AWMI:step`, genera la secuencia de entrada. Esta secuencia es la secuencia de la <`step`> elementos secundarios del nodo de elemento del primer <`Location`> nodo de elemento.  
  
-   La cláusula de predicado opcional, `where`, no se utiliza.  
  
-   El `return` expresión devuelve un valor de cadena desde el <`step`> elemento.  
  
 El [string (función de XQuery)](../xquery/data-accessor-functions-string-xquery.md) se usa para recuperar el valor de cadena de la <`step`> nodo.  
  
 Éste es el resultado parcial:  
  
```  
Insert aluminum sheet MS-2341 into the T-85A framing tool.   
Attach Trim Jig TJ-26 to the upper and lower right corners of   
the aluminum sheet. ....         
```  
  
 A continuación se exponen ejemplos de las secuencias de entrada adicionales permitidas:  
  
```sql
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in (1, 2, 3)  
  return $a')  
-- result = 1 2 3   
  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in   
   for $b in (1, 2, 3)  
      return $b  
return $a')  
-- result = 1 2 3  
  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('  
  for $a in (xs:string( "test"), xs:double( "12" ), data(/ROOT/a ))  
  return $a')  
-- result test 12 111  
```  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no admite las secuencias heterogéneas. En concreto, no se admiten las secuencias que contienen una mezcla de valores atómicos y nodos.  
  
 Iteración con frecuencia se utiliza junto con el [construcción de XML](../xquery/xml-construction-xquery.md) formatos de sintaxis en la transformación de XML, tal como se muestra en la siguiente consulta.  
  
 En la base de datos de ejemplo AdventureWorks, las instrucciones de fabricación almacenan en el **instrucciones** columna de la **Production.ProductModel** tabla tienen el formato siguiente:  
  
```xml
<Location LocationID="10" LaborHours="1.2"   
            SetupHours=".2" MachineHours=".1">  
  <step>describes 1st manu step</step>  
   <step>describes 2nd manu step</step>  
   ...  
</Location>  
...  
```  
  
 La consulta siguiente construye un nuevo XML que tiene el <`Location`> elementos con el trabajo del centro de los atributos de ubicación devueltos como elementos secundarios:  
  
```xml
<Location>  
   <LocationID>10</LocationID>  
   <LaborHours>1.2</LaborHours>  
   <SetupHours>.2</SetupHours>  
   <MachineHours>.1</MachineHours>  
</Location>  
...  
```  
  
 Esta es la consulta:  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in /AWMI:root/AWMI:Location  
        return  
          <Location>  
            <LocationID> { data($WC/@LocationID) } </LocationID>  
            <LaborHours>   { data($WC/@LaborHours) }   </LaborHours>  
            <SetupHours>   { data($WC/@SetupHours) }   </SetupHours>  
            <MachineHours> { data($WC/@MachineHours) } </MachineHours>  
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   La instrucción FLWOR recupera una secuencia de <`Location`> elementos de un producto específico.  
  
-   El [datos (función de XQuery)](../xquery/data-accessor-functions-data-xquery.md) se usa para extraer el valor de cada atributo, por lo que se agregarán al XML resultante como nodos de texto en lugar de como atributos.  
  
-   La expresión de la cláusula RETURN construye el XML deseado.  
  
 Éste es un resultado parcial:  
  
```xml
<Location>  
  <LocationID>10</LocationID>  
  <LaborHours>2.5</LaborHours>  
  <SetupHours>0.5</SetupHours>  
  <MachineHours>3</MachineHours>  
</Location>  
<Location>  
   ...  
<Location>  
...  
```  
  
## <a name="using-the-let-clause"></a>Usar la cláusula let  
 Puede utilizar la cláusula `let` para asignar nombre a las expresiones que se repiten y poder hacer referencia a ellas por medio de la variable asignada. La expresión asignada a una variable `let` se insertará en la consulta cada vez que se haga referencia a la variable en la consulta. Esto significa que la instrucción no se ejecutará una sola vez, sino tantas veces como se haga referencia a la expresión.  
  
 En la base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)], las instrucciones de fabricación contienen información sobre las herramientas requeridas y la ubicación donde se utilizan. La consulta siguiente utiliza la cláusula `let` para hacer una lista de las herramientas necesarias para generar un modelo de producción, así como las ubicaciones en que se necesita cada herramienta.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $T in //AWMI:tool  
            let $L := //AWMI:Location[.//AWMI:tool[.=data($T)]]  
        return  
          <tool desc="{data($T)}" Locations="{data($L/@LocationID)}"/>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="using-the-where-clause"></a>Usar la cláusula where  
 Puede usar el `where` cláusula para filtrar los resultados de una iteración. Esto se muestra en el ejemplo siguiente.  
  
 El proceso de fabricación de una bicicleta incluye una serie de ubicaciones de centro de trabajo. Cada una define una secuencia de pasos de fabricación. La consulta siguiente recupera únicamente las ubicaciones de centro de trabajo que fabrican un modelo de bicicleta y tienen menos de tres pasos de fabricación. Es decir, tienen menos de tres <`step`> elementos.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location  
      where count($WC/AWMI:step) < 3  
      return  
          <Location >  
           { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El `where` usa la palabra clave el **count()** función para contar el número de <`step`> ubicación del centro de elementos secundarios de cada trabajo.  
  
-   La expresión `return` construye el XML deseado a partir de los resultados de la iteración.  
  
 Éste es el resultado:  
  
```  
<Location LocationID="30"/>   
```  
  
 El resultado de la expresión de la cláusula `where` se convierte en un valor booleano mediante las reglas siguientes, en el orden especificado. Se trata de las mismas reglas que se aplican para los predicados en las expresiones de ruta de acceso, con la diferencia de que no se admiten los enteros:  
  
1.  Si la expresión `where` devuelve una secuencia vacía, su valor booleano efectivo será False.  
  
2.  Si la expresión `where` devuelve un valor de tipo booleano simple, éste será el valor booleano efectivo.  
  
3.  Si la expresión `where` devuelve una secuencia que incluye al menos un nodo, el valor booleano efectivo será True.  
  
4.  De lo contrario, provocará un error estático.  
  
## <a name="multiple-variable-binding-in-flwor"></a>Enlace de diversas variables en FLWOR  
 Puede tener una sola expresión FLWOR que enlace diversas variables a secuencias de entrada. En el ejemplo siguiente, la consulta se especifica con una variable xml sin tipo. La expresión FLOWR devuelve el primer <`Step`> en cada elemento secundario del elemento <`Location`> elemento.  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $Loc in /ManuInstructions/Location,  
       $FirstStep in $Loc/Step[1]  
   return   
       string($FirstStep)  
')  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El `for` expresión define `$Loc` y $`FirstStep` variables.  
  
-   Las expresiones `two`, `/ManuInstructions/Location` y `$FirstStep in $Loc/Step[1]`, están correlacionadas: los valores de `$FirstStep` dependen de los valores de `$Loc`.  
  
-   La expresión asociada `$Loc` genera una secuencia de <`Location`> elementos. Para cada <`Location`> elemento, `$FirstStep` genera una secuencia de uno <`Step`> elemento, un singleton.  
  
-   `$Loc` se especifica en la expresión asociada con la variable `$FirstStep`.  
  
 Éste es el resultado:  
  
```  
Manu step 1 at Loc 1   
Manu step 1 at Loc 2  
```  
  
 La consulta siguiente es similar, salvo que se especifica en la columna Instructions, escribió **xml** columna, de la **ProductModel** tabla. [Construcción de XML (XQuery)](../xquery/xml-construction-xquery.md) se usa para generar el XML que desee.  
  
```sql
SELECT Instructions.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /root/Location,  
            $S  in $WC/step  
      return  
          <Step LocationID= "{$WC/@LocationID }" >  
            { $S/node() }  
          </Step>  
') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   La cláusula `for` define dos variables, `$WC` y `$S`. La expresión asociada con `$WC` genera una secuencia de ubicaciones de centro de trabajo para la fabricación de un modelo de bicicleta. La expresión de ruta de acceso asignada a la variable `$S` genera una secuencia de pasos para cada secuencia de ubicaciones de centro de trabajo de `$WC`.  
  
-   La instrucción return construye el XML que tiene un <`Step`> elemento que contiene el paso de fabricación y **LocationID** como su atributo.  
  
-   El **declarar el espacio de nombres de elemento predeterminado** se usa en el prólogo de XQuery para que todas las declaraciones de espacio de nombres en el XML resultante aparezcan en el elemento de nivel superior. Esto facilita la lectura del resultado. Para obtener más información acerca de espacios de nombres predeterminados, consulte [controlar espacios de nombres en XQuery](../xquery/handling-namespaces-in-xquery.md).  
  
 Éste es el resultado parcial:  
  
```xml
<Step xmlns=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
  LocationID="10">  
     Insert <material>aluminum sheet MS-2341</material> into the <tool>T-   
     85A framing tool</tool>.   
</Step>  
...  
<Step xmlns=  
      "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
    LocationID="20">  
        Assemble all frame components following blueprint   
        <blueprint>1299</blueprint>.  
</Step>  
...  
```  
  
## <a name="using-the-order-by-clause"></a>Usar la cláusula order by  
 La ordenación en XQuery se realiza usando la cláusula `order by` en la expresión FLWOR. Las expresiones de ordenación que se pasan a la `order by` cláusula debe devolver valores cuyos tipos son válidos para el **gt** operador. Cada expresión de ordenación debe dar como resultado una secuencia de singleton con un elemento. De forma predeterminada, la ordenación se realiza en orden ascendente. Podrá especificar opcionalmente un orden ascendente o descendente para cada expresión de ordenación.  
  
> [!NOTE]  
>  Las comparaciones de ordenación en valores de cadena realizadas mediante la implementación de XQuery en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se realizan siempre con la intercalación de puntos de código Unicode binarios.  
  
 La consulta siguiente recupera todos los números de teléfono de un cliente determinado de la columna AdditionalContactInfo. Los resultados se ordenan por número de teléfono.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT AdditionalContactInfo.query('  
   declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 Tenga en cuenta que el [atomización (XQuery)](../xquery/atomization-xquery.md) proceso recupera el valor atómico de la <`number`> elementos antes de pasarlo a `order by`. Puede escribir la expresión utilizando el **data()** función, pero que no es necesario.  
  
```  
order by data($a/act:number[1]) descending  
```  
  
 Éste es el resultado:  
  
```xml
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
```  
  
 En lugar de declarar los espacios de nombres en el prólogo de la consulta, puede declararlos mediante el uso de WITH XMLNAMESPACES.  
  
```sql
WITH XMLNAMESPACES (  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo'  AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 También puede ordenar por valor de atributo. Por ejemplo, la consulta siguiente recupera el recién creado <`Location`> elementos que tienen los atributos LocationID y LaborHours ordenados por el atributo LaborHours en orden descendente. Como resultado, se devolverán primero las ubicaciones de centro de trabajo que tengan el máximo de horas de trabajo (LaborHours).  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location   
order by $WC/@LaborHours descending  
        return  
          <Location>  
             { $WC/@LocationID }   
             { $WC/@LaborHours }   
          </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 Éste es el resultado:  
  
```  
<Location LocationID="60" LaborHours="4"/>  
<Location LocationID="50" LaborHours="3"/>  
<Location LocationID="10" LaborHours="2.5"/>  
<Location LocationID="20" LaborHours="1.75"/>  
<Location LocationID="30" LaborHours="1"/>  
<Location LocationID="45" LaborHours=".5"/>  
```  
  
 En la consulta siguiente, se ordenan los resultados por nombre de elemento. La consulta recupera las especificaciones de un producto determinado del catálogo de productos. Las especificaciones son los elementos secundarios de la <`Specifications`> elemento.  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace  
 pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $a in /pd:ProductDescription/pd:Specifications/*   
     order by local-name($a)  
      return $a  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19;  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El `/p1:ProductDescription/p1:Specifications/*` expresión devuelve los elementos secundarios del elemento <`Specifications`>.  
  
-   La expresión `order by (local-name($a))` ordena la secuencia por la parte local del nombre del elemento.  
  
 Éste es el resultado:  
  
```xml
<Color>Available in most colors</Color>  
<Material>Almuminum Alloy</Material>  
<ProductLine>Mountain bike</ProductLine>  
<RiderExperience>Advanced to Professional riders</RiderExperience>  
<Style>Unisex</Style>    
```  
  
 Los nodos en los que se devuelve la expresión de ordenación vacía se ordenan al principio de la secuencia, tal como se muestra en el ejemplo siguiente:  
  
```sql
declare @x xml  
set @x='<root>  
  <Person Name="A" />  
  <Person />  
  <Person Name="B" />  
</root>  
'  
select @x.query('  
  for $person in //Person  
  order by $person/@Name  
  return   $person  
')  
```  
  
 Éste es el resultado:  
  
```xml
<Person />  
<Person Name="A" />  
<Person Name="B" />  
```  
  
 Se pueden especificar varios criterios de ordenación, tal como se muestra en el ejemplo siguiente. La consulta en este ejemplo ordena <`Employee`> elementos en primer lugar por título y, a continuación, Administrador de los valores de atributo.  
  
```sql
declare @x xml  
set @x='<root>  
  <Employee ID="10" Title="Teacher"        Gender="M" />  
  <Employee ID="15" Title="Teacher"  Gender="F" />  
  <Employee ID="5" Title="Teacher"         Gender="M" />  
  <Employee ID="11" Title="Teacher"        Gender="F" />  
  <Employee ID="8" Title="Administrator"   Gender="M" />  
  <Employee ID="4" Title="Administrator"   Gender="F" />  
  <Employee ID="3" Title="Teacher"         Gender="F" />  
  <Employee ID="125" Title="Administrator" Gender="F" /></root>'  
SELECT @x.query('for $e in /root/Employee  
order by $e/@Title ascending, $e/@Gender descending  
  
  return  
     $e  
')  
```  
  
 Éste es el resultado:  
  
```xml
<Employee ID="8" Title="Administrator" Gender="M" />  
<Employee ID="4" Title="Administrator" Gender="F" />  
<Employee ID="125" Title="Administrator" Gender="F" />  
<Employee ID="10" Title="Teacher" Gender="M" />  
<Employee ID="5" Title="Teacher" Gender="M" />  
<Employee ID="11" Title="Teacher" Gender="F" />  
<Employee ID="15" Title="Teacher" Gender="F" />  
<Employee ID="3" Title="Teacher" Gender="F" />  
```  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   Las expresiones de ordenación deben tener un tipo homogéneo. Esto se comprueba de forma estática.  
  
-   La ordenación de secuencias vacías no se puede controlar.  
  
-   `order by` no admite las palabras clave empty least, empty greatest ni collation.  
  
## <a name="see-also"></a>Vea también  
 [Expresiones XQuery](../xquery/xquery-expressions.md)  
  
  
