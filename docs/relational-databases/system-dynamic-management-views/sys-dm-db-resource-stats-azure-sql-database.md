---
title: Sys. DM _ _db_resource_stats (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 05/21/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 71efbc5abad150c599a674ea66409207fc2bf628
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471082"
---
# <a name="sysdmdbresourcestats-azure-sql-database"></a>sys.dm_db_resource_stats (base de datos SQL de Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve el consumo de CPU, E/S y memoria para una base de datos [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Hay una fila para cada 15 segundos, incluso si no hay ninguna actividad en la base de datos. Los datos históricos se conservan durante una hora.  
  
|Columnas|Tipo de datos|Descripción|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|Hora UTC que indica el fin del intervalo de informes actual.|  
|avg_cpu_percent|**decimal (5, 2)**|Uso de proceso promedio como porcentaje del límite del nivel de servicio.|  
|avg_data_io_percent|**decimal (5, 2)**|Uso promedio de e/s de datos en porcentaje del límite del nivel de servicio.|  
|avg_log_write_percent|**decimal (5, 2)**|Promedio de escrituras del registro de transacciones (en MBps) como porcentaje del límite del nivel de servicio.|  
|avg_memory_usage_percent|**decimal (5, 2)**|Uso de memoria promedio como porcentaje del límite del nivel de servicio.<br /><br /> Esto incluye la memoria usada para las páginas del grupo de búferes y el almacenamiento de objetos OLTP en memoria.|  
|xtp_storage_percent|**decimal (5, 2)**|Uso del almacenamiento para OLTP en memoria en porcentaje del límite del nivel de servicio (al final del intervalo de informes). Esto incluye la memoria usada para el almacenamiento de los siguientes objetos OLTP en memoria: tablas, índices y variables de tabla con optimización para memoria. También incluye la memoria usada para procesar las operaciones de ALTER TABLE.<br /><br /> Devuelve 0 si no se utiliza OLTP en memoria en la base de datos.|  
|max_worker_percent|**decimal (5, 2)**|Número máximo de trabajos simultáneos (solicitudes) en porcentaje del límite del nivel de servicio de la base de datos.|  
|max_session_percent|**decimal (5, 2)**|Número máximo de sesiones simultáneas en porcentaje del límite del nivel de servicio de la base de datos.|  
|dtu_limit|**int**|Valor actual máximo de DTU de base de datos para esta base de datos durante este intervalo. En el caso de las bases de datos que usan el modelo basado en núcleo virtual, esta columna es NULL.|
|cpu_limit|**decimal (5, 2)**|Número de núcleos virtuales para esta base de datos durante este intervalo. En el caso de las bases de datos que usan el modelo basado en DTU, esta columna es NULL.|
|avg_instance_cpu_percent|**decimal (5, 2)**|Uso promedio de la CPU de la base de datos como porcentaje del proceso de base de datos de SQL.|
|avg_instance_memory_percent|**decimal (5, 2)**|Promedio de uso de memoria de base de datos como porcentaje del proceso de base de datos de SQL.|
|avg_login_rate_percent|**decimal (5, 2)**|Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.|
|replica_role|**int**|Representa el rol de la réplica actual con 0 como principal, 1 como secundario y 2 como reenviador (principal de la secundaria geográfica). Verá "1" cuando esté conectado con intención de solo lectura a todas las secundarias legibles. Si se conecta a una región secundaria geográfica sin especificar la intención de solo lectura, debería ver "2" (conexión al reenviador).|
|||
  
> [!TIP]  
>  Para más información sobre estos límites y los niveles de servicio, consulte los temas [niveles](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) de servicio y [capacidades y límites de nivel](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)de servicio.  
  
## <a name="permissions"></a>Permisos  
 Esta vista necesita el permiso VIEW DATABASE STATE.  
  
## <a name="remarks"></a>Comentarios  
 Los datos devueltos por **Sys. DM _ _db_resource_stats** se expresan como un porcentaje de los límites máximos permitidos para el nivel de servicio/nivel de rendimiento que se está ejecutando.
 
 Si la base de datos se conmutó por error a otro servidor en los últimos 60 minutos, la vista solo devolverá datos correspondientes al tiempo que ha sido la base de datos principal desde la conmutación por error.  
  
 Para obtener una vista menos granular de estos datos, use la vista de catálogo **Sys. resource_stats** en la base de datos **maestra** . Esta vista captura datos cada 5 minutos y mantiene datos históricos durante 14 días.  Para obtener más información, vea [Sys. &#40;resource_stats&#41;Azure SQL Database](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md).  
  
 Cuando una base de datos es miembro de un grupo elástico, las estadísticas de recursos que se presentan como valores porcentuales se expresan como el porcentaje del límite máximo de las bases de datos establecidas en la configuración del grupo elástico.  
  
## <a name="example"></a>Ejemplo  
  
El ejemplo siguiente devuelve los datos del uso de recursos ordenados por la hora más reciente de la base de datos conectada actualmente.  
  
```  
SELECT * FROM sys.dm_db_resource_stats ORDER BY end_time DESC;  
  
```  
  
 En el ejemplo siguiente se identifica el promedio de consumo de DTU en términos de porcentaje del límite máximo permitido de DTU en el nivel de rendimiento de la base de datos de usuario durante la última hora. Considere aumentar el nivel de rendimiento de estos porcentajes a casi el 100 % de forma coherente.  
  
```  
SELECT end_time,   
  (SELECT Max(v)    
   FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS    
   value(v)) AS [avg_DTU_percent]   
FROM sys.dm_db_resource_stats;  
  
```  
  
 El ejemplo siguiente devuelve los valores máximo y promedio de porcentaje de CPU, la E/S de datos y registro, así como el consumo de memoria durante la última hora.  
  
```  
SELECT    
    AVG(avg_cpu_percent) AS 'Average CPU Utilization In Percent',   
    MAX(avg_cpu_percent) AS 'Maximum CPU Utilization In Percent',   
    AVG(avg_data_io_percent) AS 'Average Data IO In Percent',   
    MAX(avg_data_io_percent) AS 'Maximum Data IO In Percent',   
    AVG(avg_log_write_percent) AS 'Average Log Write I/O Throughput Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write I/O Throughput Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys. resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [Niveles de servicio](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Capacidades y límites del nivel de servicio](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
