---
title: Crear, modificar y quitar tablas | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- tables [SMO]
ms.assetid: ff0bcfff-812f-4999-b0c7-736a97804c2b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: acb2c3a5163bdb5e69d67b0f8c27d2c77d21a7be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63218254"
---
# <a name="creating-altering-and-removing-tables"></a>Crear, modificar y quitar tablas
  En los objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO), el objeto <xref:Microsoft.SqlServer.Management.Smo.Table> representa las tablas. En la jerarquía de objetos SMO, el objeto <xref:Microsoft.SqlServer.Management.Smo.Table> se encuentra por debajo del objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, debe elegir el entorno de programación, la plantilla de programación y el lenguaje en los que crear su aplicación. Para obtener más información, consulte [crear un proyecto de Visual Basic SMO en Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) o [crear un Visual C&#35; proyecto SMO en Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-table-in-visual-basic"></a>Crear, modificar y quitar una tabla en Visual Basic  
 En este ejemplo de código se crea una tabla que incluye varias columnas con tipos y propósitos diferentes. El código también proporciona ejemplos de cómo crear un campo de identidad, cómo crear una clave principal y cómo modificar las propiedades de la tabla.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBTable1](SMO How to#SMO_VBTable1)]  -->  
  
## <a name="creating-altering-and-removing-a-table-in-visual-c"></a>Crear, modificar y quitar una tabla en Visual C#  
 En este ejemplo de código se crea una tabla que incluye varias columnas con tipos y propósitos diferentes. El código también proporciona ejemplos de cómo crear un campo de identidad, cómo crear una clave principal y cómo modificar las propiedades de la tabla.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
        Server srv;   
        srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db;   
        db = srv.Databases["AdventureWorks2012"];   
        //Define a Table object variable by supplying the parent database and table name in the constructor.   
        Table tb;   
        tb = new Table(db, "Test_Table");   
        //Add various columns to the table.   
        Column col1;   
        col1 = new Column(tb, "Name", DataType.NChar(50));   
        col1.Collation = "Latin1_General_CI_AS";   
        col1.Nullable = true;   
        tb.Columns.Add(col1);   
        Column col2;   
        col2 = new Column(tb, "ID", DataType.Int);   
        col2.Identity = true;   
        col2.IdentitySeed = 1;   
        col2.IdentityIncrement = 1;   
        tb.Columns.Add(col2);   
        Column col3;   
        col3 = new Column(tb, "Value", DataType.Real);   
        tb.Columns.Add(col3);   
        Column col4;   
        col4 = new Column(tb, "Date", DataType.DateTime);   
        col4.Nullable = false;   
        tb.Columns.Add(col4);   
        //Create the table on the instance of SQL Server.   
        tb.Create();   
        //Add another column.   
        Column col5;   
        col5 = new Column(tb, "ExpiryDate", DataType.DateTime);   
        col5.Nullable = false;   
        tb.Columns.Add(col5);   
        //Run the Alter method to make the change on the instance of SQL Server.   
        tb.Alter();   
        //Remove the table from the database.   
        tb.Drop();   
        }  
```  
  
## <a name="creating-altering-and-removing-a-table-in-powershell"></a>Crear, modificar y quitar una tabla en PowerShell  
 En este ejemplo de código se crea una tabla que incluye varias columnas con tipos y propósitos diferentes. El código también proporciona ejemplos de cómo crear un campo de identidad, cómo crear una clave principal y cómo modificar las propiedades de la tabla.  
  
```  
#Load the assembly containing the objects used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.Types")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a SMO Table  
$tb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Table -argumentlist $db, "Test_Table"  
  
#Add various columns to the table.   
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::NChar(50)  
$col1 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Name", $Type  
$col1.Collation = "Latin1_General_CI_AS"  
$col1.Nullable = $true  
$tb.Columns.Add($col1)  
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Int  
$col2 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"ID", $Type  
$col2.Identity = $true  
$col2.IdentitySeed = 1  
$col2.IdentityIncrement = 1  
$tb.Columns.Add($col2)   
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Real  
$col3 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Value", $Type  
$tb.Columns.Add($col3)   
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$col4 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Date", $Type  
$col4.Nullable = $false  
$tb.Columns.Add($col4)   
  
#Create the table  
$tb.Create()  
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$col5 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"ExpiryDate", $Type  
$col5.Nullable = $false  
$tb.Columns.Add($col5)   
  
#Run the Alter method to make the change on the instance of SQL Server.   
$tb.Alter()  
  
#Remove the table from the database.   
$tb.Drop()  
  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.SqlServer.Management.Smo.Table>  
  
  
