---
title: 'Excluir elementos de esquema del documento XML resultante mediante sql: mapped (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- element does not map [SQLXML]
- annotated XSD schemas, excluding schema elements
- mapped annotation
- table mapping [SQLXML], excluding schema elements
- sql:mapped
- excluding schema elements
- element mapping [SQLXML], excluding schema elements
- column mapping [SQLXML]
- XSD schemas [SQLXML], excluding schema elements
- attribute mapping [SQLXML], excluding schema elements
- table/view mapping [SQLXML], excluding schema elements
ms.assetid: 7d2649dd-0038-4a2c-b16d-f80f7c306966
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 865a9af892f948e77aa593d3713766e7860349b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013860"
---
# <a name="excluding-schema-elements-from-the-resulting-xml-document-using-sqlmapped-sqlxml-40"></a>Excluir elementos de esquema del documento XML resultante mediante sql:mapped (SQLXML 4.0)
  Cada elemento y atributo del esquema XSD se asigna a una tabla/vista y columna de base de datos debido a la asignación predeterminada. Si desea crear un elemento en el esquema XSD que no se asigne a ninguna tabla (vista) o columna de base de datos y que no aparezca en el XML, puede especificar la anotación `sql:mapped`.  
  
 La anotación `sql:mapped` es especialmente útil si no se puede modificar el esquema o si se utiliza para validar XML de otros orígenes y, aun así, contiene datos que no están almacenados en su base de datos. La anotación `sql:mapped` difiere de `sql:is-constant` en que los elementos y atributos no asignados no aparecen en el documento XML.  
  
 La anotación `sql:mapped` toma un valor booleano (0 = false, 1 = true). Los valores permitidos son 0, 1, true y false.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, consulte [requisitos para ejecutar los ejemplos de SQLXML](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlmapped-annotation"></a>A. Especificar la anotación sql:mapped  
 Suponga que tiene un esquema XSD de algún otro origen. Este esquema XSD consta de un  **\<Person.Contact >** elemento con **ContactID**, **FirstName**, **LastName**, y **HomeAddress** atributos.  
  
 En este esquema XSD de asignación a la tabla Person.Contact en la base de datos AdventureWorks, `sql:mapped` se especifica en el **HomeAddress** atributo porque la tabla Employees no almacena direcciones particulares de los empleados. Por consiguiente, este atributo no se asigna a la base de datos y no se devuelve en el documento XML resultante cuando se especifica una consulta XPath en el esquema de asignación.  
  
 Para el resto del esquema se produce una asignación predeterminada. El  **\<Person.Contact >** elemento se asigna a la tabla Person.Contact y todos los atributos se asignan a las columnas con el mismo nombre en la tabla Person.Contact.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact">  
    <xsd:complexType>  
      <xsd:attribute name="ContactID"   type="xsd:string"/>  
      <xsd:attribute name="FirstName"    type="xsd:string" />  
      <xsd:attribute name="LastName"     type="xsd:string" />  
      <xsd:attribute name="HomeAddress" type="xsd:string"   
                     sql:mapped="false" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta de XPath de ejemplo con respecto al esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como sql-mapped.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como sql-mappedT.xml en el mismo directorio donde guardó sql-mapped.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-mapped.xml">  
            /Person.Contact[@ContactID < 10]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (MySchema.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\sql-mapped.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas SQLXML](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el conjunto de resultados:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact ContactID="1" FirstName="Gustavo" LastName="Achong" />   
  <Person.Contact ContactID="2" FirstName="Catherine" LastName="Abel" />   
  <Person.Contact ContactID="3" FirstName="Kim" LastName="Abercrombie" />   
  <Person.Contact ContactID="4" FirstName="Humberto" LastName="Acevedo" />   
  <Person.Contact ContactID="5" FirstName="Pilar" LastName="Ackerman" />   
  <Person.Contact ContactID="6" FirstName="Frances" LastName="Adams" />   
  <Person.Contact ContactID="7" FirstName="Margaret" LastName="Smith" />   
  <Person.Contact ContactID="8" FirstName="Carla" LastName="Adams" />   
  <Person.Contact ContactID="9" FirstName="Jay" LastName="Adams" />   
</ROOT>  
```  
  
 Observe que ContactID, FirstName y LastName están presentes, pero no lo está HomeAddress porque el esquema de asignación especificó 0 para el atributo `sql:mapped`.  
  
## <a name="see-also"></a>Vea también  
 [Asignación predeterminada de atributos y elementos XSD a tablas y columnas &#40;SQLXML 4.0&#41;](default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
  
