---
title: Especificar operadores booleanos en consultas XPath (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath operators [SQLXML]
- OR operator
- Boolean operators
- XPath queries [SQLXML], Boolean operators
- operators [SQLXML]
ms.assetid: 9928cff5-62ac-42aa-96bf-2e09a1df0bc3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29404c4a3dc7b4b10106e7a3a8cb170ffe1e7a3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010629"
---
# <a name="specifying-boolean-operators-in-xpath-queries-sqlxml-40"></a>Especificar operadores booleanos en consultas XPath (SQLXML 4.0)
  El ejemplo siguiente muestra cómo los operadores booleanos se especifican en consultas XPath. La consulta XPath de este ejemplo se especifica en el esquema de asignación que se incluye en SampleSchema1.xml. Para obtener información acerca de este esquema de ejemplo, vea [esquema de XSD anotado de ejemplo para obtener ejemplos de XPath &#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-specify-the-or-boolean-operator"></a>A. Especificar el operador booleano OR  
 Esta consulta XPath devuelve los  **\<cliente >** elementos secundarios del nodo de contexto con el **CustomerID** valor de atributo de 13 ó 31:  
  
```  
/child::Customer[attribute::CustomerID="13" or attribute::CustomerID="31"]  
```  
  
 Se puede especificar un acceso directo al eje `attribute` (@) y, puesto que el eje `child` es el valor predeterminado, puede omitirse:  
  
```  
/Customer[@CustomerID="13" or @CustomerID="31"]  
```  
  
 En el predicado, `attribute` es el eje y `CustomerID` es la prueba de nodo (TRUE si **CustomerID** es un  **\<atributo >** nodo, porque el  **\<atributo >** nodo es el nodo principal para el `attribute` eje). El predicado filtra los  **\<cliente >** elementos y devuelve solo aquellos que satisfacen la condición especificadas en el predicado.  
  
##### <a name="to-test-the-xpath-queries-against-the-mapping-schema"></a>Para probar las consultas XPath en el esquema de asignación  
  
1.  Copia el [código del esquema de ejemplo](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) y péguelo en un archivo de texto. Guarde el archivo como SampleSchema1.xml.  
  
2.  Cree la siguiente plantilla (BooleanOperatorsA.xml) y guárdela en el directorio donde esté guardado el archivo SampleSchema1.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[@CustomerID="13" or @CustomerID="31"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (SampleSchema1.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el conjunto de resultados de ejecución de la plantilla:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="31" SalesPersonID="286" TerritoryID="7" AccountNumber="31" CustomerType="S" Orders="Ord-51803 Ord-69427">  
    <Order SalesOrderID="Ord-51803" SalesPersonID="286" OrderDate="2003-08-01T00:00:00" DueDate="2003-08-13T00:00:00" ShipDate="2003-08-08T00:00:00">  
      <OrderDetail ProductID="Prod-718" UnitPrice="1059.31" OrderQty="1" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-838" UnitPrice="1059.31" OrderQty="1" UnitPriceDiscount="0" />   
    </Order>  
    <Order SalesOrderID="Ord-69427" SalesPersonID="286" OrderDate="2004-05-01T00:00:00" DueDate="2004-05-13T00:00:00" ShipDate="2004-05-08T00:00:00">  
      <OrderDetail ProductID="Prod-835" UnitPrice="440.1742" OrderQty="1" UnitPriceDiscount="0" />   
    </Order>  
  </Customer>  
</ROOT>  
```  
  
  
