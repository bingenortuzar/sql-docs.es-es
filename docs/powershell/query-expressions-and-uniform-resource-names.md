---
title: Expresiones de consulta y nombres de recursos uniformes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- query expressions
- unique resource names
- URN
ms.assetid: e0d30dbe-7daf-47eb-8412-1b96792b6fb9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0eca650c1e499c54715204637306485280938707
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049111"
---
# <a name="query-expressions-and-uniform-resource-names"></a>Expresiones de consulta y nombres de recursos uniformes

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Los modelos de objetos de administración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (SMO) y los complementos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell usan dos tipos de cadenas de expresiones que se parecen a las expresiones XPath. Las expresiones de consulta son cadenas que especifican un conjunto de criterios usados para enumerar uno o más objetos de una jerarquía del modelo de objetos. Un nombre de recurso uniforme (URN) es un tipo específico de cadena de expresión de consulta que identifica exclusivamente un objeto único.  

> [!NOTE]
> Hay dos módulos de SQL Server PowerShell: **SqlServer** y **SQLPS**. El módulo **SQLPS** está incluido en la instalación de SQL Server (por motivos de compatibilidad con versiones anteriores), pero ya no se actualiza. El módulo de PowerShell más actualizado es **SqlServer**. El módulo **SqlServer** contiene versiones actualizadas de los cmdlets en **SQLPS**, así como nuevos cmdlets para admitir las características más recientes de SQL.  
> Las versiones anteriores del módulo **SqlServer** *estaban incluidas* en SQL Server Management Studio (SSMS), pero solo con las versiones 16.x de SSMS. Para usar PowerShell con SSMS 17.0 y versiones posteriores, debe tener el módulo **SqlServer** instalado desde la Galería de PowerShell.
> Para instalar el módulo **SqlServer**, consulte [Instalar SQL Server PowerShell](download-sql-server-ps-module.md).

  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Object1[<FilterExpression1>]/ ... /ObjectN[<FilterExpressionN>]  
  
<FilterExpression>::=  
<PropertyExpression> [and <PropertyExpression>][...n]  
  
<PropertyExpression>::=  
      @BooleanPropertyName=true()  
 | @BooleanPropertyName=false()  
 | contains(@StringPropertyName, 'PatternString')  
  | @StringPropertyName='String'  
 | @DatePropertyName=datetime('DateString')  
 | is_null(@PropertyName)  
 | not(<PropertyExpression>)  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Object*  
 Especifica el tipo de objeto que se representa en ese nodo de la cadena de expresión. Cada objeto representa una clase de colección de estos espacios de nombres del modelo de objetos SMO:  
  
 <xref:Microsoft.SqlServer.Management.Smo>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Agent>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Broker>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Mail>  
  
 <xref:Microsoft.SqlServer.Management.Dmf>  
  
 <xref:Microsoft.SqlServer.Management.Facets>  
  
 <xref:Microsoft.SqlServer.Management.RegisteredServers>  
  
 <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>  
  
 Por ejemplo, especifique el valor Server para la clase **ServerCollection** y el valor Database para la clase **DatabaseCollection** .  
  
 \@*PropertyName*  
 Especifica el nombre de una de las propiedades de la clase que está asociada con el objeto especificado en *Object*. El nombre de la propiedad debe llevar un prefijo con el carácter \@. Por ejemplo, especifique el valor \@IsAnsiNull para **IsAnsiNull** de la propiedad de clase **Database**.  
  
 \@*BooleanPropertyName*=true()  
 Enumera todos los objetos en los que el valor de la propiedad booleana especificada se establece en TRUE.  
  
 \@*BooleanPropertyName*=false()  
 Enumera todos los objetos en los que el valor de la propiedad booleana especificada se establece en FALSE.  
  
 contains(\@*StringPropertyName*, '*PatternString*')  
 Enumera todos los objetos en los que la propiedad de cadena especificada contiene, al menos, una aparición del juego de caracteres especificado en “*PatternString*”.  
  
 \@*StringPropertyName*='*PatternString*'  
 Enumera todos los objetos en los que el valor de la propiedad de cadena especificada es exactamente igual que el patrón de caracteres especificado en “*PatternString*”.  
  
 \@*DatePropertyName*= datetime('*DateString*')  
 Enumera todos los objetos en los que el valor de la propiedad de fecha especificada coincide con la fecha especificada en “*DateString*”. *DateString* debe seguir el formato aaaa-mm-dd hh:mi:ss.mmm.  
  
|||  
|-|-|  
|aaaa|Año de cuatro dígitos.|  
|MM|Mes de dos dígitos (del 01 al 12).|  
|dd|Fecha de dos dígitos (del 01 al 31).|  
|hh|Hora de dos dígitos en un reloj de 24 horas (del 01 al 23).|  
|mi|Minutos de dos dígitos (del 01 al 59).|  
|ss|Segundos de dos dígitos (del 01 al 59).|  
|mmm|Número de milisegundos (del 001 al 999).|  
  
 Las fechas que se especifican en este formato se pueden evaluar en cualquier formato de fecha que se almacene en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 is_null(\@*PropertyName*)  
 Enumera todos los objetos en los que la propiedad especificada tiene un valor de NULL.  
  
 not(\<*PropertyExpression*>)  
 Niega el valor de evaluación de *PropertyExpression*, enumerando todos los objetos que no coinciden con la condición especificada en *PropertyExpression*. Por ejemplo, distinto de (contains(\@Name, 'xyz')) enumera todos los objetos que no tienen la cadena xyz en su nombre.  
  
## <a name="remarks"></a>Notas  
 Las expresiones de consulta son cadenas que enumeran los nodos de una jerarquía de modelo SMO. Cada nodo tiene una expresión de filtro que especifica los criterios para determinar los objetos que se enumeran en ese nodo. Las expresiones de consulta se modelan en el lenguaje de expresión XPath. Las expresiones de consulta implementan un pequeño subconjunto admitido por XPath y, además, tienen algunas extensiones que no se encuentran en XPath. Las expresiones XPath son cadenas que especifican un conjunto de criterios usados para enumerar una o mas de las etiquetas de un documento XML. Para obtener más información acerca de XPath, vea [W3C XPath Language](http://www.w3.org/TR/xpath20/).  
  
 Las expresiones de consulta deben empezar por una referencia absoluta al objeto Server. No se admiten expresiones relativas con una / inicial. La secuencia de objetos que se especifica en una expresión de consulta debe seguir la jerarquía de los objetos de la colección del modelo de objetos asociado. Por ejemplo, una expresión de consulta que hace referencia a objetos del espacio de nombres Microsoft.SqlServer.Management.Smo debe empezar por un nodo Server seguido de un nodo Database, etc.  
  
 Si no se especifica *\<FilterExpression>* en un objeto, se enumeran todos los objetos de ese nodo.  
  
## <a name="uniform-resource-names-urn"></a>Nombres de recursos uniformes (URN)  
 Los URN son un subconjunto de expresiones de consulta. Cada URN forma una referencia completa a un solo objeto. Un URN típico utiliza la propiedad Name para identificar un objeto único de cada nodo. Por ejemplo, este URN hace referencia a una columna concreta:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[@Name='SalesPerson' and @Schema='Sales']/Column[@Name='SalesPersonID']  
```  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-enumerating-objects-using-false"></a>A. Enumerar objetos mediante false()  
 Esta expresión de consulta enumera todas las bases de datos que tienen el atributo **AutoClose** definido en false en la instancia predeterminada de **MyComputer**.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@AutoClose=false()]  
```  
  
### <a name="b-enumerating-objects-using-contains"></a>B. Enumerar objetos mediante contains  
 Esta expresión de consulta enumera todas las bases de datos con distinción entre mayúsculas y minúsculas, y cuyo nombre contiene el carácter 'm'.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@CaseSensitive=false() and contains(@Name, 'm')]   
```  
  
### <a name="c-enumerating-objects-using-not"></a>C. Enumerar objetos mediante not  
 Esta expresión de consulta enumera todas las tablas de [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] que no están en el esquema **Production** y contienen la palabra History en el nombre de tabla:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[not(@Schema='Production') and contains(@Name, 'History')]  
```  
  
### <a name="d-not-supplying-a-filter-expression-for-the-final-node"></a>D. Sin proporcionar ninguna expresión de filtro para el nodo final  
 Esta expresión de consulta enumera todas las columnas de la tabla **AdventureWorks2012.Sales.SalesPerson** :  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@Schema='Sales' and @Name='SalesPerson']/Columns  
```  
  
### <a name="e-enumerating-objects-using-datetime"></a>E. Enumerar objetos mediante datetime  
 Esta expresión de consulta enumera todas las tablas creadas en la base de datos de [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] en un momento concreto:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@CreateDate=datetime('2008-03-21 19:49:32.647')]  
```  
  
### <a name="f-enumerating-objects-using-isnull"></a>F. Enumerar objetos mediante is_null  
 Esta expresión de consulta enumera todas las tablas de la base de datos de [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] que no tienen el valor NULL para su propiedad de fecha de última modificación:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[Not(is_null(@DateLastModified))]  
```  
  
## <a name="see-also"></a>Consulte también  
 [cmdlet Invoke-PolicyEvaluation](invoke-policyevaluation-cmdlet.md)   
 [SQL Server Audit &#40;motor de base de datos&#41;](../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
  
  
