---
title: Sys.dm_audit_actions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_audit_actions_TSQL
- sys.dm_audit_actions
- dm_audit_actions_TSQL
- dm_audit_actions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_audit_actions dynamic management view
ms.assetid: b987c2b9-998a-4a5f-a82d-280dc6963cbe
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5e6a6c91cb31c9c3036bc95239f0aff9c75fda7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936976"
---
# <a name="sysdmauditactions-transact-sql"></a>sys.dm_audit_actions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Devuelve una fila por cada acción de auditoría sobre la que se puede guardar información en el registro de auditoría y por cada grupo de acciones de auditoría que se puede configurar como parte de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auditoría, consulte [SQL Server Audit &#40;motor de base de datos&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**action_id**|**varchar(4)**|Id. de la acción de auditoría. Relacionados con la **action_id** valor escrito en cada registro de auditoría. Acepta valores NULL. Es NULL para los grupos de auditoría.|  
|**action_in_log**|**bit**|Indica si una acción se puede escribir en un registro de auditoría. Los valores son los siguientes:<br /><br /> 1 = Sí<br /><br /> 0 = No|  
|**name**|**sysname**|Nombre de la acción de auditoría o del grupo de acciones de auditoría. No admite valores NULL.|  
|**class_desc**|**nvarchar(120)**|El nombre de la clase del objeto al que se aplica la acción de auditoría. Puede ser cualquiera de los objetos de ámbito de servidor, de base de datos o de esquema, pero no incluye los objetos de esquema. No admite valores NULL.|  
|**parent_class_desc**|**nvarchar(120)**|Nombre de la clase primaria del objeto descrito por class_desc. Es NULL si class_desc es Server.|  
|**covering_parent_action_name**|**nvarchar(120)**|Nombre de la acción de auditoría o del grupo de acciones de auditoría que contiene la acción de auditoría descrita en esta fila. Se usa para crear una jerarquía de acciones, incluyendo acciones de cobertura. Acepta valores NULL.|  
|**configuration_level**|**nvarchar(10)**|Indica que la acción o el grupo de acciones especificado en esta fila se puede configurar en el nivel de grupo o de acción. Es NULL si la acción no se puede configurar.|  
|**containing_group_name**|**nvarchar(120)**|El nombre del grupo de auditoría que contiene la acción especificada. Es NULL si el valor del nombre es un grupo.|  
  
## <a name="permissions"></a>Permisos  
 Las entidades de seguridad deben tener **seleccione** permiso. De forma predeterminada, dicho permiso se concede a Public.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Crear una auditoría de servidor y una especificación de auditoría de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
