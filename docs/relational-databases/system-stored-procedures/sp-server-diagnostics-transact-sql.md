---
title: sp_server_diagnostics (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_server_diagnostics
- sp_server_diagnostics_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_server_diagnostics
ms.assetid: 62658017-d089-459c-9492-c51e28f60efe
author: stevestein
ms.author: sstein
ms.openlocfilehash: 30ea7fba212cc99b8d6d7e58397d29731048c6f4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056292"
---
# <a name="spserverdiagnostics-transact-sql"></a>sp_server_diagnostics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Captura datos de diagnóstico e información de estado acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para detectar errores potenciales. El procedimiento se ejecuta en modo repetido y envía los resultados periódicamente. Se puede invocar desde una conexión DAC o normal.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_server_diagnostics [@repeat_interval =] 'repeat_interval_in_seconds'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @repeat_interval = ] 'repeat_interval_in_seconds'` Indica el intervalo de tiempo en que se ejecutará el procedimiento almacenado varias veces para enviar información de estado.  
  
 *repeat_interval_in_seconds* es **int** con el valor predeterminado es 0. Los valores válidos de los parámetros son 0 o cualquier valor mayor o igual que 5. El procedimiento almacenado tiene que ejecutarse al menos cinco segundos para devolver los datos completos. El tiempo mínimo que el procedimiento almacenado se ejecuta en el modo repetido es 5 segundos.  
  
 Si no se especifica este parámetro o si el valor especificado es 0, el procedimiento almacenado devolverá los datos una vez y, a continuación, saldrá.  
  
 Si el valor especificado es menor que el valor mínimo, generará un error y no devolverá nada.  
  
 Si el valor especificado es mayor o igual que 5, el procedimiento almacenado se ejecuta varias veces para devolver el estado de mantenimiento hasta que se cancele manualmente.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
**sp_server_diagnostics** devuelve la siguiente información  
  
|columna|Data type|Descripción|  
|------------|---------------|-----------------|  
|**creation_time**|**datetime**|Indica la marca de tiempo de creación de la fila. Cada fila de un conjunto de filas único tiene la misma marca de tiempo.|  
|**component_type**|**sysname**|Indica si la fila contiene información para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componente o de un grupo de disponibilidad Always On de nivel de instancia:<br /><br /> instance<br /><br /> AlwaysOn: AvailabilityGroup|  
|**component_name**|**sysname**|Indica el nombre del componente o el nombre del grupo de disponibilidad:<br /><br /> sistema<br /><br /> resource<br /><br /> query_processing<br /><br /> io_subsystem<br /><br /> events<br /><br /> *\<nombre del grupo de disponibilidad >*|  
|**state**|**int**|Indica el estado de mantenimiento del componente:<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> 3|  
|**state_desc**|**sysname**|Describe la columna de estado. Las descripciones que corresponden a los valores de la columna de estado son:<br /><br /> 0: Desconocido<br /><br /> 1: limpiar<br /><br /> 2: advertencia<br /><br /> 3: error|  
|**data**|**varchar (max)**|Especifica los datos que son específicos del componente.|  
  
 Estas son las descripciones de los cinco componentes:  
  
-   **sistema**: Recopila los datos desde la perspectiva del sistema en los bloqueos por subproceso, condiciones de procesamiento graves, tareas improductivas, errores de página y el uso de CPU. Esta información genera una recomendación del estado de mantenimiento total.  
  
-   **recurso**:  Recopila los datos desde una perspectiva de los recursos de memoria física y virtual, grupos de búferes, páginas, caché y otros objetos de memoria. Esta información genera una recomendación general del estado de mantenimiento.  
  
-   **query_processing**: Recopila los datos desde la perspectiva del procesamiento de consultas en los subprocesos de trabajo, tareas, tipos de espera, sesiones de uso intensivo de CPU y tareas de bloqueo. Esta información genera una recomendación general del estado de mantenimiento.  
  
-   **io_subsystem**: Recopila datos de E/S. Además de los datos de diagnóstico, este componente genera un estado de mantenimiento limpio o de advertencia solamente para un subsistema de E/S.  
  
-   **Eventos**: Recopila datos y superficies a través del procedimiento almacenado en los errores y eventos de interés registrados por el servidor, incluidos los detalles sobre las excepciones de búfer de anillo, los eventos de búfer de anillo acerca del agente de memoria, fuera de la memoria, el monitor del programador, el grupo de búferes, bloqueos por subproceso, seguridad y conectividad. Los eventos mostrarán siempre 0 como estado.  
  
-   **\<nombre del grupo de disponibilidad >** : Recopila datos para el grupo de disponibilidad especificado (si component_type = "siempre en: AvailabilityGroup").  
  
## <a name="remarks"></a>Comentarios  
Desde la perspectiva de los errores, los componentes del sistema, recursos y procesamiento de consultas se aprovecharán para la detección de errores mientras que los componentes de eventos e io_subsystem se aprovecharán solo con fines de diagnóstico.  
  
En la tabla siguiente se asignan los componentes a sus estados de mantenimiento asociados.  
  
|Componentes|Limpio (1)|Advertencia (2)|Error (3)|Desconocido (0)|  
|----------------|-----------------|-------------------|-----------------|--------------------|  
|sistema|x|x|x||  
|resource|x|x|x||  
|query_processing|x|x|x||  
|io_subsystem|x|x|||  
|events||||x|  
  
La (x) de cada fila representa los estados de mantenimiento válidos para el componente. Por ejemplo, io_subsystem se mostrará como limpio o como advertencia. No mostrará los estados de error.  
 
> [!NOTE]
> Ejecución de procedimiento interna sp_server_diagnostics se implementa en un subproceso con una prioridad alta preferente.
  
## <a name="permissions"></a>Permisos  
es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
Se recomienda utilizar sesiones extendidas para capturar la información de estado y guardarla en un archivo que se encuentre fuera de SQL Server. Por consiguiente, todavía puede acceder a ella si hay un error. En el siguiente ejemplo se guarda el resultado de una sesión de eventos en un archivo:  
```sql  
CREATE EVENT SESSION [diag]  
ON SERVER  
           ADD EVENT [sp_server_diagnostics_component_result] (set collect_data=1)  
           ADD TARGET [asynchronous_file_target] (set filename='c:\temp\diag.xel');  
GO  
ALTER EVENT SESSION [diag]  
      ON SERVER STATE = start;  
GO  
```  
  
La consulta de ejemplo siguiente lee el archivo de registro de sesión extendido:  
```sql  
SELECT  
    xml_data.value('(/event/@name)[1]','varchar(max)') AS Name  
  , xml_data.value('(/event/@package)[1]', 'varchar(max)') AS Package  
  , xml_data.value('(/event/@timestamp)[1]', 'datetime') AS 'Time'  
  , xml_data.value('(/event/data[@name=''component_type'']/value)[1]','sysname') AS Sysname  
  , xml_data.value('(/event/data[@name=''component_name'']/value)[1]','sysname') AS Component  
  , xml_data.value('(/event/data[@name=''state'']/value)[1]','int') AS State  
  , xml_data.value('(/event/data[@name=''state_desc'']/value)[1]','sysname') AS State_desc  
  , xml_data.query('(/event/data[@name="data"]/value/*)') AS Data  
FROM   
(  
      SELECT  
                        object_name as event  
                        ,CONVERT(xml, event_data) as xml_data  
       FROM    
      sys.fn_xe_file_target_read_file('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\*.xel', NULL, NULL, NULL)  
)   
AS XEventData  
ORDER BY time;  
```  
  
En el siguiente ejemplo se captura el resultado de sp_server_diagnostics en una tabla en un modo no repetido:  
```sql  
CREATE TABLE SpServerDiagnosticsResult  
(  
      create_time DateTime,  
      component_type sysname,  
      component_name sysname,  
      state int,  
      state_desc sysname,  
      data xml  
);  
INSERT INTO SpServerDiagnosticsResult  
EXEC sp_server_diagnostics; 
```  

En la consulta de ejemplo siguiente se lee la salida de resumen de la tabla:  
```sql  
SELECT create_time,
       component_name,
       state_desc 
FROM SpServerDiagnosticsResult;  
``` 

En la consulta de ejemplo siguiente se leen parte de los resultados detallados de cada componente de la tabla:  
```sql  
-- system
select data.value('(/system/@systemCpuUtilization)[1]','bigint') as 'System_CPU',
   data.value('(/system/@sqlCpuUtilization)[1]','bigint') as 'SQL_CPU',
   data.value('(/system/@nonYieldingTasksReported)[1]','bigint') as 'NonYielding_Tasks',
   data.value('(/system/@pageFaults)[1]','bigint') as 'Page_Faults',
   data.value('(/system/@latchWarnings)[1]','bigint') as 'Latch_Warnings',
   data.value('(/system/@BadPagesDetected)[1]','bigint') as 'BadPages_Detected',
   data.value('(/system/@BadPagesFixed)[1]','bigint') as 'BadPages_Fixed'
from SpServerDiagnosticsResult 
where component_name like 'system'
go

-- Resource Monitor
select data.value('(./Record/ResourceMonitor/Notification)[1]', 'VARCHAR(max)') AS [Notification],
    data.value('(/resource/memoryReport/entry[@description=''Working Set'']/@value)[1]', 'bigint')/1024 AS [SQL_Mem_in_use_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Paging File'']/@value)[1]', 'bigint')/1024 AS [Avail_Pagefile_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Physical Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_Physical_Mem_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Virtual Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_VAS_MB],
    data.value('(/resource/@lastNotification)[1]','varchar(100)') as 'LastNotification',
    data.value('(/resource/@outOfMemoryExceptions)[1]','bigint') as 'OOM_Exceptions'
from SpServerDiagnosticsResult 
where component_name like 'resource'
go

-- Nonpreemptive waits
select waits.evt.value('(@waitType)','varchar(100)') as 'Wait_Type',
   waits.evt.value('(@waits)','bigint') as 'Waits',
   waits.evt.value('(@averageWaitTime)','bigint') as 'Avg_Wait_Time',
   waits.evt.value('(@maxWaitTime)','bigint') as 'Max_Wait_Time'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/topWaits/nonPreemptive/byDuration/wait') AS waits(evt)
where component_name like 'query_processing'
go

-- Preemptive waits
select waits.evt.value('(@waitType)','varchar(100)') as 'Wait_Type',
   waits.evt.value('(@waits)','bigint') as 'Waits',
   waits.evt.value('(@averageWaitTime)','bigint') as 'Avg_Wait_Time',
   waits.evt.value('(@maxWaitTime)','bigint') as 'Max_Wait_Time'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/topWaits/preemptive/byDuration/wait') AS waits(evt)
where component_name like 'query_processing'
go

-- CPU intensive requests
select cpureq.evt.value('(@sessionId)','bigint') as 'SessionID',
   cpureq.evt.value('(@command)','varchar(100)') as 'Command',
   cpureq.evt.value('(@cpuUtilization)','bigint') as 'CPU_Utilization',
   cpureq.evt.value('(@cpuTimeMs)','bigint') as 'CPU_Time_ms'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/cpuIntensiveRequests/request') AS cpureq(evt)
where component_name like 'query_processing'
go

-- Blocked Process Report
select blk.evt.query('.') as 'Blocked_Process_Report_XML'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/blockingTasks/blocked-process-report') AS blk(evt)
where component_name like 'query_processing'
go

-- IO
select data.value('(/ioSubsystem/@ioLatchTimeouts)[1]','bigint') as 'Latch_Timeouts',
   data.value('(/ioSubsystem/@totalLongIos)[1]','bigint') as 'Total_Long_IOs'
from SpServerDiagnosticsResult 
where component_name like 'io_subsystem'
go

-- Event information
select xevts.evt.value('(@name)','varchar(100)') as 'xEvent_Name',
   xevts.evt.value('(@package)','varchar(100)') as 'Package',
   xevts.evt.value('(@timestamp)','datetime') as 'xEvent_Time',
   xevts.evt.query('.') as 'Event Data'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/events/session/RingBufferTarget/event') AS xevts(evt)
where component_name like 'events'
go  
``` 
  
## <a name="see-also"></a>Vea también  
 [Directiva de conmutación por error para instancias de clústeres de conmutación por error](../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  
