---
title: Algunas réplicas de disponibilidad no sincronizan datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0fb7d422687d0bc956937b30bae261b28edb3931
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788264"
---
# <a name="some-availability-replicas-are-not-synchronizing-data"></a>Algunas réplicas de disponibilidad no sincronizan datos
    
## <a name="introduction"></a>Introducción  
  
|||  
|-|-|  
|**Nombre de directiva**|Estado de sincronización de datos de las réplicas de disponibilidad|  
|**Problema**|Algunas réplicas de disponibilidad no sincronizan datos.|  
|**Categoría**|**Advertencia**|  
|**Faceta**|grupo de disponibilidad|  
  
## <a name="description"></a>Descripción  
 Esta directiva acumula el estado de sincronización de datos de todas las réplicas de disponibilidad en el grupo de disponibilidad y comprueba si la sincronización de alguna réplica de disponibilidad no está operativa. La directiva está en mal estado si alguno de los estados de sincronización de datos de la réplica de disponibilidad es NOT SYNCHRONIZING.  
  
 Esta directiva está en un estado correcto si ninguno de los estados de sincronización de datos de la réplica de disponibilidad es NOT SYNCHRONIZING.  
  
> [!NOTE]  
>  Para esta versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], la información sobre las posibles causas y soluciones se encuentra en el artículo [Algunas réplicas de disponibilidad no sincronizan datos](https://go.microsoft.com/fwlink/p/?LinkId=220852) de la wiki de TechNet.  
  
## <a name="possible-causes"></a>Posibles causas  
 En este grupo de disponibilidad, al menos una réplica secundaria tiene un estado de sincronización NOT SYNCHRONIZING y no recibe datos de la réplica principal.  
  
## <a name="possible-solution"></a>Solución posible  
 Use el estado de directiva de la réplica de disponibilidad para buscar la réplica de disponibilidad con un estado NOT SYNCHRONIZING y, a continuación, resuelva el problema en la réplica de disponibilidad.  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
