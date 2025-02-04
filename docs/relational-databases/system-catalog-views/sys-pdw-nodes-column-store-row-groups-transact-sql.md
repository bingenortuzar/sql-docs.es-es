---
title: sys.pdw_nodes_column_store_row_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 17a4c925-d4b5-46ee-9cd6-044f714e6f0e
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: e89405e04a06e8171c69b81066be743ee99d4534
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106709"
---
# <a name="syspdwnodescolumnstorerowgroups-transact-sql"></a>sys.pdw_nodes_column_store_row_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Proporciona información de índices de almacén de columnas agrupado en una base por segmento para ayudar al administrador de decisiones de sistema de administración en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. **Sys.pdw_nodes_column_store_row_groups** tiene una columna para el número total de filas almacenadas físicamente (incluidas las marcadas como eliminadas) y una columna para el número de filas marcadas como eliminadas. Use **sys.pdw_nodes_column_store_row_groups** para determinar qué fila grupos tienen un alto porcentaje de filas eliminadas y deben volver a generar.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. de la tabla subyacente. Se trata de la tabla física en el nodo de proceso, no el object_id de la tabla lógica en el nodo de Control. Por ejemplo, object_id no coincide con el valor object_id en sys.tables.<br /><br /> Para unir con sys.tables, use sys.pdw_index_mappings.|  
|**index_id**|**int**|Id. del índice agrupado en *object_id* tabla.|  
|**partition_number**|**int**|Identificador de la partición de tabla que contiene el grupo de filas *row_group_id*. Puede usar *partition_number* para unir Esta DMV a sys.partitions.|  
|**row_group_id**|**int**|Id. de este grupo de filas. Es único en la partición.|  
|**dellta_store_hobt_id**|**bigint**|El hobt_id para los grupos de filas delta, o NULL si el tipo del grupo de filas no es delta. Un grupo de filas delta es un grupo de filas de lectura/escritura que acepta nuevos registros. Un grupo de filas delta tiene el **abierto** estado. Un grupo de filas delta está todavía en formato de almacén de filas y no se ha comprimido al formato de almacén de columnas.|  
|**state**|**tinyint**|Número de identificación asociado con el state_description.<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED|  
|**state_desccription**|**nvarchar(60)**|Descripción del estado persistente del grupo de filas:<br /><br /> Abra - un grupo de filas de lectura/escritura que acepta nuevos registros. Un grupo de filas abierto está todavía en formato de almacén de filas y no se ha comprimido al formato de almacén de columnas.<br /><br /> CERRADO: un grupo de filas que se ha rellenado, pero el proceso de tupla motriz aún no se han comprimido.<br /><br /> COMPRIMIR - un grupo de filas que se ha rellenado y comprimido.|  
|**total_rows**|**bigint**|Total de filas almacenadas físicamente en el grupo de filas. Es posible que se hayan eliminado algunas, pero estas se siguen almacenando. El número máximo de filas en un grupo de filas es 1.048.576 (hexadecimal FFFFF).|  
|**deleted_rows**|**bigint**|Número de filas almacenadas físicamente en el grupo de filas que están marcadas para eliminación.<br /><br /> Siempre 0 para diferencias grupos de filas.|  
|**size_in_bytes**|**int**|Tamaño total, en bytes, de todas las páginas de este grupo de filas. Este tamaño no incluye el tamaño necesario para almacenar los metadatos o diccionarios compartidos.|  
|**pdw_node_id**|**int**|Identificador único de un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nodo.|  
|**distribution_id**|**int**|Identificador único de la distribución.|
  
## <a name="remarks"></a>Comentarios  
 Devuelve una fila para cada grupo de filas del almacén de columnas de cada tabla que tenga un índice clúster o no clúster de almacén de columnas.  
  
 Use **sys.pdw_nodes_column_store_row_groups** para determinar el número de filas incluido en el grupo de filas y el tamaño del grupo de filas.  
  
 Cuando el número de filas eliminadas de un grupo de filas alcanza un alto porcentaje de las filas totales, la tabla pierde eficiencia. Vuelva a generar el índice de almacén de columnas para reducir el tamaño de la tabla, reduciendo así la E/S de disco necesaria para leer la tabla. Para volver a generar el uso del índice de almacén de columnas el **RECOMPILAR** opción de la **ALTER INDEX** instrucción.  
  
 El almacén de columnas actualizable primero inserta nuevos datos en un **abierto** grupo de filas, que está en formato de almacén de filas y, a veces también se denomina tabla delta.  Una vez que un grupo de filas abierto está lleno, su estado cambia a **cerrado**. La tupla motriz comprime un grupo de filas cerrado en formato de almacén de columnas y el estado cambia a **comprimida**.  La tupla motriz es un proceso en segundo plano que de forma periódica se despierta y comprueba si hay grupos de filas cerrados listos para comprimirse en un grupo de filas de almacén de columnas.  La tupla motriz también cancela la asignación de los grupos de filas en los que se han borrado todas las filas. Desasignadas los grupos de filas se marcan como **retirado**. Para ejecutar la tupla motriz inmediatamente, use el **REORGANIZAR** opción de la **ALTER INDEX** instrucción.  
  
 Cuando se ha rellenado un grupo de filas de almacén de columnas, se comprime y ya no se aceptan filas nuevas. Cuando se eliminan filas de un grupo comprimido, siguen estando allí pero están marcadas como eliminadas. Las actualizaciones de un grupo comprimido se implementan como una eliminación del grupo comprimido, y como una inserción en un grupo abierto.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso **VIEW SERVER STATE**.  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 El ejemplo siguiente combina el **sys.pdw_nodes_column_store_row_groups** tabla con otras tablas del sistema para devolver información sobre tablas específicas. La columna `PercentFull` calculada es una estimación de la eficacia del grupo de filas. Para buscar información en un única tabla, quite los guiones de comentario delante de la cláusula WHERE y proporcione un nombre de tabla.  
  
```  
SELECT IndexMap.object_id,   
  object_name(IndexMap.object_id) AS LogicalTableName,   
  i.name AS LogicalIndexName, IndexMap.index_id, NI.type_desc,   
  IndexMap.physical_name AS PhyIndexNameFromIMap,   
  CSRowGroups.*,  
  100*(ISNULL(deleted_rows,0))/total_rows AS PercentDeletedRows   
FROM sys.tables AS t  
JOIN sys.indexes AS i  
    ON t.object_id = i.object_id  
JOIN sys.pdw_index_mappings AS IndexMap  
    ON i.object_id = IndexMap.object_id  
    AND i.index_id = IndexMap.index_id  
JOIN sys.pdw_nodes_indexes AS NI  
    ON IndexMap.physical_name = NI.name  
    AND IndexMap.index_id = NI.index_id  
JOIN sys.pdw_nodes_column_store_row_groups AS CSRowGroups  
    ON CSRowGroups.object_id = NI.object_id   
    AND CSRowGroups.pdw_node_id = NI.pdw_node_id  
AND CSRowGroups.index_id = NI.index_id      
--WHERE t.name = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, IndexMap.physical_name, pdw_node_id;  
```  

La siguiente [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] ejemplo cuenta las filas por partición para columnas agrupadas almacenan también cómo muchas filas están en grupos de filas Compressed, cerrado o abierto:  

```
SELECT
    s.name AS [Schema Name]
    ,t.name AS [Table Name]
    ,rg.partition_number AS [Partition Number]
    ,SUM(rg.total_rows) AS [Total Rows]
    ,SUM(CASE WHEN rg.State = 1 THEN rg.Total_rows Else 0 END) AS [Rows in OPEN Row Groups]
    ,SUM(CASE WHEN rg.State = 2 THEN rg.Total_Rows ELSE 0 END) AS [Rows in Closed Row Groups]
    ,SUM(CASE WHEN rg.State = 3 THEN rg.Total_Rows ELSE 0 END) AS [Rows in COMPRESSED Row Groups]
FROM sys.pdw_nodes_column_store_row_groups rg
JOIN sys.pdw_nodes_tables pt
ON rg.object_id = pt.object_id AND rg.pdw_node_id = pt.pdw_node_id AND pt.distribution_id = rg.distribution_id
JOIN sys.pdw_table_mappings tm
ON pt.name = tm.physical_name
INNER JOIN sys.tables t
ON tm.object_id = t.object_id
INNER JOIN sys.schemas s
ON t.schema_id = s.schema_id
GROUP BY s.name, t.name, rg.partition_number
ORDER BY 1, 2
```
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  
