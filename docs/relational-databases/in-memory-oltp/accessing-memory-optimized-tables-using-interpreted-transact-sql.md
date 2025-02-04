---
title: Acceso a tablas con optimización para memoria mediante Transact-SQL interpretado | Microsoft Docs
ms.custom: ''
ms.date: 05/31/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 92a44d4d-0e53-4fb0-b890-de264c65c95a
author: MightyPen
ms.author: genemi
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dd722c59384b1a7878ac2b940da9534ba5d1f7a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951328"
---
# <a name="accessing-memory-optimized-tables-using-interpreted-transact-sql"></a>Acceso a tablas con optimización para memoria mediante Transact-SQL interpretado
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

 Con unas pocas excepciones, puede tener acceso a las tablas optimizadas para memoria mediante cualquier consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] u operación DML (select, insert, update o delete), lotes ad hoc y los módulos de SQL como procedimientos almacenados, funciones con valores de tabla, desencadenadores y vistas.  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado hace referencia a procedimientos almacenados o lotes de [!INCLUDE[tsql](../../includes/tsql-md.md)] distintos de un procedimiento almacenado compilado de forma nativa. El acceso de [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado a las tablas optimizadas para memoria se conoce como acceso de interoperabilidad.  

A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], las consultas en [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado puede examinar tablas optimizadas para memoria en paralelo, en lugar de solamente en modo de serie.

También se puede tener acceso a las tablas con optimización para memoria mediante un procedimiento almacenado compilado de forma nativa. Los procedimientos almacenados compilados de forma nativa se recomiendan para las operaciones OLTP donde el rendimiento es un factor crítico.  
  
El acceso interpretado de [!INCLUDE[tsql](../../includes/tsql-md.md)] se recomienda en estos casos:  
  
- Consultas ad hoc y tareas administrativas.  
  
- Consultas de notificación, que suelen usar construcciones no disponibles en los procedimientos almacenados compilados de forma nativa (como funciones de *ventana* , a las que a veces se hace referencia como funciones [OVER](../../t-sql/queries/select-over-clause-transact-sql.md) ).  
  
- Para migrar componentes esenciales para el rendimiento de su aplicación a tablas optimizadas para memoria, con cambios mínimos en el código de la aplicación (o sin ningún cambio). Puede ver mejoras en el rendimiento si se migran las tablas. Si después migra los procedimientos almacenados a procedimientos almacenados compilados de forma nativa, puede ver una mejora adicional del rendimiento.  
  
- Cuando no hay disponible una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] para los procedimientos almacenados compilados de forma nativa.  
  
Sin embargo, las construcciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes no se admiten en procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado que tienen acceso a datos de una tabla optimizada para memoria.  
  
|Área|No compatible|  
|----------|-----------------|  
|Acceso a tablas|TRUNCATE TABLE<br /><br /> MERGE (tabla optimizada para memoria como destino).<br /><br /> Cursores dinámicos y keyset (se degradan automáticamente en cursores estáticos).<br /><br /> Acceso de los módulos CLR, con la conexión de contexto.<br /><br /> Hacen referencia a una tabla optimizada para memoria desde una vista indizada.|  
|A través de bases de datos|Consultas entre bases de datos<br /><br /> Transacciones a través de bases de datos<br /><br /> Servidores vinculados|  
  
## <a name="table-hints"></a>Sugerencias de tabla

Para obtener más información acerca de las sugerencias de tabla, vea: [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md). SNAPSHOT se agregó para admitir [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
Las siguientes sugerencias de tabla no se admiten cuando se obtiene acceso a una tabla optimizada para memoria mediante [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado.  

  
|||||  
|-|-|-|-|  
|HOLDLOCK|IGNORE_CONSTRAINTS|IGNORE_TRIGGERS|NOWAIT|  
|PAGLOCK|READCOMMITTED|READCOMMITTEDLOCK|READPAST|  
|READUNCOMMITTED|ROWLOCK|SPATIAL_WINDOW_MAX_CELLS = *entero*|TABLOCK|  
|TABLOCKXX|UPDLOCK|XLOCK||  
  

Al tener acceso a una tabla optimizada para memoria desde una transacción explícita o implícita con [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado, debe hacer al menos una de las siguientes acciones:  
  
- Especificar una [sugerencia de tabla de nivel de aislamiento](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md) como SNAPSHOT, REPEATABLEREAD o SERIALIZABLE.  
  
- Establecer la opción de base de datos [MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT](../../t-sql/statements/alter-database-transact-sql-set-options.md) en ON.  
  
No es necesaria una sugerencia de tabla de nivel de aislamiento para las tablas optimizadas para memoria a las que acceden las consultas que se ejecutan en [modo de confirmación automática](https://msdn.microsoft.com/c8de5b60-d147-492d-b601-2eeae8511d00).  
  
## <a name="see-also"></a>Consulte también

[Compatibilidad de Transact-SQL con OLTP en memoria](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   

[Migrar a OLTP en memoria](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  

