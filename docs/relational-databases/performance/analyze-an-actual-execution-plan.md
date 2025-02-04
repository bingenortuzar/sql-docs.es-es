---
title: Análisis de un plan de ejecución real | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- analyzing execution plans
- analyzing actual execution plans
- execution plans [SQL Server], analyzing
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: e0f23ceb75856db921e4c6303a8013d351f364e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68219593"
---
# <a name="analyze-an-actual-execution-plan"></a>Análisis de un plan de ejecución real
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En este tema se describe cómo analizar planes de ejecución gráficos reales mediante la función Plan Analysis (Análisis de plan) de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

> [!NOTE]
> Los planes de ejecución reales se generan tras ejecutar las consultas o los lotes del [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por este motivo, un plan de ejecución real contiene información de tiempo de ejecución, como el número de filas real, las métricas de uso real de recursos o las advertencias en tiempo de ejecución (si las hubiera). Para obtener más información, vea [Mostrar un plan de ejecución real](../../relational-databases/performance/display-an-actual-execution-plan.md).
  
Para poder solucionar problemas de rendimiento de consulta, es necesario tener un buen conocimiento de los planes de ejecución y procesamiento de consultas, a fin de poder localizar y corregir las causas raíz.

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] incluye una funcionalidad que implementa cierto grado de automatización de la tarea de análisis de plan de ejecución real, especialmente para planes grandes y complejos. El objetivo es que sea más fácil encontrar los escenarios de [Cardinality Estimation](../../relational-databases/performance/cardinality-estimation-sql-server.md) (Estimación de cardinalidad) inexactos y obtener recomendaciones sobre las posibles mitigaciones disponibles.

> [!IMPORTANT]
> Asegúrese de que se realizan pruebas adecuadas de las mitigaciones propuestas antes de aplicarlas en entornos de producción.
  
## <a name="to-analyze-an-execution-plan-for-a-query"></a>Para analizar un plan de ejecución para una consulta  
  
1.  Abra un archivo de plan de ejecución de consulta guardado previamente (.sqlplan) desde el menú **Archivo** y haga clic en **Abrir archivo**, o arrastre un archivo de plan a la ventana [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]. De forma alternativa, si acaba de ejecutar una consulta y elige mostrar su plan de ejecución, vaya a la pestaña **Plan de ejecución** en el panel de resultados. 

2.  Haga clic en un área en blanco del plan de ejecución y haga clic en **Analizar el plan de ejecución real**. 

    ![Hacer clic con el botón derecho en Analizar el plan de ejecución real](../../relational-databases/performance/media/plananalysismenuoption.png "Right-click Analyze Actual Execution Plan")   

3.  Se abre la ventana **Análisis del plan de presentación** en la parte inferior. La pestaña **Instrucción múltiple** es útil para analizar los planes con varias instrucciones, permitiendo que se analice la instrucción correcta.

4.  Seleccione la pestaña Escenarios para ver detalles sobre los problemas encontrados en el plan de ejecución real. Para cada operador enumerado en el panel izquierdo, el panel derecho muestra detalles sobre el escenario en el vínculo *Para más información sobre este escenario, haga clic aquí* y se muestran los motivos posibles para explicar ese escenario.

    ![Resultados del análisis del plan de ejecución](../../relational-databases/performance/media/plananalysis-scenarios.png "Execution Plan Analysis results") 
