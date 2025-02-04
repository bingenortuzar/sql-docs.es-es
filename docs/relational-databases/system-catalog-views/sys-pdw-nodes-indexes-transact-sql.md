---
title: sys.pdw_nodes_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 261bcb7f-a906-4979-b274-bc5f1aa66426
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: bb20ecd4fe212f4004061a6c39ad33c3ffc8ac8e
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68809929"
---
# <a name="syspdw_nodes_indexes-transact-sql"></a>sys.pdw_nodes_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Devuelve índices para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|identificador del objeto al que pertenece este índice.||  
|name|**sysname**|Nombre del índice. Name es único solo dentro del objeto. NULL = Montón||  
|index_id|**int**|identificador del índice. el número de la secuencia es único en el objeto.<br /><br /> 0 = Montón<br /><br /> 1 = Índice clúster<br /><br /> > 1 = índice no clúster||  
|type|**tinyint**|Tipo de índice:<br /><br /> 0 = Montón<br /><br /> 1 = Clúster<br /><br /> 2 = No clúster<br /><br /> 5 = índice de almacén de columnas optimizado para memoria xVelocity en clúster|  
|type_desc|**nvarchar(60)**|Descripción del tipo de índice:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> ALMACÉN DE COLUMNAS AGRUPADO||  
|is_unique|**bit**|0 = El índice no es exclusivo.|Siempre es 0.|  
|data_space_id|**int**|identificador del espacio de datos para este índice. El espacio de datos es un grupo de archivos o un esquema de partición.<br /><br /> 0 = object_id es una función con valores de tabla.||  
|ignore_dup_key|**bit**|0 = IGNORE_DUP_KEY está OFF.|Siempre es 0.|  
|is_primary_key|**bit**|1 = El índice forma parte de una restricción PRIMARY KEY.|Siempre es 0.|  
|is_unique_constraint|**bit**|1 = El índice forma parte de una restricción UNIQUE.|Siempre es 0.|  
|fill_factor|**tinyint**|> 0 = porcentaje de FILLFACTOR utilizado al crear o volver a generar el índice.<br /><br /> 0 = Valor predeterminado|Siempre es 0.|  
|is_padded|**bit**|0 = PADINDEX está OFF.|Siempre es 0.|  
|is_disabled|**bit**|1 = El índice está deshabilitado.<br /><br /> 0 = El índice no está deshabilitado.||  
|is_hypothetical|**bit**|0 = El índice no es hipotético.|Siempre es 0.|  
|allow_row_locks|**bit**|1 = El índice admite bloqueos de fila.|Siempre es 1.|  
|allow_page_locks|**bit**|1 = El índice admite bloqueos de página.|Siempre es 1.|  
|has_filter|**bit**|0 = El índice no tiene un filtro.|Siempre es 0.|  
|filter_definition|**nvarchar(max)**|Expresión para el subconjunto de filas incluido en el índice filtrado.|Siempre es NULL.|  
|pdw_node_id|**int**|Identificador único de un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nodo.|NOT NULL|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="see-also"></a>Vea también  
 [SQL Data Warehouse y vistas de catálogo de almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
