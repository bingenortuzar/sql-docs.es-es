---
title: Actualización de datos en el Monitor de replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- refreshing data
ms.assetid: e9582244-7d00-45f4-be16-020a65c76a5e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 03dae95f44b4166947da4ef7bd88b532db00dd03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667241"
---
# <a name="refresh-data-in-replication-monitor"></a>Actualizar datos en el Monitor de replicación
  En el Monitor de replicación, la ventana principal y las ventanas de detalles (las ventanas que se inician desde la ventana principal) se pueden actualizar automática o manualmente. Para actualizar una ventana manualmente, presione F5. De manera predeterminada, la ventana principal se actualiza automáticamente cada cinco segundos; este valor se puede personalizar para cada publicador.  
  
 Los datos que se muestran en el Monitor de replicación se consultan desde una caché; para obtener información sobre la relación entre la caché y la actualización del Monitor de replicación, vea [Almacenamiento en caché, actualización y rendimiento del Monitor de replicación](caching-refresh-and-replication-monitor-performance.md). Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](start-the-replication-monitor.md).  
  
### <a name="to-set-refresh-options-for-replication-monitor"></a>Para establecer las opciones de actualización del Monitor de replicación  
  
1.  Haga clic con el botón secundario en el panel izquierdo del Monitor de replicación y, a continuación, haga clic en **Configuración del publicador**.  
  
2.  En el cuadro de diálogo **Configuración del publicador** , establezca las opciones **Actualizar automáticamente** y **Frecuencia de actualización** . El valor establecido en **Actualizar automáticamente** afecta a la ventana principal del Monitor de replicación. El valor establecido en **Frecuencia de actualización** también afecta a las ventanas de detalles cuya configuración se haya establecido de modo que se actualicen automáticamente (los cambios en la configuración solo afectan a las ventanas de detalles abiertas después del cambio).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-specify-that-a-detail-window-should-automatically-refresh"></a>Para especificar que una ventana de detalles se actualice automáticamente  
  
1.  Abra una ventana de detalles en el Monitor de replicación. Por ejemplo:  
  
    1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
    2.  Haga clic en la pestaña **Todas las suscripciones** .  
  
    3.  Haga clic con el botón secundario en una suscripción y, a continuación, haga clic en **Ver detalles**.  
  
2.  En la ventana de detalles **Suscripción \<<nombreDeSuscripción>** , haga clic en **Acción** y, a continuación, en **Actualizar automáticamente**. La frecuencia de actualización es establece con el valor que se especifique en **Frecuencia de actualización** en el cuadro de diálogo **Configuración del publicador** .  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación](../monitoring-replication.md)  
  
  
