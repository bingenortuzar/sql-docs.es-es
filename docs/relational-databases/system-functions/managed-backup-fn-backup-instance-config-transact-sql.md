---
title: managed_backup.fn_backup_instance_config (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_backup_instance_config
- smart_admin.fn_backup_instance_config_TSQL
- fn_backup_instance_config_TSQL
- smart_admin.fn_backup_instance_config
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_instance_config
- fn_backup_instance_config
ms.assetid: 2382a547-c0c9-4e1d-87c9-d8526192eb5a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 41c689d03ebae3afe16dc51d8a47c54e923d3a82
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067762"
---
# <a name="managedbackupfnbackupinstanceconfig-transact-sql"></a>managed_backup.fn_backup_instance_config (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila con la configuración predeterminada de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la instancia de SQL Server.  
  
 Utilice este procedimiento almacenado para revisar o para determinar la configuración predeterminada actual de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la instancia de SQL Server.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
managed_backup.fn_backup_db_config ()  
```  
  
##  <a name="Arguments"></a> Argumentos  
 None  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|is_smart_backup_enabled|INT|Muestra 1 cuando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitada y 0 cuando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está deshabilitada.|  
|credential_name|SYSNAME|La Credencial SQL predeterminada que se usa para autenticarse en el almacenamiento.|  
|retention_days|INT|Período de retención predeterminado establecido en el nivel de instancia.|  
|storage_url|NVARCHAR (1024)|La dirección URL de la cuenta de almacenamiento predeterminada establecida en el nivel de instancia.|  
|encryption_algorithm|SYSNAME|Nombre del algoritmo de cifrado. Se establece en NULL si no se especifica el cifrado.|  
|encryptor_type|NVARCHAR (32)|Tipo de sistema de cifrado usado: certificado o clave asimétrica. Se establece en NULL si no hay ningún sistema de cifrado especificado.|  
|encryptor_name|SYSNAME|Nombre del certificado o de la clave asimétrica. Se establece en NULL si no hay ningún nombre especificado|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Debe pertenecer a la **db_backupoperator** rol de base de datos con **ALTER ANY CREDENTIAL** permisos. El usuario no debe denegarse **VIEW ANY DEFINITION** permisos.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve la configuración predeterminada de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la instancia en la que se ejecuta:  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_instance_config ();  
  
```  
  
  
