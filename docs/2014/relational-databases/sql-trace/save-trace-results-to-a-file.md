---
title: Guardar los resultados de un seguimiento en un archivo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 74f80667-62f3-4e14-bb1a-f0c2b6ef3402
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a55662b38fbd69dc45d8f0031856ad4da5929038
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63136453"
---
# <a name="save-trace-results-to-a-file"></a>Guardar los resultados de un seguimiento en un archivo
  Los resultados de un seguimiento se pueden guardar en un archivo. Un archivo de seguimiento es un archivo donde se escriben los resultados de un seguimiento. Un archivo de seguimiento puede ubicarse en un directorio local (por ejemplo C:\\*nombreDeCarpeta*\\*nombreDeArchivo.trc*) o un directorio de red (por ejemplo \\\nombreDeEquipo\nombreDeRecursoCompartido\nombreDeArchivo.trc).  
  
 Puede utilizar los archivos de seguimiento para realizar lo siguiente:  
  
-   Reproducir seguimientos  
  
-   Auditar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Realizar análisis de rendimiento  
  
-   Correlacionar eventos de seguimiento con contadores de rendimiento para mejorar la detección de problemas  
  
-   Realizar análisis del Asistente para la optimización de motor de bases de datos  
  
-   Optimizar las consultas  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] guarda los resultados de seguimiento en un archivo cuando se ha especificado una ruta de acceso y un nombre de archivo para el argumento **@tracefile** del procedimiento almacenado **sp_trace_create**.  
  
> [!NOTE]  
>  Si hay especificada una ruta de acceso al procedimiento almacenado **sp_trace_create** para guardar el archivo de seguimiento, el directorio debe ser accesible para el servidor. También debe tener presente que si un directorio local está especificado con **sp_trace_create**, se trata de un directorio local en el equipo servidor.  
  
 Si se utiliza [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , ello le permite guardar los resultados de un seguimiento en un archivo o una tabla. Si guarda los resultados de un seguimiento en una tabla, tendrá el mismo acceso que si guarda el seguimiento en un archivo, además de poder realizar consultas en la tabla para buscar eventos específicos.  
  
 Para obtener más información sobre cómo guardar los resultados de seguimiento, vea [Guardar los resultados de un seguimiento en una tabla &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-table-sql-server-profiler.md) y [Guardar los resultados de seguimiento en un archivo &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/save-trace-results-to-a-file-sql-server-profiler.md).  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)   
 [Crear un seguimiento &#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)   
 [Crear un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
  
