---
title: Reproducir un script Transact-SQL (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- scripts [SQL Server], traces
- replaying traces
ms.assetid: 9c0eb222-e6e3-4bc1-a25f-a41e962d361b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 62ca5b9038a8c5cfd7590ed2754691266a691c5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906082"
---
# <a name="replay-a-transact-sql-script-sql-server-profiler"></a>Reproducir un script Transact-SQL (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Cuando pruebe posibles soluciones para un problema de rendimiento, utilice el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para reproducir scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] y compare el rendimiento antes y después de los cambios.  
  
### <a name="to-replay-a-transact-sql-script"></a>Para reproducir un script Transact-SQL  
  
1.  En el menú **Archivo** , seleccione **Abrir**y haga clic en **Archivo de script**.  
  
2.  Seleccione el archivo de script [!INCLUDE[tsql](../../includes/tsql-md.md)] que desee abrir. Asegúrese de que el script [!INCLUDE[tsql](../../includes/tsql-md.md)] contiene los eventos necesarios para la reproducción. Para más información, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
3.  En el menú **Reproducir** , haga clic en **Iniciar**y conéctese al servidor en el que desee reproducir el script.  
  
4.  Compruebe la configuración en el cuadro de diálogo **Configuración de reproducción** y haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Consulte también  
 [Reproducir seguimientos](../../tools/sql-server-profiler/replay-traces.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
