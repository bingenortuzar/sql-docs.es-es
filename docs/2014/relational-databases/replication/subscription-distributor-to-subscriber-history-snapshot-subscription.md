---
title: Suscripción, Historial de Distribuidor a suscriptor (suscripción de instantánea) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.pubtodist.snapshot.f1
ms.assetid: d3575964-f287-4bcf-8d2e-f81a33141b25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e0520c28d78b8036072b70de2d8f83a1a8c72da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628780"
---
# <a name="subscription-distributor-to-subscriber-history-snapshot-subscription"></a>Suscripción, Historial de Distribuidor a suscriptor (suscripción de instantánea)
  La pestaña **Historial de Distribuidor a suscriptor** muestra información detallada sobre el Agente de distribución, incluidos el estado, el historial, los mensajes informativos y cualquier mensaje de error.  
  
## <a name="options"></a>Opciones  
 Seleccione las sesiones del Agente de distribución que desee ver en el menú **Ver** y, a continuación, seleccione una sesión concreta en la cuadrícula etiquetada como **Sesiones del Agente de distribución**. En la cuadrícula con la etiqueta **Acciones en la sesión seleccionada**se muestra información detallada de la sesión. Si la sesión seleccionada finalizó con un error, también se muestra el área de texto con la etiqueta **Detalles del error o mensaje de la sesión seleccionada** .  
  
 **Vista**  
 Seleccione las sesiones del Agente de distribución que desee ver.  
  
 **Estado**  
 Estado del Agente de distribución. En la lista siguiente se muestran los valores de estado posibles:  
  
-   Error  
  
-   Completada  
  
-   Intentando de nuevo  
  
-   En ejecución  
  
 **Start Time**  
 Muestra la hora de inicio de la sesión.  
  
 **Hora de finalización**  
 Muestra la hora de finalización de la sesión. Si no se ha detenido el agente, el campo se mostrará vacío.  
  
 **Duración**  
 Cantidad de tiempo que se ha ejecutado el Agente de distribución en esta sesión. El tiempo representa el tiempo transcurrido si el agente se encuentra en ejecución, y el tiempo total de la sesión si la sesión del agente ha finalizado.  
  
 **Mensaje de error**  
 Si una sesión terminó en error, este campo muestra el último mensaje de error registrado por el Agente de distribución. Si la sesión no ha finalizado con error, el campo se mostrará vacío.  
  
 **Mensaje de la acción**  
 Todos los mensajes informativos y de error que el Agente de distribución ha registrado durante la sesión seleccionada.  
  
 **Hora de la acción**  
 Muestra la hora de realización de la acción descrita en la columna **Mensaje de la acción** .  
  
 **Detalles del error o mensaje de la sesión seleccionada**  
 Solo se muestra si la sesión seleccionada presenta un valor de **Error** en la columna **Estado** . El área de texto muestra la información detallada del error y el comando que se intentaba ejecutar en el momento de producirse el error. También incluye vínculos a la información adicional relativa al error.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de replicación](monitor/start-the-replication-monitor.md)   
 [Visualización de información y realización de tareas mediante el Monitor de replicación](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitoring Replication](monitoring-replication.md)  (Supervisar la replicación)  
 [Información general sobre los agentes de replicación](agents/replication-agents-overview.md)  
  
  
