---
title: sp_rename (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_rename_TSQL
- sp_rename
dev_langs:
- TSQL
helpviewer_keywords:
- renaming indexes
- renaming columns
- sp_rename
- renaming tables
ms.assetid: bc3548f0-143f-404e-a2e9-0a15960fc8ed
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 070c2a362a69fb6863cc263da3975efc66c7c9f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006934"
---
# <a name="sprename-transact-sql"></a>sp_rename (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cambia el nombre de un objeto creado por el usuario en la base de datos actual. Este objeto puede ser una tabla, índice, columna, tipo de datos alias, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] tipo definido por el usuario de common language runtime (CLR).  
  
> [!CAUTION]  
>  Al cambiar cualquier parte del nombre de un objeto se pueden interrumpir scripts y procedimientos almacenados. Se recomienda no utilizar esta instrucción para cambiar el nombre a procedimientos almacenados, desencadenadores, funciones definidas por el usuario o vistas; en su lugar, quite el objeto y vuelva a crearlo con el nuevo nombre.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_rename [ @objname = ] 'object_name' , [ @newname = ] 'new_name'   
    [ , [ @objtype = ] 'object_type' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @objname =] '*object_name*'  
 Es el nombre actual completo o incompleto del objeto de usuario o tipo de datos. Si el objeto se va a cambiar es una columna de una tabla, *object_name* debe tener el formato *table.column* o *esquema.tabla.columna*. Si el objeto se va a cambiar es un índice, *object_name* debe tener el formato *table.index* o *schema.table.index*. Si el objeto se va a cambiar es una restricción, *object_name* debe tener el formato *schema.constraint*.  
  
 Las comillas solo se necesitan si se especifica un objeto completo. Si se proporciona un nombre completo, incluido el nombre de la base de datos, el nombre de la base de datos debe ser el de la base de datos actual. *object_name* es **nvarchar(776)** , no tiene ningún valor predeterminado.  
  
 [ @newname =] '*new_name*'  
 Es el nuevo nombre del objeto especificado. *new_name* debe ser un nombre de una sola parte y debe seguir las reglas para identificadores. *NewName* es **sysname**, no tiene ningún valor predeterminado.  
  
> [!NOTE]  
>  Los nombres de los desencadenadores no pueden comenzar por # o ##.  
  
 [ @objtype =] '*object_type*'  
 Es el tipo de objeto cuyo nombre se va a cambiar. *object_type* es **varchar (13)** , su valor predeterminado es null, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|COLUMN|Una columna cuyo nombre se va a cambiar.|  
|DATABASE|Una base de datos definida por el usuario. Este tipo de objeto es necesario cuando se cambia el nombre de una base de datos|  
|INDEX|Índice definido por el usuario. Si se cambia el nombre a un índice con estadísticas, también se cambia automáticamente a las estadísticas.|  
|OBJECT|Realiza un seguimiento de un elemento de un tipo en [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). Por ejemplo, OBJECT podría utilizarse para cambiar el nombre de objetos como restricciones (CHECK, FOREIGN KEY, PRIMARY o UNIQUE KEY), tablas de usuario y reglas.|  
|STATISTICS|**Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Estadísticas que crea un usuario explícitamente o que se crean implícitamente con un índice. Si se cambia el nombre de las estadísticas de un índice, también se cambia automáticamente el nombre del índice.|  
|USERDATATYPE|Un [tipos definidos por el usuario CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) agregados mediante la ejecución [CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md) o [sp_addtype](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md).|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o un número distinto de cero (error)  
  
## <a name="remarks"></a>Comentarios  
 Solo se puede cambiar el nombre de un objeto o tipo de datos de la base de datos actual. No se pueden cambiar los nombres de la mayoría de los tipos de datos y objetos del sistema.  
  
 sp_rename cambia automáticamente el nombre del índice asociado cuando se cambia el nombre de una restricción PRIMARY KEY o UNIQUE. Si un índice cuyo nombre se ha cambiado está enlazado a una restricción PRIMARY KEY, sp_rename también cambia automáticamente el nombre de esta restricción.  
  
 sp_rename se puede utilizar para cambiar el nombre de los índices XML principales y secundarios.  
  
 Cambiar el nombre de un procedimiento almacenado, función, vista o desencadenador no cambiará el nombre del objeto correspondiente en la columna de definición de la [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) vista de catálogo, o bien obtenido usando la [OBJECT_ DEFINICIÓN](../../t-sql/functions/object-definition-transact-sql.md) función integrada. Por lo tanto, se recomienda no utilizar sp_rename para cambiar el nombre a estos tipos de objetos. En su lugar, quite el objeto y vuelva a crearlo con su nuevo nombre.  
  
 Al cambiar el nombre de un objeto como una tabla o columna, no se cambia automáticamente el nombre de las referencias a ese objeto. Es necesario modificar de forma manual los objetos que hacen referencia al objeto cuyo nombre se ha cambiado. Por ejemplo, si se cambia el nombre de una columna de una tabla y en un desencadenador existe una referencia a esa columna, es necesario modificar el desencadenador para reflejar el nuevo nombre de la columna. Use [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) para ver las dependencias del objeto antes de cambiarle el nombre.  
  
## <a name="permissions"></a>Permisos  
 Para cambiar el nombre de objetos, columnas e índices, se necesita permiso ALTER en el objeto. Para cambiar el nombre de tipos de usuario, se necesita el permiso CONTROL en el tipo. Para cambiar el nombre de una base de datos, debe pertenecer a los roles fijos de servidor sysadmin o dbcreator.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-renaming-a-table"></a>A. Cambiar el nombre de una tabla  
 En el siguiente ejemplo se cambia el nombre de la tabla `SalesTerritory` por `SalesTerr` en el esquema `Sales` .  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
GO  
```  
  
### <a name="b-renaming-a-column"></a>b. Cambiar el nombre de una columna  
 El ejemplo siguiente se cambia el nombre el `TerritoryID` columna en el `SalesTerritory` tabla `TerrID`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';  
GO  
```  
  
### <a name="c-renaming-an-index"></a>C. Cambiar el nombre de un índice  
 En el siguiente ejemplo se cambia el nombre del índice `IX_ProductVendor_VendorID` por `IX_VendorID`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';  
GO  
```  
  
### <a name="d-renaming-an-alias-data-type"></a>D. Cambiar el nombre de un tipo de datos de alias  
 En el siguiente ejemplo se cambia el nombre del tipo de datos de alias `Phone` por `Telephone`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_rename N'Phone', N'Telephone', N'USERDATATYPE';  
GO  
```  
  
### <a name="e-renaming-constraints"></a>E. Cambiar el nombre de las restricciones  
 En los siguientes ejemplos se cambia el nombre de las restricciones PRIMARY KEY, CHECK y FOREIGN KEY. Al cambiar el nombre de una restricción, debe especificarse el esquema al que pertenece.  
  
```  
USE AdventureWorks2012;   
GO  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');   
GO  
  
-- Rename the primary key constraint.  
sp_rename 'HumanResources.PK_Employee_BusinessEntityID', 'PK_EmployeeID';  
GO  
  
-- Rename a check constraint.  
sp_rename 'HumanResources.CK_Employee_BirthDate', 'CK_BirthDate';  
GO  
  
-- Rename a foreign key constraint.  
sp_rename 'HumanResources.FK_Employee_Person_BusinessEntityID', 'FK_EmployeeID';  
  
-- Return the current Primary Key, Foreign Key and Check constraints for the Employee table.  
SELECT name, SCHEMA_NAME(schema_id) AS schema_name, type_desc  
FROM sys.objects  
WHERE parent_object_id = (OBJECT_ID('HumanResources.Employee'))   
AND type IN ('C','F', 'PK');  
  
```  
  
```  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_Person_BusinessEntityID   HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_BusinessEntityID          HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_Employee_BirthDate                 HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
name                                  schema_name        type_desc  
------------------------------------- ------------------ ----------------------  
FK_Employee_ID                        HumanResources     FOREIGN_KEY_CONSTRAINT  
PK_Employee_ID                        HumanResources     PRIMARY_KEY_CONSTRAINT  
CK_BirthDate                          HumanResources     CHECK_CONSTRAINT  
CK_Employee_MaritalStatus             HumanResources     CHECK_CONSTRAINT  
CK_Employee_HireDate                  HumanResources     CHECK_CONSTRAINT  
CK_Employee_Gender                    HumanResources     CHECK_CONSTRAINT  
CK_Employee_VacationHours             HumanResources     CHECK_CONSTRAINT  
CK_Employee_SickLeaveHours            HumanResources     CHECK_CONSTRAINT  
  
(7 row(s) affected)  
  
```  
  
### <a name="f-renaming-statistics"></a>F. Cambiar el nombre de las estadísticas  
 El ejemplo siguiente crea un objeto de estadísticas denominado contactMail1 y, a continuación, cambia el nombre de la estadística para el nuevo contacto mediante sp_rename. Al cambiar el nombre de las estadísticas, el objeto se debe especificar con el formato schema.table.statistics_name.  
  
```  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
  
sp_rename 'Person.Person.ContactMail1', 'NewContact','Statistics';  
  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
