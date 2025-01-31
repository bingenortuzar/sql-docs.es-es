---
title: sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governor
- sys.resource_governor_TSQL
- resource_governor
- resource_governor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: f94cc3ccd0278a3ae2f46707f2680f8d198db58a
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70873919"
---
# <a name="sysdm_resource_governor_resource_pools_history_ex-transact-sql"></a>sys.dm_resource_governor_resource_pools_history_ex (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

Devuelve una instantánea en un intervalo de 20 segundos para los últimos 32 minutos (128 archivos en total) de las estadísticas de grupos de recursos para un Azure SQL Database.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**pool_id**|int|Identificador del grupo de recursos. No admite valores NULL.
|**name**|sysname|Nombre del grupo de recursos. No admite valores NULL.|
|**snapshot_time**|datetime2|Fecha y hora de la instantánea de estadísticas del grupo de recursos tomada|
|**duration_ms**|int|Duración entre la instantánea actual y la anterior|
|**statistics_start_time**|datetime2|La hora en que se restablecieron las estadísticas para este grupo. No admite valores NULL.|
|**active_session_count**|int|Total de sesiones activas en la instantánea actual|
|**active_worker_count**|int|Total de trabajos en la instantánea actual|
|**delta_cpu_usage_ms**|int|Uso de CPU en milisegundos desde la última instantánea. No admite valores NULL.|
|**delta_cpu_usage_preemptive_ms**|int|Las llamadas preferentes Win32 no rigen por el RG de CPU de SQL, desde la última instantánea|
|**used_data_space_kb**|bigint|Espacio total usado en las bases de datos de usuario asociadas con el grupo de usuarios|
|**allocated_disk_space_kb**|bigint|Tamaño total de los archivos de datos de las bases de datos de usuario en el grupo de usuarios asociado a|
|**target_memory_kb**|bigint|La cantidad de memoria de destino, en kilobytes, que el grupo de recursos de servidor está intentando lograr. Depende de la configuración actual y del estado del servidor. No admite valores NULL.|
|**used_memory_kb**|bigint|La cantidad de memoria utilizada, en kilobytes, para el grupo de recursos de servidor. No admite valores NULL.|
|**cache_memory_kb**|bigint|El uso de la memoria caché total actual en kilobytes. No admite valores NULL.|
|**compile_memory_kb**|bigint|El uso de memoria descartada total actual en kilobytes (kB). La mayoría de este uso sería para la compilación y optimización, pero también puede incluir otros usuarios de la memoria. No admite valores NULL.|
|**active_memgrant_count**|bigint|El número actual de concesiones de memoria. No admite valores NULL.|
|**active_memgrant_kb**|bigint|La suma, en kilobytes (kB), de las concesiones actuales de memoria. No admite valores NULL.|
|**used_memgrant_kb**|bigint|La memoria usada (descartada) total actual de las concesiones de memoria. No admite valores NULL.|
|**delta_memgrant_timeout_count**|int|recuento de los tiempos de espera de concesión de memoria en este grupo de recursos de este período. No admite valores NULL.|
|**delta_memgrant_waiter_count**|int|El número de consultas pendientes actualmente en concesiones de memoria. No admite valores NULL.|
|**delta_out_of_memory_count**|int|El número de asignaciones de memoria con errores en el grupo desde la última instantánea. No admite valores NULL.|
|**delta_read_io_queued**|int|Número total de e/s de lectura en cola desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_read_io_issued**|int|Número total de e/s de lectura emitidos desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_read_io_completed**|int|Número total de e/s de lectura completadas desde la última instantánea. No admite valores NULL.|
|**delta_read_io_throttled**|int|Número total de e/s de lectura limitados desde la instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_read_bytes**|bigint|Número total de bytes leídos desde la última instantánea. No admite valores NULL.|
|**delta_read_io_stall_ms**|int|Tiempo total (en milisegundos) entre la llegada y finalización de e/s de lectura desde la última instantánea. No admite valores NULL.|
|**delta_read_io_stall_queued_ms**|int|Tiempo total (en milisegundos) entre la llegada de e/s de lectura y el problema desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S. Un delta_read_io_stall_queued_ms distinto de cero significa que la e/s se ve afectada por RG.|
|**delta_write_io_queued**|int|Número total de e/s de escritura en cola desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_write_io_issued**|int|Número total de e/s de escritura emitidas desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_write_io_completed**|int|Número total de e/s de escritura completadas desde la última instantánea. No admite valores NULL|
|**delta_write_io_throttled**|int|Número total de e/s de escritura limitado desde la última instantánea. No admite valores NULL|
|**delta_write_bytes**|bigint|Número total de bytes escritos desde la última instantánea. No admite valores NULL.|
|**delta_write_io_stall_ms**|int|Tiempo total (en milisegundos) entre la llegada y finalización de e/s de escritura desde la última instantánea. No admite valores NULL.|
|**delta_write_io_stall_queued_ms**|int|Tiempo total (en milisegundos) entre la llegada de e/s de escritura y el problema desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**delta_io_issue_delay_ms**|int|Tiempo total (en milisegundos) entre el problema programado y el problema real de e/s desde la última instantánea. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**max_iops_per_volume**|int|La configuración máxima de e/s por segundo (IOPS) por volumen de disco para este grupo. Acepta valores NULL. Es NULL si el grupo de recursos de servidor no está regulado para las operaciones de E/S.|
|**max_memory_kb**|bigint|La cantidad máxima de memoria, en kilobytes, que el grupo de recursos de servidor puede tener. Depende de la configuración actual y del estado del servidor. No admite valores NULL.
|**max_log_rate_kb**|bigint|Velocidad de registro máxima (kilobytes por segundo) en el nivel de grupo de recursos.|
|**max_data_space_kb**|bigint|Límite máximo de almacenamiento de grupo elástico para este grupo elástico en kilobytes.|
|**max_session**|int|Límite de sesión para el grupo|
|**max_worker**|int|Límite de trabajo para el grupo|
|**min_cpu_percent**|int|La configuración actual del ancho banda de la CPU promedio garantizado para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. No admite valores NULL.|
|**max_cpu_percent**|int|La configuración actual del ancho banda de la CPU promedio máximo permitido para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. No admite valores NULL.|
|**cap_cpu_percent**|int|El límite máximo de ancho de banda de la CPU que recibirán todas las solicitudes en el grupo de recursos. Limita el nivel de ancho de banda máximo de la CPU según el nivel especificado. El intervalo permitido para el valor es de 1 a 100. No admite valores NULL.|
|**min_vcores**|decimal (5, 2)|La configuración actual del ancho banda de la CPU promedio garantizado para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU.  En unidades de núcleos virtuales|
|**max_vcores**|decimal (5, 2)|La configuración actual del ancho banda de la CPU promedio máximo permitido para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU.  En unidad de núcleos virtuales|
|**cap_vcores**|decimal (5, 2)|El límite máximo de ancho de banda de la CPU que recibirán todas las solicitudes en el grupo de recursos.  En unidad en núcleos virtuales|
|**instance_cpu_count**|int|Número de CPU configuradas para la instancia|
|**instance_cpu_percent|decimal (5, 2)|Porcentaje de CPU configurado para la instancia|
|**instance_vcores**|decimal (5, 2)|Número de núcleos virtuales configurados para la instancia|
|**delta_log_bytes_used**|decimal (5, 2)|Generación total de registros (en bytes) en el nivel de grupo desde la última instantánea|
|**avg_login_rate_percent**|decimal (5, 2)|Número de inicios de sesión desde la última instantánea, en comparación con el límite de inicio de sesión|
|**delta_vcores_used**|decimal (5, 2)|Uso de Compute en el recuento de núcleos virtuales desde la última instantánea.|
|**cap_vcores_used_percent**|decimal (5, 2)|Uso de proceso promedio en porcentaje del límite del grupo.|
|**instance_vcores_used_percent**|decimal (5, 2)|Uso de proceso promedio en porcentaje del límite de la instancia de SQL.|
|**avg_data_io_percent**|decimal (5, 2)|Uso de e/s promedio en porcentaje según el límite del grupo.|
|**avg_log_write_percent**|decimal (5, 2)|Uso de recursos de escritura promedio en porcentaje del límite del grupo.|
|**avg_storage_percent**|decimal (5, 2)|Uso de almacenamiento medio en porcentaje del límite de almacenamiento del grupo.|
|**avg_allocated_storage_percent**|decimal (5, 2)|El porcentaje de espacio de datos asignado por todas las bases de datos del grupo elástico. Esta es la proporción de espacio de datos asignado al tamaño máximo de los datos para el grupo elástico. Para obtener más información, consulte: Administración del espacio de archivo en SQL Database|
|**max_worker_percent**|decimal (5, 2)|Número máximo de trabajos simultáneos (solicitudes) en porcentaje según el límite del grupo.|
|**max_session_percent**|decimal (5, 2)|Número máximo de sesiones simultáneas en porcentaje según el límite del grupo.|
|||

## <a name="permissions"></a>Permisos

Esta vista requiere el permiso VIEW SERVER STATE.

## <a name="remarks"></a>Comentarios

Los usuarios pueden tener acceso a esta vista de administración dinámica para supervisar el consumo de recursos casi en tiempo real para el grupo de cargas de trabajo de usuario, así como los grupos internos del sistema de la instancia de Azure SQL Database.

> [!IMPORTANT]
> La mayoría de los datos expuestos por esta DMV están destinados al consumo interno y están sujetos a cambios.

## <a name="examples"></a>Ejemplos

En el ejemplo siguiente se devuelven los datos de velocidad de registro máximo y el consumo en cada instantánea por grupo de usuarios  

```sql
select snapshot_time, name, max_log_rate_kb, delta_log_bytes_used from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

En el ejemplo siguiente se devuelve información similar a sys. elastic_pool_resource_stats sin tener que conectarse a la maestra lógica

```sql
select snapshot_time, name, cap_vcores_used_percent,
  avg_data_io_percent,  
  avg_log_write_percent,
  avg_storage_percent,
  avg_allocated_storage_percent,
  max_data_space_kb,
  max_worker_percent,
  max_session_percent
    from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

## <a name="see-also"></a>Vea también

- [Gobierno de velocidad de registro de traducción](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [Límites de recursos de DTU de grupo elástico](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [Límites de recursos de núcleo virtual de grupo elástico](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
