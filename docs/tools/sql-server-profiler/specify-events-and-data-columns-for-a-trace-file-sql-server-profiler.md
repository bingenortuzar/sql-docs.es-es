---
title: Especificar eventos y columnas de datos para un archivo de seguimiento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- adding events
- traces [SQL Server], data columns
- deleting events
- removing events
- traces [SQL Server], events
ms.assetid: 7da715a3-2f03-4063-b6a4-20fd7b44e675
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4ed34a9e051435e7f6e990b445cf0ffd88383f09
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059692"
---
# <a name="specify-events-and-data-columns-for-a-trace-file-sql-server-profiler"></a>Especificar eventos y columnas de datos para un archivo de seguimiento (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe el modo de especificar clases de eventos y columnas de datos para seguimientos mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-specify-events-and-data-columns-for-a-trace"></a>Para especificar eventos y columnas de datos para un seguimiento  
  
1.  En el cuadro de diálogo **Propiedades de seguimiento** o **Propiedades de la plantilla de seguimiento** , haga clic en la pestaña **Selección de eventos** .  
  
     La pestaña **Selección de eventos** contiene un control de cuadrícula. El control de cuadrícula es una tabla que contiene todas las clases de eventos en las que se puede realizar un seguimiento. La tabla contiene una fila para cada clase de evento. Las clases de eventos pueden diferir ligeramente dependiendo del tipo y la versión del servidor al que esté conectado. Las clases de eventos se identifican en la columna **Eventos**de la cuadrícula y se agrupan por categorías de eventos. En las demás columnas se enumeran las columnas de datos que pueden devolverse para cada clase de evento.  
  
2.  En el cuadro de diálogo **Selección de eventos**, use el control de cuadrícula para agregar o eliminar eventos y columnas de datos del archivo de seguimiento.  
  
3.  Para eliminar eventos del seguimiento, desactive casilla en la columna **Eventos** para cada clase de evento.  
  
4.  Para incluir eventos en un seguimiento, active la casilla en la columna **Eventos** para cada clase de evento, o bien seleccione una columna de datos que corresponda a un evento.  
  
> [!IMPORTANT]  
>  Si el seguimiento se va a correlacionar con los datos del Monitor de sistema o del Monitor de rendimiento, es necesario incluir en el seguimiento las columnas de datos **Hora de inicio** y **Hora de finalización** .  
  
 Si incluye una clase de evento, todas las columnas de datos asociadas también se incluyen en el seguimiento si ha activado la casilla correspondiente a un evento. Si ha activado la casilla de una determinada columna, solo se incluye esa columna en el seguimiento.  
  
1.  Para quitar columnas de datos de una clase de eventos, desactive las casillas de la columna de datos en la fila de la clase de eventos o haga clic con el botón derecho en el encabezado de columna y seleccione la opción **Anular la selección de la columna** .  
  
2.  Opcionalmente, aplique filtros al seguimiento. Para obtener más información, vea [Filtrar eventos en un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
