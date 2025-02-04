---
title: Sys.dm_os_buffer_pool_extension_configuration (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_buffer_pool_extension_configuration
- sys.dm_os_buffer_pool_extension_configuration_TSQL
- dm_os_buffer_pool_extension_configuration_TSQL
- sys.dm_os_buffer_pool_extension_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_buffer_pool_extension_configuration dynamic management view
ms.assetid: d52cc481-4d29-4f33-b63d-231ec35d092f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 38e4e1ad85a5e968d4b0bb33a3a72a829942585b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900229"
---
# <a name="sysdmosbufferpoolextensionconfiguration-transact-sql"></a>sys.dm_os_buffer_pool_extension_configuration (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Devuelve la información de configuración de la extensión del grupo de búferes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Devuelve una fila por cada archivo de la extensión del grupo de búferes.  
  

  
| Nombre de columna | Tipo de datos | Descripción |
| :---------- | :-------- | :---------- |
|path|**nvarchar**(256)|Ruta y nombre de archivo de la memoria caché de la extensión del grupo de búferes. Acepta valores NULL.|  
|file_id|**int**|Identificador del archivo de la extensión del grupo de búferes. No admite valores NULL.|  
|state|**int**|Estado de la característica de extensión del grupo de búferes. No admite valores NULL.<br /><br /> 0: extensión del grupo de búferes deshabilitada<br /><br /> 1: deshabilitando extensión del grupo de búferes<br /><br /> 2: reservado para uso futuro<br /><br /> 3: habilitando extensión del grupo de búferes<br /><br /> 4: reservado para uso futuro<br /><br /> 5: extensión del grupo de búferes habilitada|  
|state_description|**nvarchar**(60)|Describe el estado de la característica de extensión del grupo de búferes. Acepta valores NULL.<br /><br /> 0 = EXTENSIÓN DEL GRUPO DE BÚFERES DESHABILITADA<br /><br /> 5 = EXTENSIÓN DEL GRUPO DE BÚFERES HABILITADA|
|current_size_in_kb|**bigint**|Tamaño actual del archivo de la extensión del grupo de búferes. No admite valores NULL.|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-configuration-buffer-pool-extension-information"></a>A. Devolver la información de la extensión del grupo de búferes de configuración  
 El ejemplo siguiente devuelve todas las columnas de la DMV sys.dm_os_buffer_pool_extension_configruation.  
  
```sql  
SELECT path, file_id, state, state_description, current_size_in_kb  
FROM sys.dm_os_buffer_pool_extension_configuration;  
```  
  
### <a name="b-returning-the-number-of-cached-pages-in-the-buffer-pool-extension-file"></a>b. Devolver el número de páginas en caché del archivo de la extensión del grupo de búferes  
 El ejemplo siguiente devuelve el número de páginas en caché de cada archivo de la extensión del grupo de búferes.  
  
```sql  
SELECT COUNT(*) AS cached_pages_count  
FROM sys.dm_os_buffer_descriptors  
WHERE is_in_bpool_extension <> 0  
;  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensión del grupo de búferes](../../database-engine/configure-windows/buffer-pool-extension.md)   
 [sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)  
  
  
