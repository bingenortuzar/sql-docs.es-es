---
title: trace_xe_event_map (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- trace_xe_event_map_TSQL
- trace_xe_event_map
dev_langs:
- TSQL
helpviewer_keywords:
- trace_xe_event_map
- extended events [SQL Server], tables
ms.assetid: 537aa292-3540-47e8-be28-56dc01abc343
author: stevestein
ms.author: sstein
ms.openlocfilehash: 07810bcd1f43bd3fd2428361e5f429edb9c7c3d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056241"
---
# <a name="extended-events-tables---tracexeeventmap"></a>Tablas de eventos extendidos: trace_xe_event_map
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para cada evento de eventos extendidos que está asignado a una clase de eventos de Seguimiento de SQL. Esta tabla se almacena en la base de datos maestra en el esquema sys.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|trace_event_id|**smallint**|Identificador de la clase de eventos de Seguimiento de SQL que está asignando.|  
|package_name|**nvarchar(60)**|El nombre del paquete de eventos extendidos donde reside el evento asignado.|  
|xe_event_name|**nvarchar(60)**|El nombre del evento de eventos extendidos que está asignado a la clase de eventos de Seguimiento de SQL.|  
  
## <a name="remarks"></a>Comentarios  
 Puede utilizar la siguiente consulta para identificar las acciones de eventos de eventos extendidos que son equivalentes a las clases de eventos de Seguimiento de SQL:  
  
```  
SELECT te.name, xe.package_name, xe.xe_event_name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NOT NULL  
```  
  
 No todas las clases de eventos tienen eventos de eventos extendidos equivalentes. Puede utilizar la siguiente consulta para enumerar las clases de eventos que no tienen un equivalente de eventos extendidos:  
  
```  
SELECT te.trace_event_id, te.name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NULL  
```  
  
 En la consulta anterior, la mayoría de las clases de eventos devueltas están relacionadas con la auditoría. Recomendamos que use la Auditoría de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para auditar. Auditoría de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa eventos extendidos para facilitar la creación de auditorías. Para obtener más información, vea [SQL Server Audit &#40;motor de base de datos&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
## <a name="see-also"></a>Vea también  
 [trace_xe_action_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-action-map.md)  
  
  
