---
title: Programar seguimientos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], events
- traces [SQL Server]
- traces [SQL Server], stopping
- events [SQL Server], filters
- scheduling traces [SQL Server]
- traces [SQL Server], scheduling
- stopping traces
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 12061040ea7fa1b34d892230fbba73f4c34a1949
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140691"
---
# <a name="schedule-traces"></a>Programar seguimientos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hay dos formas de programar trazas. Puede hacer lo siguiente:  
  
-   Habilitar una hora de detención de seguimiento.  
  
-   Utilizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programar una seguimiento.  
  
## <a name="specifying-a-stop-time"></a>Especificar una hora de detención  
 Puede especificar una hora de detención de seguimiento si utiliza procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] o si utiliza el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. La hora de detención debe establecerse al configurar originalmente la seguimiento.  
  
## <a name="scheduling-traces-by-using-sql-server-agent"></a>Programar seguimientos mediante el Agente SQL Server  
 La mejor forma de programar seguimientos consiste en usar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para iniciar el seguimiento y, después, especificar una hora de detención de seguimiento mediante el procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_trace_setstatus**o el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 **Para establecer un filtro de hora de finalización para una seguimiento**  
  
 [Filtrar eventos basándose en la hora de finalización del evento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
 [Tareas administrativas automatizadas &#40;Agente SQL Server&#41;](https://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)  
  
  
