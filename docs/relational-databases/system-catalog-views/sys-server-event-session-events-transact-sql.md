---
title: Sys.server_event_session_events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_events
- server_event_session_events_TSQL
- sys.server_event_session_events
- sys.server_event_session_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_events catalog view
- xe
ms.assetid: 75986e91-1fc7-4f14-98ac-4e90154a74db
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9ac3c2bd13b5f89ea8d87336e579e196e3754c5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133230"
---
# <a name="sysservereventsessionevents-transact-sql"></a>sys.server_event_session_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada evento de una sesión de eventos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|Identificador de la sesión de eventos. No admite valores NULL.|  
|event_id|**int**|Id. del evento. Este Id. es único dentro de un objeto de sesión de eventos. No admite valores NULL.|  
|NAME|**sysname**|Nombre del evento. No admite valores NULL.|  
|paquete|**sysname**|Nombre del paquete de eventos que contiene el evento. No admite valores NULL.|  
|módulo|**sysname**|Nombre del módulo que contiene el evento. No admite valores NULL.|  
|predicate|**nvarchar(3000)**|La expresión de predicado aplicada al evento. Acepta valores NULL.|  
|predicate_xml|**nvarchar(3000)**|La expresión de predicado XML aplicada al evento. Acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="remarks"></a>Comentarios  
 Esta vista tiene las siguientes cardinalidades de relación.  
  
||||  
|-|-|-|  
|De|En|Relación|  
|sys.server_event_session_events.event_session_id|Sys.server_event_sessions.event_session_id|Varios a uno|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de eventos extendidos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
