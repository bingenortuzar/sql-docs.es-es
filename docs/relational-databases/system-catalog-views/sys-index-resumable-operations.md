---
title: sys.index_resumable_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: ''
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d4f79da2af2630fa54a06dc26b32cf22287f7c1d
ms.sourcegitcommit: 853c2c2768caaa368dce72b4a5e6c465cc6346cf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71227197"
---
# <a name="sysindex_resumable_operations-transact-sql"></a>Sys. index_resumable_operations (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**Sys. index_resumable_operations** es una vista del sistema que supervisa y comprueba el estado de ejecución actual de la recompilación de índices reanudables.  
**Se aplica a**: SQL Server 2017 y Azure SQL Database
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|IDENTIFICADOR del objeto al que pertenece este índice (no acepta valores NULL).|  
|**index_id**|**int**|IDENTIFICADOR del índice (no acepta valores NULL). el número de la **secuencia es único** en el objeto.|
|**Nombre**|**sysname**|Nombre del índice. **Name** es único solo dentro del objeto.|  
|**sql_text**|**nvarchar(max)**|Texto de la instrucción de T-SQL DDL|
|**last_max_dop**|**smallint**|Última MAX_DOP usada (valor predeterminado = 0)|
|**partition_number**|**int**|Número de partición dentro del índice o montón propietario. En el caso de las tablas e índices sin particiones, o en caso de que se vuelvan a generar todas las particiones, el valor de esta columna es NULL.|
|**state**|**tinyint**|Estado operativo del índice reanudable:<br /><br />0 = en ejecución<br /><br />1 = pausa|
|**state_desc**|**nvarchar(60)**|Descripción del estado operativo de un índice reanudable (en ejecución o en pausa)|  
|**start_time**|**datetime**|Hora de inicio de la operación de índice (no acepta valores NULL)|
|**last_pause_time**|**datatime**| Hora de última pausa de operación de índice (que acepta valores NULL). NULL si la operación se está ejecutando y nunca está en pausa.|
|**total_execution_time**|**int**|Tiempo total de ejecución desde la hora de inicio en minutos (no acepta valores NULL)|
|**percent_complete**|**real**|Finalización del progreso de la operación de índice en% (no acepta valores NULL).|
|**page_count**|**bigint**|Número total de páginas de índice asignadas por la operación de generación de índice para los índices nuevos y de asignación (no acepta valores NULL).

## <a name="permissions"></a>Permisos

[!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  

## <a name="example"></a>Ejemplo

 Muestra todas las operaciones de recompilación de índice reanudables que se encuentran en estado de pausa.

```sql
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```

## <a name="see-also"></a>Vea también

- [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)
- [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)
- [Vistas de catálogo](catalog-views-transact-sql.md)
- [Vistas de catálogo de objetos](object-catalog-views-transact-sql.md)
- [sys.indexes](sys-xml-indexes-transact-sql.md)
- [sys.index_columns](sys-index-columns-transact-sql.md)
- [sys.xml_indexes](sys-xml-indexes-transact-sql.md)
- [sys.objects](sys-index-columns-transact-sql.md)
- [sys.key_constraints](sys-key-constraints-transact-sql.md)
- [sys.filegroups](sys-filegroups-transact-sql.md)
- [sys.partition_schemes](sys-partition-schemes-transact-sql.md)
- [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](querying-the-sql-server-system-catalog-faq.md)
