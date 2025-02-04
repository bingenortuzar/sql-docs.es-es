---
title: Expresiones de comparación (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- node comparison operators [XQuery]
- comparison expressions [XQuery]
- node order comparison operators [XQuery]
- expressions [XQuery], comparison
- comparison operators [XQuery]
- value comparison operators
ms.assetid: dc671348-306f-48ef-9e6e-81fc3c7260a6
author: rothja
ms.author: jroth
ms.openlocfilehash: 7462e089f70b4da76edea25dcfe6e7e314ad7c46
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039032"
---
# <a name="comparison-expressions-xquery"></a>Expresiones de comparación (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery proporciona los siguientes tipos de operadores de comparación:  
  
-   Operadores de comparación generales  
  
-   Operadores de comparación de valor  
  
-   Operadores de comparación de nodos  
  
-   Operadores de comparación de nodo  
  
## <a name="general-comparison-operators"></a>Operadores de comparación generales  
 Los operadores de comparación generales se pueden utilizar para comparar valores atómicos, secuencias o cualquier combinación de ambos.  
  
 Los operadores generales se definen en la tabla siguiente.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|=|Igual|  
|!=|No igual|  
|\<|Menor que|  
|>|Mayor que|  
|\<=|Menor o igual que|  
|>=|Mayor o igual que|  
  
 Cuando se comparan dos secuencias mediante operadores de comparación generales y existe un valor en la segunda secuencia que compara True con un valor de la primera, el resultado general será True. De lo contrario, será False. Por ejemplo, (1, 2, 3) = (3, 4) es True, puesto que el valor 3 aparece en ambas secuencias.  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2,3) = (3,4)')    
```  
  
 La comparación espera que los valores sean de tipos comparables. En concreto, se comprueban estáticamente. En las comparaciones numéricas, se puede dar la promoción de tipos numéricos. Por ejemplo, si se compara un valor decimal de 10 con un valor doble 1e1, el valor decimal se cambiará a doble. Tenga en cuenta que esto puede dar resultados inexactos, pues las comparaciones dobles no pueden ser exactas.  
  
 Si uno de los valores no tiene tipo, se convertirá al tipo del otro valor. En el ejemplo siguiente, el valor 7 se trata como un entero. Antes de compararlo, el valor sin tipo de /a[1] se convertirá en entero. La comparación de enteros devolverá True.  
  
```  
declare @x xml  
set @x='<a>6</a>'  
select @x.query('/a[1] < 7')  
```  
  
 Por el contrario, si se compara el valor sin tipo con una cadena u otro valor sin tipo, se convertirá a xs:string. En la consulta siguiente, la cadena 6 se compara con la cadena "17". La consulta siguiente devuelve False a causa de la comparación de cadenas.  
  
```  
declare @x xml  
set @x='<a>6</a>'  
select @x.query('/a[1] < "17"')  
```  
  
 La consulta siguiente devuelve imágenes pequeñas de un modelo del catálogo de productos proporcionado en la base de datos de ejemplo AdventureWorks. La consulta compara una secuencia de valores atómicos devueltos por `PD:ProductDescription/PD:Picture/PD:Size` con una secuencia de valores singleton, "small". Si la comparación es True, devuelve el < imagen\> elemento.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('         
    for $P in /PD:ProductDescription/PD:Picture[PD:Size = "small"]         
    return $P') as Result         
FROM   Production.ProductModel         
WHERE  ProductModelID=19         
```  
  
 La siguiente consulta compara una secuencia de números de teléfono de < número\> elementos a la cadena literal "112-111-1111". La consulta compara la secuencia de elementos de números de teléfono de la columna AdditionalContactInfo para determinar si un número de teléfono determinado de un cliente en concreto existe en el documento.  
  
```  
WITH XMLNAMESPACES (  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.value('         
   /aci:AdditionalContactInfo//act:telephoneNumber/act:number = "112-111-1111"', 'nvarchar(10)') as Result         
FROM Person.Contact         
WHERE ContactID=1         
```  
  
 La consulta devuelve True. Esto indica que el número existe en el documento. La consulta siguiente es una versión ligeramente modificada de la consulta anterior. En esta consulta, los valores de números de teléfono recuperados del documento se comparan con una secuencia de dos valores de números de teléfono. Si la comparación es True, el < número\> se devuelve el elemento.  
  
```  
WITH XMLNAMESPACES (  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.query('         
  if (/aci:AdditionalContactInfo//act:telephoneNumber/act:number = ("222-222-2222","112-111-1111"))         
  then          
     /aci:AdditionalContactInfo//act:telephoneNumber/act:number         
  else         
    ()') as Result         
FROM Person.Contact         
WHERE ContactID=1  
  
```  
  
 Éste es el resultado:  
  
```  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
    111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
    112-111-1111  
\</act:number>   
```  
  
## <a name="value-comparison-operators"></a>Operadores de comparación de valores  
 Los operadores de comparación de valores se utilizan para comparar valores atómicos. Tenga en cuenta que, en las consultas, puede utilizar operadores de comparación generales en lugar de operadores de comparación de valores.  
  
 Los operadores de comparación de valores se definen en la tabla siguiente.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|eq|Igual|  
|ne|No igual|  
|lt|Menor que|  
|gt|Mayor que|  
|le|Menor o igual que|  
|ge|Mayor o igual que|  
  
 Si los dos valores comparan lo mismo en función del operador seleccionado, la expresión devolverá True. De lo contrario, devolverá False. Si alguno de los valores es una secuencia vacía, el resultado de la expresión será False.  
  
 Estos operadores solo funcionan en valores atómicos singleton. Es decir, no se puede especificar una secuencia como uno de los operandos.  
  
 Por ejemplo, la siguiente consulta recupera \<imagen > elementos para un modelo de producto donde el tamaño de imagen es "pequeño:  
  
```  
SELECT CatalogDescription.query('         
              declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";         
              for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]         
              return         
                    $P         
             ') as Result         
FROM Production.ProductModel         
WHERE ProductModelID=19         
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   `declare namespace` define el prefijo de espacio de nombres que se utilizará posteriormente en la consulta.  
  
-   El \<tamaño > valor del elemento se compara con el valor atómico especificado, "small".  
  
-   Tenga en cuenta que dado que los operadores de valores solo funcionan en valores atómicos, la **data()** función implícitamente se usa para recuperar el valor del nodo. Es decir, `data($P/PD:Size) eq "small"` obtiene el mismo resultado.  
  
 Éste es el resultado:  
  
```  
\<PD:Picture   
  xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  \<PD:Angle>front\</PD:Angle>  
  \<PD:Size>small\</PD:Size>  
  \<PD:ProductPhotoID>31\</PD:ProductPhotoID>  
\</PD:Picture>  
```  
  
 Tenga en cuenta que las reglas de promoción de tipos para comparaciones de valores son las mismas que para las comparaciones generales. Además, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utiliza las mismas reglas de conversión para los valores sin tipo durante las comparaciones de valores, al igual que durante las comparaciones generales. En cambio, las reglas de la especificación XQuery siempre convierten el valor sin tipo a xs:string durante las comparaciones de valores.  
  
## <a name="node-comparison-operator"></a>Operadores de comparación de nodos  
 El operador de comparación de nodo, **es**, solo se aplica a tipos de nodo. El resultado que devuelve indica si dos nodos pasados como operandos representan al mismo nodo en el documento de origen. Este operador devuelve True si los dos operandos son el mismo nodo. De lo contrario, devuelve False.  
  
 La consulta siguiente comprueba si la ubicación de centro de trabajo 10 es la primera en el proceso de fabricación de un modelo de producto determinado.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions' AS AWMI)  
  
SELECT ProductModelID, Instructions.query('         
    if (  (//AWMI:root/AWMI:Location[@LocationID=10])[1]         
          is          
          (//AWMI:root/AWMI:Location[1])[1] )          
    then         
          <Result>equal</Result>         
    else         
          <Result>Not-equal</Result>         
         ') as Result         
FROM Production.ProductModel         
WHERE ProductModelID=7           
```  
  
 Éste es el resultado:  
  
```  
ProductModelID       Result          
-------------- --------------------------  
7              <Result>equal</Result>      
```  
  
## <a name="node-order-comparison-operators"></a>Operadores de comparación de orden de nodos  
 Los operadores de comparación de orden de nodos comparan pares de nodos según sus posiciones en un documento.  
  
 A continuación se exponen las comparaciones que se realizan en función del orden en el documento:  
  
-   `<<` : Does **operando 1** preceder **operando 2** en el orden del documento.  
  
-   `>>` : Does **operando 1** siga **operando 2** en el orden del documento.  
  
 La consulta siguiente devuelve True si la descripción del catálogo de productos el \<garantía > elemento que aparezcan antes que la \<Mantenimiento > elemento en el orden del documento de un determinado producto.  
  
```  
WITH XMLNAMESPACES (  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS WM)  
  
SELECT CatalogDescription.value('  
     (/PD:ProductDescription/PD:Features/WM:Warranty)[1] <<   
           (/PD:ProductDescription/PD:Features/WM:Maintenance)[1]', 'nvarchar(10)') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El **value()** método de la **xml**se usa el tipo de datos en la consulta.  
  
-   El resultado booleano de la consulta se convierte en **nvarchar (10)** y se devuelven.  
  
-   La consulta devuelve True.  
  
## <a name="see-also"></a>Vea también  
 [Sistema de tipos &#40;XQuery&#41;](../xquery/type-system-xquery.md)   
 [Expresiones XQuery](../xquery/xquery-expressions.md)  
  
  
