---
title: Iniciar el Monitor de replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, starting
ms.assetid: e037bd27-cc87-4ee9-9e5f-83f6d717cfa4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: ebf3dcfa2671fb2388cbe4a0ec1ddb0a9510445d
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770533"
---
# <a name="start-the-replication-monitor"></a>Iniciar el Monitor de replicación
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  El Monitor de replicación se puede iniciar desde [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] en cualquier instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o desde el símbolo del sistema. Tras iniciar el Monitor de replicación, agregue uno o más publicadores para supervisión. Para obtener más información, vea [Agregar y quitar publicadores del Monitor de replicación](../../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md).  
  
### <a name="to-start-replication-monitor-from-sql-server-management-studio"></a>Para iniciar el Monitor de replicación desde SQL Server Management Studio  
  
1.  Conéctese a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]y expanda el nodo de servidor.  
  
2.  Haga clic con el botón secundario en la carpeta **Replicación** o en cualquiera de sus subcarpetas y, a continuación, haga clic en **Iniciar Monitor de replicación**.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

### <a name="to-start-replication-monitor-from-the-command-prompt"></a>Para iniciar el Monitor de replicación desde el símbolo del sistema  
  
1.  Desde el símbolo del sistema, navegue al directorio de instalación de herramientas. La ruta de acceso predeterminada es [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]Tools\Binn\.  
  
2.  Ejecute sqlmonitor.exe.  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
