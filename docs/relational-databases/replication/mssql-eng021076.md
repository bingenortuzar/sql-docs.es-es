---
title: MSSQL_ENG021076 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021076 error
ms.assetid: 612e5c59-ba3e-49c3-a3df-56bac3d850a2
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 20f819b4a4751ca46f3e010954508486827f7ae3
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770346"
---
# <a name="mssqleng021076"></a>MSSQL_ENG021076
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21076|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|La instantánea inicial del artículo '%1!' aún no está disponible.|  
  
## <a name="explanation"></a>Explicación  
 El error MSSQL_ENG021076 puede producirse si el Agente de distribución se inicia antes de que el Agente de instantáneas haya terminado de generar la instantánea. El error se produce solo si la publicación contiene un único artículo. Si la publicación contiene más de un artículo, en su lugar se produce el error MSSQL_ENG021075. Para más información, consulte [MSSQL_ENG021075](../../relational-databases/replication/mssql-eng021075.md).  
  
## <a name="user-action"></a>Acción del usuario  
 Si el Agente de instantáneas para la publicación no se ha iniciado desde que se creó la suscripción, o si no se ha iniciado desde la última vez que decidió reinicializar la suscripción, inicie el Agente de instantáneas y deje que se complete antes de iniciar el Agente de distribución. Para obtener más información, vea [Crear y aplicar una instantánea](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
 Si no finaliza el Agente de instantáneas, revise el historial del Agente de instantáneas para detectar posibles errores y soluciónelos. Para obtener información sobre la visualización del estado y los errores en Monitor de replicación, vea [Visualización de información y realización de tareas mediante el Monitor de replicación](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Si el error persiste, aumente el registro del agente y especifique un archivo de salida para el registro. Dependiendo del contexto del error, esto puede proporcionar los pasos que conducen al error o a mensajes de error adicionales.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
