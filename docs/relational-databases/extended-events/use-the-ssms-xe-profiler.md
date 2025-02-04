---
title: Uso de XEvent Profiler de SSMS | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: yualan
ms.author: alayu
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 512a32fbbc57b960369b052615973b999f378a90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68009383"
---
# <a name="use-the-ssms-xevent-profiler"></a>Uso de XEvent Profiler de SSMS

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
XEvent Profiler es una característica de SQL Server Management Studio (SSMS) que muestra una ventana con los eventos extendidos para visualizarlos de forma dinámica. En la información general puede consultar los motivos por los que el generador de perfiles resulta tan útil, las características principales y las instrucciones para visualizar los eventos extendidos.

## <a name="why-would-i-use-the-xevent-profiler"></a>¿Por qué XEvent Profiler es tan útil?
A diferencia de SQL Profiler, XEvent Profiler está directamente integrado en SSMS y compilado con la tecnología de eventos extendidos escalables en el motor de SQL. Esta característica permite acceder rápidamente a una visualización de streaming en vivo de los eventos de diagnóstico en el servidor SQL. Dicha visualización se puede personalizar. Además, las personalizaciones que haga se pueden compartir con otros usuarios de SSMS como archivo .viewsettings. La sesión que crea XE Profiler es menos invasiva para el servidor SQL en ejecución que otro seguimiento SQL similar, en el caso de usar SQL Profiler. El usuario también puede personalizar esta sesión con la IU de propiedades de sesión de XE existentes o mediante TSQL.

## <a name="prerequisites"></a>Prerequisites
Esta característica solo está disponible para la versión 17.3 de SQL Server Management Studio (SSMS) u otras posteriores. Asegúrese de utilizar la última versión, que podrá encontrar [aquí](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a id="getting-started"></a>Introducción
Para acceder a XEvent Profiler, siga estos pasos:

1. Abra **SQL Server Management Studio**.

2. Conéctese a una instancia de Motor de base de datos de SQL Server o el localhost.

3. En el Explorador de objetos, encontrará el elemento de menú correspondiente a XE Profiler. Para expandirlo, haga clic en el signo "+".

   ![Menú de XE Profiler](media/xevents-xe-profiler-menu.png)

4. Si quiere ver todos los eventos extendidos de esta sesión, haga doble clic en **Estándar**. Si quiere ver las instrucciones SQL registradas, haga clic en **T-SQL**. En caso de que todavía no haya ninguna sesión creada, se creará una para usted.

   ![Sesión de XE Profiler](media/xevents-xe-profiler-start-session.png)

5. Ahora puede ver los eventos extendidos.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

   ![Visor de XE Profiler](media/xevents-xe-profiler-start-viewer.png)

## <a name="see-also"></a>Consulte también
[Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
[Herramientas de eventos extendidos](../../relational-databases/extended-events/extended-events-tools.md)  
  
  
