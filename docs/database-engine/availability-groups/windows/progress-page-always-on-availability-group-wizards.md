---
title: Página Progreso (asistentes para grupos de disponibilidad AlwaysOn)
description: Una descripción de las opciones que se encuentran en la página "Progreso" del "Asistente para grupo de disponibilidad de Always On" dentro de SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.failoverwizard.progress.f1
- sql13.swb.adddatabasewizard.progress.f1
- sql13.swb.addreplicawizard.progress.f1
- sql13.swb.newagwizard.progress.f1
ms.assetid: bd3b0306-8384-4120-a1c9-03825f0ae26a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 87201ed5c3d2368f54e2ffb0c57391322066a30b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014477"
---
# <a name="progress-page-always-on-availability-group-wizards"></a>Página Progreso (asistentes para grupos de disponibilidad AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Utilice este cuadro de diálogo para ver el progreso del asistente de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] que esté ejecutando en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. La barra de progreso indica el progreso relativo de los pasos que el asistente realiza.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Más detalles**  
 Haga clic en la flecha abajo para mostrar una cuadrícula de progreso que enumera los pasos completados, en orden, seguida de la operación en curso actual. La cuadrícula contiene las columnas siguientes:  
  
 **Nombre**  
 Muestra una frase que describe un paso concreto.  
  
 **Estado**  
 Indica el resultado de los pasos completados y el porcentaje de finalización del paso actual, del siguiente modo:  
  
|Resultado|Descripción|  
|------------|-----------------|  
|**Error**|Indica que la operación para este paso ha experimentado un error. Haga clic en el vínculo para mostrar un cuadro de diálogo de mensaje que describe el error.|  
|**En curso (** *porcentaje completado* **)**|Indica que la operación se está produciendo ahora y calcula el porcentaje completado de este paso.|  
|**Correcto**|Indica que la operación correspondiente a este paso se ha completado correctamente.|  
  
 **Menos detalles**  
 Haga clic para ocultar la cuadrícula de progreso.  
  
 **Cancelar**  
 Haga clic para omitir las operaciones restantes y salir del asistente.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una réplica al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una base de datos al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
-   [Usar el Asistente para grupo de disponibilidad de conmutación por error &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
