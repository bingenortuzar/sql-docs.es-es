---
title: Especificar funciones de conversión explícita en consultas XPath (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit conversion functions [SQLXML]
- string function
- number function
- XPath queries [SQLXML], explicit conversion functions
ms.assetid: 1111cb5d-2bd9-4bdb-8de2-dc0e47452dd6
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e01c63fd0961755eefc0afb0493005d3b5c1c6c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027068"
---
# <a name="specifying-explicit-conversion-functions-in-xpath-queries-sqlxml-40"></a>Especificar funciones de conversión explícita en consultas XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En los siguientes ejemplos se muestra cómo especificar funciones de conversión explícita en consultas XPath. Las consultas XPath de estos ejemplos se especifican en el esquema de asignación que se incluye en SampleSchema1.xml. Para obtener información acerca de este esquema de ejemplo, vea [esquema de XSD anotado de ejemplo para obtener ejemplos de XPath &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-use-the-number-explicit-conversion-function"></a>A. Usar la función de conversión explícita number()  
 El **number()** función convierte un argumento en un número.  
  
 Suponiendo que el valor de **ContactID** no es numérico, la siguiente consulta convierte **ContactID** a un número y lo compara con el valor 4. A continuación, la consulta devuelve todos  **\<empleado >** elementos secundarios del nodo de contexto con el **ContactID** atributo que tiene un valor numérico de 4:  
  
```  
/child::Contact[number(attribute::ContactID)= 4]  
```  
  
 Un acceso directo a la **atributo** eje (@) se pueden especificar y porque el **secundarios** es el eje predeterminado, puede omitirse de la consulta:  
  
```  
/Contact[number(@ContactID) = 4]  
```  
  
 En términos relacionales, la consulta devuelve un empleado con un **ContactID** de 4.  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para probar la consulta XPath en el esquema de asignación  
  
1.  Copia el [código del esquema de ejemplo](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) y péguelo en un archivo de texto. Guarde el archivo como SampleSchema1.xml.  
  
2.  Cree la siguiente plantilla (ExplicitConversionA.xml) y guárdela en el mismo directorio donde esté guardado el archivo SampleSchema1.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Contact[number(@ContactID)=4]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (SampleSchema1.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el conjunto de resultados de ejecución de esta plantilla:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
### <a name="b-use-the-string-explicit-conversion-function"></a>b. Usar la función de conversión explícita string()  
 El **string()** función convierte un argumento en una cadena.  
  
 La siguiente consulta convierte **ContactID** en una cadena y lo compara con la cadena de valor "4". La consulta devuelve todos los  **\<empleado >** elementos secundarios del nodo de contexto con un **ContactID** con un valor de cadena "4":  
  
```  
/child::Contact[string(attribute::ContactID)="4"]  
```  
  
 Un acceso directo a la **atributo** eje (@) se pueden especificar y porque el **secundarios** es el eje predeterminado, puede omitirse de la consulta:  
  
```  
/Contact[string(@ContactID)="4"]  
```  
  
 Funcionalmente, esta consulta devuelve los mismos resultados que la consulta de ejemplo anterior, pero la evaluación se realiza en un valor de cadena y no en el valor numérico (es decir, el número 4).  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Para probar la consulta XPath en el esquema de asignación  
  
1.  Copia el [código del esquema de ejemplo](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) y péguelo en un archivo de texto. Guarde el archivo como SampleSchema1.xml.  
  
2.  Cree la siguiente plantilla (ExplicitConversionB.xml) y guárdela en el mismo directorio donde esté guardado el archivo SampleSchema1.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Contact[string(@ContactID)="4"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (SampleSchema1.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el conjunto de resultados de ejecución de la plantilla:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Contact ContactID="4" LastName="Acevedo" FirstName="Humberto" Title="Sr." />   
</ROOT>  
```  
  
  
