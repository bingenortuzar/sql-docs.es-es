---
title: Estados de creación de reflejo (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- states [SQL Server], database mirroring
- PENDING_FAILOVER state
- mirroring states [SQL Server]
- DISCONNECTED state
- SYNCHRONIZING state
- SYNCHRONIZED state
- SUSPENDED state
- database mirroring [SQL Server], states
ms.assetid: 90062917-74f9-471b-b49e-bc153ae1a468
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9e3e3756f65baa7e1b62e3a84ff709a60b9c887b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754552"
---
# <a name="mirroring-states-sql-server"></a>Estados de creacion de reflejo (SQL Server)
  Durante una sesión de creación de reflejo de la base de datos, la base de datos reflejada siempre se encuentra en un estado específico (el *estado de creación de reflejo*). El estado de la base de datos refleja el estado de la comunicación, el flujo de datos y la diferencia de datos entre los asociados. La sesión de creación de reflejo de la base de datos adopta el mismo estado que la base de datos principal.  
  
 Durante una sesión de creación de reflejo de una base de datos, las instancias de servidor se supervisan entre sí. Los asociados usan el estado de creación de reflejo para supervisar la base de datos. A excepción del estado PENDING_FAILOVER, las bases de datos principal y reflejada siempre tienen el mismo estado. Si se establece un testigo para la sesión, cada uno de los asociados supervisa el testigo mediante su estado de conexión (CONNECTED o DISCONNECTED).  
  
 Los estados posibles de creación de reflejo de la base de datos son:  
  
|estado de creación de reflejo|Descripción|  
|---------------------|-----------------|  
|SYNCHRONIZING|El contenido de la base de datos reflejada está atrasado con respecto al contenido de la base de datos principal. El servidor principal va enviando entradas del registro al servidor reflejado, que está aplicando los cambios a la base de datos reflejada para ponerla al día.<br /><br /> Al inicio de una sesión de creación de reflejo de la base de datos, la base de datos se encuentra en el estado SYNCHRONIZING. En este estado, el servidor principal sigue dando servicio a la base de datos, mientras que el reflejado intenta ponerse al día.|  
|SYNCHRONIZED|El estado de creación de reflejo cambia a SYNCHRONIZED cuando el servidor reflejado está suficientemente al día con respecto al servidor principal. La base de datos permanece en este estado mientras el servidor principal continúa con el envío de cambios al servidor reflejado, y el servidor reflejado continúa con la aplicación de los cambios en la base de datos reflejada.<br /><br /> Si la seguridad de las transacciones se establece en FULL, se admite la conmutación automática por error y la conmutación manual por error en el estado SYNCHRONIZED; no hay pérdida de datos tras la conmutación por error.<br /><br /> Si la seguridad de las transacciones está desactivada, siempre es posible sufrir alguna pérdida de datos, incluso en el estado SYNCHRONIZED.|  
|SUSPENDED|La copia reflejada de la base de datos no está disponible. La base de datos principal se ejecuta sin enviar registros al servidor reflejado, condición conocida como *ejecución expuesta*. Éste es el estado después de una conmutación por error.<br /><br /> Una sesión también puede tener el estado SUSPENDED como resultado de errores al rehacer, o bien si el administrador pone en pausa la sesión.<br /><br /> SUSPENDED es un estado persistente que sobrevive a los apagados e inicios de los asociados.|  
|PENDING_FAILOVER|Este estado se encuentra solo en el servidor principal después de que se haya iniciado una conmutación por error, pero el servidor todavía no se ha pasado al rol reflejado.<br /><br /> Cuando se inicia la conmutación por error, la base de datos principal pasa al estado PENDING_FAILOVER, finaliza rápidamente cualquier conexión de usuario y asume el rol reflejado inmediatamente.|  
|DISCONNECTED|El asociado ha perdido la comunicación con el otro asociado.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
