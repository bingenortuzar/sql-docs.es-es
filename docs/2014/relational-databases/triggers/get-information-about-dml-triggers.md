---
title: Obtener información sobre los desencadenadores DML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- metadata [SQL Server], triggers
- viewing DML triggers
- DML triggers, metadata
- displaying DML triggers
- status information [SQL Server], triggers
- DML triggers, viewing
ms.assetid: 37574aac-181d-4aca-a2cc-8abff64237dc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dc207c4c1bc7ddc2c7c4f590622e04a0f7739375
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62698751"
---
# <a name="get-information-about-dml-triggers"></a>Obtener información acerca de los desencadenadores DML
  En este tema se describe cómo obtener información acerca de los desencadenadores DML en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esta información puede incluir los tipos de desencadenadores de una tabla, el nombre de un desencadenador, su propietario y la fecha en que se creó o modificó. Si el desencadenador no se cifró cuando se creó, se obtiene la definición del desencadenador. Puede usar la definición para entender cómo un desencadenador afecta a la tabla en la que se define. También puede averiguar los objetos que usa un desencadenador específico. Con esta información, puede identificar los objetos que afectan al desencadenador, en el caso de que se modifiquen o se eliminen de la base de datos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para obtener información acerca de los desencadenadores DML, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 **sys.sql.modules**, **sys.object**, **sys.triggers**, **sys.events**, **sys.trigger_events**  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../security/metadata-visibility-configuration.md).  
  
 OBJECT_DEFINITION, OBJECTPROPERTY, **sp_helptext**  
 Debe pertenecer al rol **public** . La definición de objetos de usuario está visible para el propietario del objeto o para los receptores que dispongan de uno de los siguientes permisos: ALTER, CONTROL, TAKE OWNERSHIP o VIEW DEFINITION. Estos permisos corresponden implícitamente a los miembros de los roles fijos de base de datos **db_owner**, **db_ddladmin**y **db_securityadmin** .  
  
 **sys.sql_expression_dependencies**  
 Necesita el permiso VIEW DEFINITION en la base de datos y el permiso SELECT en **sys.sql_expression_dependencies** para la base de datos. De forma predeterminada, solo se concede el permiso SELECT a los miembros del rol fijo de base de datos **db_owner** . Si se conceden los permisos SELECT y VIEW DEFINITION a otro usuario, el receptor puede ver todas las dependencias de la base de datos.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-view-the-definition-of-a-dml-trigger"></a>Para ver la definición de un desencadenador DML  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda la base de datos que desee, expanda **Tablas**y, a continuación, expanda la tabla que contiene el desencadenador cuya definición desea ver.  
  
3.  Expanda **Desencadenadores**, haga clic con el botón derecho en el desencadenador que quiera y, luego, haga clic en **Modificar**. La definición del desencadenador DML aparecerá en la ventana de consulta.  
  
#### <a name="to-view-the-dependencies-of-a-dml-trigger"></a>Para ver las dependencias de un desencadenador DML  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda la base de datos que desee, expanda **Tablas**y, a continuación, expanda la tabla que contiene el desencadenador y sus dependencias que desea ver.  
  
3.  Expanda **Desencadenadores**, haga clic con el botón derecho en el desencadenador que quiere y, luego, haga clic en **Ver dependencias**.  
  
4.  En la ventana **Dependencias del objeto**, para ver los objetos que dependen del desencadenador DML, seleccione **Objetos que dependen de \<nombre del desencadenador DML>**. Los objetos aparecerán en el área **Dependencias** .  
  
     Para ver los objetos de los que depende el DML, seleccione **Objetos de los que depende \<nombre del desencadenador DML>**. Los objetos aparecerán en el área **Dependencias** . Expanda cada nodo para ver todos los objetos.  
  
5.  Para obtener información sobre un objeto que aparece en el área **Dependencias** , haga clic en el objeto. En el campo **Objeto seleccionado** , la información se proporciona en los cuadros **Nombre**, **Tipo**y **Tipo de dependencia** .  
  
6.  Para cerrar la ventana **Dependencias del objeto** , haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-view-the-definition-of-a-dml-trigger"></a>Para ver la definición de un desencadenador DML  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue uno de los ejemplos siguientes en la ventana de consulta y haga clic en **Ejecutar**. En cada ejemplo se muestra cómo puede ver la definición del desencadenador `iuPerson` .  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT definition   
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID(N'Person.iuPerson');   
GO  
```  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'Person.iuPerson')) AS ObjectDefinition;   
GO  
  
```  
  
```sql  
USE AdventureWorks2012;   
GO  
EXEC sp_helptext 'Person.iuPerson'  
GO  
  
```  
  
#### <a name="to-view-the-dependencies-of-a-dml-trigger"></a>Para ver las dependencias de un desencadenador DML  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue uno de los ejemplos siguientes en la ventana de consulta y haga clic en **Ejecutar**. En cada ejemplo se muestra cómo puede ver las dependencias del desencadenador `iuPerson` .  
  
```  
USE AdventureWorks2012;   
GO  
SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc, referenced_class_desc,   
    referenced_server_name, referenced_database_name, referenced_schema_name,   
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,   
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referencing_id = OBJECT_ID(N'Person.iuPerson');   
GO  
  
```  
  
#### <a name="to-view-information-about-dml-triggers-in-the-database"></a>Para ver información acerca de los desencadenadores DML de la base de datos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue uno de los ejemplos siguientes en la ventana de consulta y haga clic en **Ejecutar**. En cada ejemplo se muestra cómo puede ver la información acerca de los desencadenadores DML (`TR`) de la base de datos.  
  
```  
USE AdventureWorks2012;   
GO  
SELECT  name, parent_id, create_date, modify_date, is_instead_of_trigger  
FROM sys.triggers  
WHERE type = 'TR';   
GO  
  
```  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT  name, object_id, schema_id, parent_object_id, type_desc, create_date, modify_date, is_published  
FROM sys.objects  
WHERE type = 'TR';   
GO  
  
```  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT OBJECTPROPERTY(OBJECT_ID(N'Person.iuPerson'), 'ExecIsInsteadOfTrigger');   
GO  
  
```  
  
#### <a name="to-view-information-about-events-that-fire-a-dml-trigger"></a>Para ver información acerca de los eventos que activan un desencadenador DML  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue uno de los ejemplos siguientes en la ventana de consulta y haga clic en **Ejecutar**. En cada ejemplo se muestra cómo puede ver los eventos que activan el desencadenador `iuPerson` .  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT object_id, type, type_desc, is_trigger_event, event_group_type, event_group_type_desc   
FROM sys.events  
WHERE object_id = OBJECT_ID('Person.iuPerson');   
GO  
```  
  
```sql  
USE AdventureWorks2012;   
GO   
SELECT object_id, type,is_first, is_last  
FROM sys.trigger_events  
WHERE object_id = OBJECT_ID('Person.iuPerson');   
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/enable-trigger-transact-sql)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/disable-trigger-transact-sql)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)   
 [sp_rename &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [sp_help &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-transact-sql)   
 [sp_helptrigger &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptrigger-transact-sql)   
 [sys.triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql)   
 [sys.trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-trigger-events-transact-sql)   
 [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)   
 [sys.server_triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectpropertyex-transact-sql)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](/sql/t-sql/functions/object-definition-transact-sql)  
  
  
