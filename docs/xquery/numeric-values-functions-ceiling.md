---
title: CEILING (función de XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:ceiling function
- ceiling function [XQuery]
ms.assetid: 594f1dd0-3c27-41b3-b809-9ce6714c5a97
author: rothja
ms.author: jroth
ms.openlocfilehash: fe18f488b83c1a8c9236c642751c1dc80bfe7e6c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946575"
---
# <a name="numeric-values-functions---ceiling"></a>Funciones de valores numéricos: ceiling 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el número más pequeño, sin la parte fraccionaria, que no sea menor que el valor de su argumento. Si el argumento es una secuencia vacía, devuelve la secuencia vacía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:ceiling ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Número al que se aplica la función.  
  
## <a name="remarks"></a>Comentarios  
 Si el tipo de *$arg* es uno de los tres tipos bases numéricos, **xs: float**, **xs: Double**, o **xs: decimal**, el tipo de valor devuelto es igual a el *$arg* tipo.  
  
 Si el tipo de *$arg* es un tipo derivado de uno de los tipos numéricos, el tipo de valor devuelto es el tipo base numérico.  
  
 Si la entrada a las funciones fn: Floor, fn o fn: ROUND es **xdt: untypedAtomic**, se convertirá implícitamente al **xs: Double**.  
  
 Cualquier otro tipo genera un error estático.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos AdventureWorks.  
  
### <a name="a-using-the-ceiling-xquery-function"></a>A. Usar la función ceiling() de XQuery  
 Para el modelo de producto 7, esta consulta devuelve una lista de las ubicaciones de los centros de trabajo del proceso de fabricación del modelo de producto. Para cada ubicación de centro de trabajo, la consulta devuelve el Id. de ubicación, las horas de trabajo y el tamaño del lote, en caso de que estén documentados. La consulta utiliza la **ceiling** función para devolver las horas de trabajo como valores de tipo **decimal**.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
     for $i in /AWMI:root/AWMI:Location  
     return   
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ ceiling($i/@LaborHours) }" >  
                    {   
                      $i/@LotSize  
                    }    
       </Location>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El prefijo de espacio de nombres AWMI viene del inglés Adventure Works Manufacturing Instructions (instrucciones de fabricación de Adventure Works). Este prefijo hace referencia al mismo espacio de nombres que se utiliza en el documento que se consulta.  
  
-   **Instrucciones** es un **xml** columna de tipo. Por lo tanto, el [método query() (tipo de datos XML)](../t-sql/xml/query-method-xml-data-type.md) se usa para especificar XQuery. La instrucción de XQuery se especifica como el argumento para el método de consulta.  
  
-   **para... devolver** es una construcción de bucle. En la consulta, el **para** bucle identifica una lista de \<ubicación > elementos. Para cada ubicación de centro de trabajo, el **devolver** instrucción en el **para** bucle describe el XML que se va a generar:  
  
    -   Un \<ubicación > elemento que tiene los atributos LocationID y LaborHrs. La expresión correspondiente situada dentro de las llaves ({ }) recupera los valores requeridos del documento.  
  
    -   El {$i/@LotSize } expresión recupera el atributo LotSize del documento, si está presente.  
  
    -   Éste es el resultado:  
  
```  
ProductModelID Result    
-------------- ------------------------------------------------------  
7      <Location LocationID="10" LaborHrs="3" LotSize="100"/>  
       <Location LocationID="20" LaborHrs="2" LotSize="1"/>     
       <Location LocationID="30" LaborHrs="1" LotSize="1"/>     
       <Location LocationID="45" LaborHrs="1" LotSize="20"/>  
       <Location LocationID="60" LaborHrs="3" LotSize="1"/>     
       <Location LocationID="60" LaborHrs="4" LotSize="1"/>  
```  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **ceiling()** función asigna todos los valores enteros a xs: decimal.  
  
## <a name="see-also"></a>Vea también  
 [Función FLOOR &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [Función Round &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)  
  
  
