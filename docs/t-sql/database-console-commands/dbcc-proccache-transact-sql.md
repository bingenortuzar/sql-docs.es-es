---
title: DBCC PROCCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC PROCCACHE
- DBCC_PROCCACHE_TSQL
- PROCCACHE_TSQL
- PROCCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- procedure cache [SQL Server]
- displaying procedure cache information
- DBCC PROCCACHE statement
ms.assetid: 7a4f9f8a-13ff-4bf2-ba29-c17012a23659
author: pmasl
ms.author: umajay
ms.openlocfilehash: 7720324915ea147cf5cac938c196957a6cb04c51
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116455"
---
# <a name="dbcc-proccache-transact-sql"></a>DBCC PROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Muestra información acerca de la caché de procedimientos en forma de tabla.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC PROCCACHE [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 por  
 Permite que se especifiquen opciones.  
  
 NO_INFOMSGS  
 Suprime todos los mensajes informativos que tienen niveles de gravedad entre 0 y 10.  
  
## <a name="remarks"></a>Notas  
La caché de procedimientos se utiliza para almacenar en caché los planes compilados y ejecutables con el fin de acelerar la ejecución de lotes. Las entradas de una caché de procedimientos están en el nivel de lote. La caché de procedimientos incluye las siguientes entradas:
-   Planes compilados  
-   Planes de ejecución  
-   Árbol algebraico  
-   Procedimientos extendidos  
  
## <a name="result-sets"></a>Conjuntos de resultados  
En la tabla siguiente se describen las columnas del conjunto de resultados.
  
|Nombre de columna|Descripción|  
|-----------------|-----------------|  
|**num proc buffs**|Número total de páginas utilizadas por todas las entradas de la caché de procedimientos.|  
|**num proc buffs used**|Número total de páginas utilizadas por todas las entradas que se están utilizando actualmente.|  
|**num proc buffs active**|Se conserva únicamente por compatibilidad con versiones anteriores. Número total de páginas utilizadas por todas las entradas que se están utilizando actualmente.|  
|**proc cache size**|Número total de entradas de la caché de procedimientos.|  
|**proc cache used**|Número total de entradas que se están utilizando actualmente.|  
|**proc cache active**|Se conserva únicamente por compatibilidad con versiones anteriores. Número total de entradas que se están utilizando actualmente.|  
  
## <a name="permissions"></a>Permisos  
Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner** .
  
## <a name="see-also"></a>Consulte también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
