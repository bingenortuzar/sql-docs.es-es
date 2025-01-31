---
title: Solucionar problemas de informes para la ejecución de paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8fc476ac-bd69-434e-9636-70776e0b3b6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1c1a59d9e77806666c487b0778edd574bcaa5e42
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62926321"
---
# <a name="troubleshooting-reports-for-package-execution"></a>Solucionar problemas de informes para la ejecución de paquetes
  En la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], existen informes estándar en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ayudarlo a supervisar y solucionar problemas relacionados con los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que se han implementado en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . En concreto, dos de estos informes le ayudarán a ver el estado de ejecución de los paquetes e identificar la causa de los errores de ejecución.  
  
-   **Panel de Integration Services** : este informe proporciona información general sobre todas las ejecuciones de paquetes de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en las últimas 24 horas. El informe muestra información sobre el estado, tipo de operación, nombre del paquete, etc., para cada paquete.  
  
     La Hora de inicio, la Hora de finalización y la Duración se pueden interpretar de la manera siguiente:  
  
    -   Si el paquete se sigue ejecutando: Duración = hora actual - Hora de inicio  
  
    -   Si el paquete se ha completado: Duración = Hora de finalización - Hora de inicio  
  
     Para cada paquete que se ha ejecutado en el servidor, el panel le permite 'acercar' para buscar detalles específicos sobre los errores que podrían haberse producido durante la ejecución del paquete. Por ejemplo, haga clic en **Información general** para mostrar información general de alto nivel sobre el estado de las tareas durante la ejecución o haga clic en **Todos los mensajes** para mostrar los mensajes detallados que se capturaron como parte de la ejecución del paquete.  
  
     Puede filtrar la tabla que se muestra en cualquier página si hace clic en **Filtro** y selecciona los criterios deseados en el cuadro de diálogo **Configuración de filtro** . Los criterios de filtro disponibles dependen de los datos que se muestran. Puede cambiar el criterio de ordenación del informe haciendo clic en el icono de ordenación del cuadro de diálogo **Configuración de filtro** .  
  
-   **Informe “Actividad: todas las ejecuciones”** : en este informe, se muestra un resumen de todas las ejecuciones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] realizadas en el servidor. El resumen muestra información para cada ejecución, como el estado, la hora de inicio y la hora de finalización. Cada entrada de resumen incluye vínculos a más información acerca de la ejecución, incluidos los mensajes generados durante la ejecución y los datos de rendimiento. Al igual que con el Panel de Integration Services, puede aplicar un filtro a la tabla para reducir la información mostrada.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Ver informes del servidor de Integration Services](../view-reports-for-the-integration-services-server.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [Informes para el servidor de Integration Services](../reports-for-the-integration-services-server.md)  
  
 [Herramientas para solucionar problemas con la ejecución de paquetes](troubleshooting-tools-for-package-execution.md)  
  
  
