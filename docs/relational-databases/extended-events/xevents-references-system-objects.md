---
title: Objetos del sistema relacionados con XEvents | Microsoft Docs
ms.custom: ''
ms.date: 03/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jukoesma
ms.technology: xevents
ms.topic: reference
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a8be742db65127eaeac24c54fbcf9386d49453c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903393"
---
# <a name="system-objects-that-support-extended-events"></a>Objetos del sistema que admiten eventos extendidos

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

El presente artículo proporciona vínculos a otros artículos relacionados con eventos extendidos. En este tipo de artículos se tratan los siguientes aspectos:

- Objetos del sistema que proporcionan compatibilidad con la característica de eventos extendidos.
- Partes de SQL Server que usan eventos extendidos.
- Aspectos de eventos extendidos que son específicos de Azure SQL Database en la nube.

Las listas no están necesariamente completas.

## <a name="system-tables"></a>Tablas del sistema

- [Tablas de eventos extendidos: trace_xe_action_map](../system-tables/extended-events-tables-trace-xe-action-map.md)

- [Tablas de eventos extendidos: trace_xe_event_map](../system-tables/extended-events-tables-trace-xe-event-map.md)

## <a name="system-catalog-views"></a>Vistas de catálogo del sistema

- [Vistas de catálogo de eventos extendidos (Transact-SQL)](../system-catalog-views/extended-events-catalog-views-transact-sql.md)

- [sys.server_event_sessions (Transact-SQL)](../system-catalog-views/sys-server-event-sessions-transact-sql.md)

- [sys.server_event_session_actions (Transact-SQL)](../system-catalog-views/sys-server-event-session-actions-transact-sql.md)

- [sys.server_event_session_events (Transact-SQL)](../system-catalog-views/sys-server-event-session-events-transact-sql.md)

- [sys.server_event_session_fields (Transact-SQL)](../system-catalog-views/sys-server-event-session-fields-transact-sql.md)

- [sys.server_event_session_targets (Transact-SQL)](../system-catalog-views/sys-server-event-session-targets-transact-sql.md)

## <a name="other-system-objects"></a>Otros objetos del sistema

- [Vistas de administración dinámica de eventos extendidos](../system-dynamic-management-views/extended-events-dynamic-management-views.md)

## <a name="uses-of-extended-events-by-sql-server-itself"></a>Usos de eventos extendidos mediante el propio SQL Server

Esta lista no pretende ser completa.

- [Obtener acceso a información de diagnóstico en el registro de eventos extendidos](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)

- [Configuración de eventos extendidos para grupos de disponibilidad Always On](../../database-engine/availability-groups/windows/always-on-extended-events.md)

- [Eventos extendidos de Stretch Database](../../sql-server/stretch-database/extended-events-for-stretch-database.md)

## <a name="azure-sql-database-and-extended-events"></a>Azure SQL Database y eventos extendidos

- [Eventos extendidos en Azure SQL Database](/azure/sql-database/sql-database-xevent-db-diff-from-svr)

- [sys.database_event_session_targets (Azure SQL Database)](../system-catalog-views/sys-database-event-session-targets-azure-sql-database.md)

- [sys.database_event_session_fields (Azure SQL Database)](../system-catalog-views/sys-database-event-session-fields-azure-sql-database.md)

- [sys.database_event_session_events (Azure SQL Database)](../system-catalog-views/sys-database-event-session-events-azure-sql-database.md)

- [sys.database_event_session_actions (Azure SQL Database)](../system-catalog-views/sys-database-event-session-actions-azure-sql-database.md)
