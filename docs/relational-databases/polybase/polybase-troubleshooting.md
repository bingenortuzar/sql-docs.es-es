---
title: Supervisión y solución de problemas de PolyBase | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- PolyBase, monitoring
- PolyBase, performance monitoring
helpviewer_keywords:
- PolyBase, troubleshooting
ms.assetid: f119e819-c3ae-4e0b-a955-3948388a9cfe
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: aboke
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 79edaf5c5940caf00cb03de98d532de400a553a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062025"
---
# <a name="monitor-and-troubleshoot-polybase"></a>Supervisión y solución de problemas de PolyBase

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Para solucionar problemas de PolyBase, use las técnicas que aparecen en este tema.

## <a name="catalog-views"></a>Vistas de catálogo

Use las vistas de catálogo que aparecen aquí para administrar las operaciones de PolyBase.

|||  
|-|-|  
|Ver|Descripción|  
|[sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)|Identifica tablas externas.|  
|[sys.external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)|Identifica orígenes de datos externos.|  
|[sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)|Identifica formatos de archivo externos.|  

## <a name="dynamic-management-views"></a>Vistas de administración dinámica  

|||  
|-|-|  
|[sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)|[sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)|  
|[sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|[sys.dm_exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|[sys.dm_exec_distributed_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-requests-transact-sql.md)|[sys.dm_exec_distributed_sql_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-sql-requests-transact-sql.md)|  
|[sys.dm_exec_dms_services &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)|[sys.dm_exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|[sys.dm_exec_external_operations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)|[sys.dm_exec_external_work &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)|  

Las consultas de PolyBase se dividen en una serie de pasos en sys.dm_exec_distributed_request_steps. En la tabla siguiente, se proporciona una asignación desde el nombre del paso a la DMV asociada.

|Paso de PolyBase|DMV asociada|  
|-|-|
|HadoopJobOperation | sys.dm_exec_external_operations|
|RandomIdOperation | sys.dm_exec_distributed_request_steps|
|HadoopRoundRobinOperation | sys.dm_exec_dms_workers|
|StreamingReturnOperation | sys.dm_exec_dms_workers|
|OnOperation | sys.dm_exec_distributed_sql_requests |

## <a name="to-monitor-polybase-queries-using-dmvs"></a>Para supervisar consultas de PolyBase con DMV

Supervise y solucione problemas de las consultas de PolyBase con los siguientes DMV.

1. **Encuentre las consultas que más tardan en ejecutarse**  

   Anote el id. de ejecución de la consulta que más tarda en ejecutarse.

   ```sql
    -- Find the longest running query  
   SELECT execution_id, st.text, dr.total_elapsed_time  
   FROM sys.dm_exec_distributed_requests  dr  
         cross apply sys.dm_exec_sql_text(sql_handle) st  
   ORDER BY total_elapsed_time DESC;  
   ```

1. **Encuentre el paso de la consulta distribuida que más tarda en ejecutarse**  

   Use el id. de ejecución que anotó en el paso anterior. Anote el índice de paso del paso que más tarda en ejecutarse.

   Compruebe el valor location_type del paso que más tarda en ejecutarse:  

   - HEAD o proceso: implica una operación SQL. Vaya al Paso 3a.

      - DMS: implica una operación del servicio de movimiento de datos de PolyBase. Vaya al Paso 3b.

      ```sql  
      -- Find the longest running step of the distributed query plan  
      SELECT execution_id, step_index, operation_type, distribution_type,   
      location_type, status, total_elapsed_time, command   
      FROM sys.dm_exec_distributed_request_steps   
      WHERE execution_id = 'QID4547'   
      ORDER BY total_elapsed_time DESC;  
      ```  

1. **Encuentre el progreso de la ejecución del paso que más tarda en ejecutarse**  

   1. **Encuentre el progreso de la ejecución de un paso de SQL**  

      Use el id. de ejecución y el índice de paso que anotó en los pasos anteriores. Use el id. de ejecución y el índice de paso que anotó en los pasos anteriores.

      ```sql  
      -- Find the execution progress of SQL step    
      SELECT execution_id, step_index, distribution_id, status,   
      total_elapsed_time, row_count, command   
      FROM sys.dm_exec_distributed_sql_requests   
      WHERE execution_id = 'QID4547' and step_index = 1;  
      ```  

   1. **Encuentre el progreso de la ejecución de un paso de DMS**

      Use el id. de ejecución y el índice de paso que anotó en los pasos anteriores.

      ```sql  
      -- Find the execution progress of DMS step    
      SELECT execution_id, step_index, dms_step_index, status,   
      type, bytes_processed, total_elapsed_time  
      FROM sys.dm_exec_dms_workers   
      WHERE execution_id = 'QID4547'   
      ORDER BY total_elapsed_time DESC;
      ```  

1. **Encuentre la información sobre las operaciones DMS externas**  

   Use el id. de ejecución y el índice de paso que anotó en los pasos anteriores.

   ```sql  
   SELECT execution_id, step_index, dms_step_index, compute_node_id,   
   type, input_name, length, total_elapsed_time, status   
   FROM sys.dm_exec_external_work   
   WHERE execution_id = 'QID4547' and step_index = 7   
   ORDER BY total_elapsed_time DESC;  
   ```  

## <a name="to-view-the--polybase-query-plan-to-be-changed"></a>Para ver el plan de consulta de PolyBase (y cambiarlo): 

1. En SSMS, habilite **Incluir plan de ejecución real** (Ctrl+M) y ejecute la consulta.

2. Haga clic en la pestaña **Plan de ejecución** .

   ![Plan de consulta de PolyBase](../../relational-databases/polybase/media/polybase-query-plan.png "Plan de consulta de PolyBase")  

3. Haga clic con el botón derecho en el **operador de consulta remota** y seleccione **Propiedades**.

4. Copie y pegue el valor de consulta remota en un editor de texto para ver el plan de consulta remota en formato XML. A continuación, se muestra un ejemplo.

   ```xml  

   <dsql_query number_nodes="1" number_distributions="8" number_distributions_per_node="8">  
      <sql>ExecuteMemo explain query</sql>  
      <dsql_operations total_cost="0" total_number_operations="6">  
        <dsql_operation operation_type="RND_ID">  
          <identifier>TEMP_ID_74</identifier>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_74] ([SensorKey] INT NOT NULL, [CustomerKey] INT NOT NULL, [GeographyKey] INT, [Speed] FLOAT(53) NOT NULL, [YearMeasured] INT NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">EXEC [tempdb].[sys].[sp_addextendedproperty] @name=N'IS_EXTERNAL_STREAMING_TABLE', @value=N'true', @level0type=N'SCHEMA', @level0name=N'dbo', @level1type=N'TABLE', @level1name=N'TEMP_ID_74'</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">UPDATE STATISTICS [tempdb].[dbo].[TEMP_ID_74] WITH ROWCOUNT = 2401, PAGECOUNT = 7</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="MULTI">  
          <dsql_operation operation_type="STREAMING_RETURN">  
            <operation_cost cost="1" accumulative_cost="1" average_rowsize="24" output_rows="5762.1" />  
            <location distribution="AllDistributions" />  
            <select>SELECT [T1_1].[SensorKey] AS [SensorKey],  
             [T1_1].[CustomerKey] AS [CustomerKey],  
             [T1_1].[GeographyKey] AS [GeographyKey],  
             [T1_1].[Speed] AS [Speed],  
             [T1_1].[YearMeasured] AS [YearMeasured]  
      FROM   (SELECT [T2_1].[SensorKey] AS [SensorKey],  
                     [T2_1].[CustomerKey] AS [CustomerKey],  
                     [T2_1].[GeographyKey] AS [GeographyKey],  
                     [T2_1].[Speed] AS [Speed],  
                     [T2_1].[YearMeasured] AS [YearMeasured]  
              FROM   [tempdb].[dbo].[TEMP_ID_74] AS T2_1  
              WHERE  ([T2_1].[Speed] > CAST (6.50000000000000000E+001 AS FLOAT))) AS T1_1</select>  
          </dsql_operation>  
          <dsql_operation operation_type="ExternalRoundRobinMove">  
            <operation_cost cost="16.594848" accumulative_cost="17.594848" average_rowsize="24" output_rows="19207" />  
            <external_uri>hdfs://10.193.26.177:8020/Demo/car_sensordata.tbl/</external_uri>  
            <destination_table>[TEMP_ID_74]</destination_table>  
          </dsql_operation>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_74]</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
      </dsql_operations>  
   </dsql_query>  
   ```  

## <a name="to-monitor-nodes-in-a-polybase-group"></a>Para supervisar los nodos de un grupo de PolyBase  

Después de configurar un conjunto de máquinas como parte de un grupo de escalado horizontal de PolyBase, puede supervisar el estado de las máquinas. Para obtener detalles sobre cómo crear un grupo de escalado horizontal, vea [Grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md).

1. Conéctese a SQL Server en el nodo principal de un grupo.

2. Ejecute la DMV [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) para ver todos los nodos del grupo de PolyBase.

3. Ejecute la DMV [sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md) para ver el estado de todos los nodos del grupo de PolyBase.

## <a name="hadoop-name-node-high-availability"></a>Alta disponibilidad de NameNode de Hadoop

Actualmente, PolyBase no se comunica con servicios de alta disponibilidad de NameNode como Zookeeper o Knox, pero existe una solución alternativa probada que se puede usar para ofrecer la funcionalidad.

Solución alternativa: Usar un nombre DNS para volver a enrutar las conexiones al NameNode activo. Para ello, debe asegurarse de que el origen de datos externo usa un nombre DNS para comunicarse con el NameNode. Si se produce una conmutación por error de NameNode, deberá cambiar la dirección IP asociada al nombre DNS usado en la definición del origen de datos externo. Se volverán a enrutar todas las conexiones nuevas al NameNode correcto. Las conexiones existentes generarán un error si se produce una conmutación por error. Para automatizar este proceso, un "latido" puede hacer ping en el NameNode activo. Si se produce un error en el latido, se puede suponer que se ha producido una conmutación por error y pasar automáticamente a las direcciones IP secundarias.

## <a name="error-messages-and-possible-solutions"></a>Mensajes de error y posibles soluciones

Para solucionar errores de tabla externa, consulte el blog de Murshed Zaman [https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/](https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/ "Errores y posibles soluciones de configuración de PolyBase").

## <a name="see-also"></a>Vea también

[Solución de problemas de conectividad de Kerberos con PolyBase](polybase-troubleshoot-connectivity.md)
