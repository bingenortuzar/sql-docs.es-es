---
title: Sys.dm_exec_query_resource_semaphores (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_query_resource_semaphores_TSQL
- dm_exec_query_resource_semaphores_TSQL
- sys.dm_exec_query_resource_semaphores
- dm_exec_query_resource_semaphores
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_resource_semaphores dynamic management view
ms.assetid: e43a2aa9-dd52-4c89-911e-1a7d05f7ffbb
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 026c13a461d6b4efe7244a08a9f3cdbe117deee9
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255282"
---
# <a name="sysdmexecqueryresourcesemaphores-transact-sql"></a>sys.dm_exec_query_resource_semaphores (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve la información acerca del estado actual del semáforo de recursos de consulta en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **Sys.dm_exec_query_resource_semaphores** proporciona el estado general de ejecución de consultas y permite determinar si el sistema puede tener acceso a suficiente memoria. Esta vista complementa la información de la memoria obtenida [sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md) para proporcionar una imagen completa del estado de la memoria de servidor. **Sys.dm_exec_query_resource_semaphores** devuelve una fila para el semáforo de recursos normal y otra fila para el semáforo de recursos de consultas pequeñas. Hay dos requisitos para un semáforo de consultas pequeñas:  
  
-   La concesión de memoria solicitada debe ser inferior a 5 MB.  
  
-   El costo de la consulta debe ser inferior a 3 unidades de costo  
  
> [!NOTE]  
>  Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_exec_query_resource_semaphores**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**resource_semaphore_id**|**smallint**|Id. no único del semáforo de recursos. 0 para el semáforo de recursos normal y 1 para el semáforo de recursos de consultas pequeñas.|  
|**target_memory_kb**|**bigint**|Concede el destino de uso en kilobytes.|  
|**max_target_memory_kb**|**bigint**|Máximo destino potencial en kilobytes. Es NULL para el semáforo de recursos de consultas pequeñas.|  
|**total_memory_kb**|**bigint**|Memoria mantenida por el semáforo de recursos en kilobytes. Si el sistema está bajo presión de memoria o si mínima forzada ha concedido la memoria es con frecuencia, este valor puede ser mayor que el **target_memory_kb** o **max_target_memory_kb** valores. La memoria total es una suma de la memoria disponible y concedida.|  
|**available_memory_kb**|**bigint**|Memoria disponible para una nueva concesión en kilobytes.|  
|**granted_memory_kb**|**bigint**|Memoria concedida total en kilobytes.|  
|**used_memory_kb**|**bigint**|Parte físicamente usada de la memoria concedida en kilobytes.|  
|**grantee_count**|**int**|Número de consultas activas que tienen sus concesiones satisfechas.|  
|**waiter_count**|**int**|Número de consultas que esperan que sus concesiones se satisfagan.|  
|**timeout_error_count**|**bigint**|Número total de errores de tiempo de espera desde el inicio del servidor. Es NULL para el semáforo de recursos de consultas pequeñas.|  
|**forced_grant_count**|**bigint**|Número total concesiones de memoria mínima forzada desde el inicio del servidor. Es NULL para el semáforo de recursos de consultas pequeñas.|  
|**pool_id**|**int**|Id. del grupo de recursos de servidor al que pertenece este semáforo de recursos.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requieren el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere el **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.   
  
## <a name="remarks"></a>Comentarios  
 Las consultas que utilizan vistas de administración dinámica que incluyen ORDER BY o agregados pueden aumentar el consumo de memoria y, de esta forma, contribuir al problema que están solucionando.  
  
 Usar **sys.dm_exec_query_resource_semaphores** para solucionar problemas, pero no se incluye en las aplicaciones que se va a usar las versiones futuras de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La característica del regulador de recursos permite que un administrador de bases de datos distribuya los recursos del servidor entre los grupos de recursos de servidor, hasta un máximo de 64 fondos. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores, cada grupo se comporta como una pequeña instancia independiente del servidor y requiere dos semáforos.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica y funciones relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
  


