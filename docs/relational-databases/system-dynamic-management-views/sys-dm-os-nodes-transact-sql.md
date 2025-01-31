---
title: sys.dm_os_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b2b6f88e857ab7fc6300698174914126fb0881f6
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265734"
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Un componente interno denominado SQLOS crea las estructuras de nodo que imitan el procesador de hardware. Estas estructuras se pueden cambiar mediante el uso de [soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md) para crear diseños de nodo personalizados.  

> [!NOTE]
> A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usará automáticamente soft-NUMA para determinadas configuraciones de hardware. Para obtener más información, consulte [Soft-NUMA automática](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa).
  
En la tabla siguiente se proporciona información acerca de estos nodos.  
  
> [!NOTE]
> Para llamar a esta DMV de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_nodes**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|Identificador del nodo.|  
|node_state_desc|**nvarchar(256)**|Descripción del estado del nodo. Los valores se muestran primero con los valores mutuamente exclusivos, seguidos de los valores combinables. Por ejemplo:<br /> Online, Thread Resources Low, Lazy Preemptive<br /><br />Hay cuatro valores node_state_desc mutuamente excluyentes. Que aparecen a continuación con sus descripciones.<br /><ul><li>ONLINE: Nodo está en línea<li>OFFLINE: Nodo está sin conexión<li>IDLE: Nodo no tiene ninguna solicitud de trabajo pendiente y ha entrado en un estado de inactividad.<li>IDLE_READY: Nodo no tiene ninguna solicitud de trabajo pendiente y está preparado para entrar en un estado de inactividad.</li></ul><br />Hay tres valores node_state_desc combinables, enumerados a continuación con sus descripciones.<br /><ul><li>DAC: Este nodo se reserva para el [conexión administrativa dedicada](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).<li>THREAD_RESOURCES_LOW: No hay ningún subproceso nuevo puede crearse en este nodo debido a una condición de memoria baja.<li>AGREGADO SIN INTERRUPCIÓN: Indica los nodos se agregaron en respuesta a eventos de CPU de agregar un acceso rápido.</li></ul>|  
|memory_object_address|**varbinary(8)**|Dirección del objeto de memoria asociada con este nodo. Relación uno a uno con [sys.dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).memory_object_address.|  
|memory_clerk_address|**varbinary(8)**|Dirección de distribuidor de memoria asociada con este nodo. Relación uno a uno con [sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).memory_clerk_address.|  
|io_completion_worker_address|**varbinary(8)**|La dirección del trabajador asignada a la realización de E/S para este nodo. Relación uno a uno con [sys.dm_os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).worker_address.|  
|memory_node_id|**smallint**|Identificador del nodo de memoria al que pertenece este nodo. Relación de varios a uno con [sys.dm_os_memory_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md).memory_node_id.|  
|cpu_affinity_mask|**bigint**|Mapa de bits que identifica las CPU con las que este nodo está asociado.|  
|online_scheduler_count|**smallint**|Número de programadores en línea que están administrados por este nodo.|  
|idle_scheduler_count|**smallint**|Número de programadores en línea que no tienen ningún trabajador activo.|  
|active_worker_count|**int**|Número de trabajadores que están activos en todos los programadores administrados por este nodo.|  
|avg_load_balance|**int**|Promedio de tareas por programador en este nodo.|  
|timer_task_affinity_mask|**bigint**|Mapa de bits que identifica los programadores que pueden tener asignadas tareas de temporizador.|  
|permanent_task_affinity_mask|**bigint**|Mapa de bits que identifica los programadores que pueden tener asignadas tareas permanentes.|  
|resource_monitor_state|**bit**|Cada nodo tiene asignado un monitor de recursos. El monitor de recursos puede estar en ejecución o inactivo. El valor 1 indica en ejecución y 0 inactividad.|  
|online_scheduler_mask|**bigint**|Identifica la máscara de afinidad de proceso para este nodo.|  
|processor_group|**smallint**|Identifica el grupo de procesadores para este nodo.|  
|cpu_count |**int** |Número de CPU disponibles para este nodo. |
|pdw_node_id|**int**|El identificador para el nodo en esta distribución.<br /><br /> **Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requieren el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere el **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.   

## <a name="see-also"></a>Vea también    
 [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
