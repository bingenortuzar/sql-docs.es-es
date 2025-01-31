---
title: MSSQLSERVER_2020 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2020 (Database Engine error)
ms.assetid: 4a8bf90f-a083-4c53-84f0-d23c711c8081
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e54a04cc9d787ae4d6d4545bbc5d9661bbba213d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869386"
---
# <a name="mssqlserver2020"></a>MSSQLSERVER_2020
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2020|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico||  
|Texto del mensaje|Las dependencias notificadas para la entidad "%.*ls" no incluyen referencias a las columnas. Esto se debe a que la entidad hace referencia a un objeto que no existe o a un error de una o varias instrucciones de la entidad.  Antes de volver a ejecutar la consulta, asegúrese de que no hay errores en la entidad y que existen todos los objetos a los que hace referencia la entidad.|  
  
## <a name="explanation"></a>Explicación  
 La función de sistema **sys.dm_sql_referenced_entities** notificará cualquier dependencia de nivel de columna para las referencias enlazadas a esquemas. Por ejemplo, la función notificará todas las dependencias de nivel de columna de una vista indizada, ya que una vista indizada requiere que se establezcan enlaces de esquema. Sin embargo, cuando la entidad a la que se hace referencia no está enlazada a un esquema, las dependencias de columna se notifican exclusivamente cuando todas las instrucciones incluidas en las columnas a las que se hace referencia se pueden enlazar. Las instrucciones se pueden enlazar correctamente solo si se analizan todos los objetos que contienen en ese momento. Si alguna instrucción definida en la entidad no se puede enlazar, las dependencias de columna no se notificarán y la columna **referenced_minor_id** devolverá 0. Cuando las dependencias de columna no se pueden devolver, se produce el error 2020. Este error no impide que la consulta devuelva dependencias de nivel de objeto.  
  
## <a name="user-action"></a>Acción del usuario  
 Corrija los errores identificados en el mensaje antes que el error 2020. Por ejemplo, en el siguiente ejemplo de código, la vista `Production.ApprovedDocuments` se define en las columnas `Title`, `ChangeNumber` y `Status` de la tabla `Production.Document`. La función de sistema **sys.dm_sql_referenced_entities** recibe consultas relacionadas con los objetos y las columnas de los que dependa la vista `ApprovedDocuments`. Como la vista no se crea utilizando la cláusula WITH SCHEMA_BINDING, las columnas a las que se hace referencia en la vista se pueden modificar en la tabla de referencia. En el ejemplo se modifica la columna `ChangeNumber` de la tabla `Production.Document` al cambiar el nombre a `TrackingNumber`. La vista de catálogo recibe de nuevo consultas de la vista `ApprovedDocuments`; sin embargo, no puede enlazarse a todas las columnas definidas en la vista. Se devuelven los errores 207 y 2020, que identifican el problema. A fin de resolver el problema, la vista debe modificarse para que refleje el nuevo nombre de la columna.  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `CREATE VIEW Production.ApprovedDocuments`  
  
 `AS`  
  
 `SELECT Title, ChangeNumber, Status`  
  
 `FROM Production.Document`  
  
 `WHERE Status = 2;`  
  
 `GO`  
  
 `SELECT referenced_schema_name AS schema_name`  
  
 `,referenced_entity_name AS table_name`  
  
 `,referenced_minor_name AS referenced_column`  
  
 `FROM sys.dm_sql_referenced_entities ('Production.ApprovedDocuments', 'OBJECT');`  
  
 `GO`  
  
 `EXEC sp_rename 'Production.Document.ChangeNumber', 'TrackingNumber', 'COLUMN';`  
  
 `GO`  
  
 `SELECT referenced_schema_name AS schema_name`  
  
 `,referenced_entity_name AS table_name`  
  
 `,referenced_minor_name AS referenced_column`  
  
 `FROM sys.dm_sql_referenced_entities ('Production.ApprovedDocuments', 'OBJECT');`  
  
 `GO`  
  
 La consulta devuelve los siguientes mensajes de error.  
  
 `Msg 207, Level 16, State 1, Procedure ApprovedDocuments, Line 3`  
  
 `Invalid column name 'ChangeNumber'.`  
  
 `Msg 2020, Level 16, State 1, Line 1`  
  
 `The dependencies reported for entity`  
  
 `"Production.ApprovedDocuments" do not include references to`  
  
 `columns. This is either because the entity references an`  
  
 `object that does not exist or because of an error in one or`  
  
 `more statements in the entity. Before rerunning the query,`  
  
 `ensure that there are no errors in the entity and that all`  
  
 `objects referenced by the entity exist.`  
  
 En el ejemplo siguiente se corrige el nombre de la columna en la vista.  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `ALTER VIEW Production.ApprovedDocuments`  
  
 `AS`  
  
 `SELECT Title,TrackingNumber, Status`  
  
 `FROM Production.Document`  
  
 `WHERE Status = 2;`  
  
 `GO`  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
  
