---
title: Base de datos de instantáneas con grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 7432da1c-ce2f-4cd9-af41-54c97744166b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cba02aa87e800391ffba3c791c1ee4341462c3f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62814661"
---
# <a name="database-snapshots-with-alwayson-availability-groups-sql-server"></a>Instantáneas de bases de datos con grupos de disponibilidad AlwaysOn (SQL Server)
  Puede crear una instantánea de base de datos en una base de datos primaria o secundaria en un grupo de disponibilidad. El rol de réplica debe ser PRIMARY o SECONDARY y no debe encontrarse en el estado RESOLVING.  
  
 Se recomienda que el estado de sincronización de la base de datos sea SYNCHRONIZING o SYNCHRONIZED cuando se crea una instantánea de base de datos. Sin embargo, las instantáneas de base de datos pueden crearse cuando el estado de sincronización de la base de datos sea NOT SYNCHRONIZING.  
  
 Una instantánea de base de datos debe seguir funcionando aunque la réplica se DESCONECTE de la réplica primaria.  
  
 Algunas condiciones de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] pueden hacer que la base de datos de origen y sus instantáneas de base de datos se reinicien y desconecten temporalmente a los usuarios. Estas condiciones son:  
  
-   La réplica principal cambia los roles, ya sea porque la réplica principal actual se queda sin conexión y vuelve a conectarse en la misma instancia del servidor o porque se produce un error en el grupo de disponibilidad.  
  
-   La base de datos entra en el rol secundario.  
  
 Si se produce una conmutación por error de la réplica de disponibilidad que hospeda las instantáneas de base de datos, estas permanecen en la instancia del servidor donde se crearon. Los usuarios pueden seguir usando las instantáneas tras la conmutación por error. Si el rendimiento es importante en el entorno, se recomienda crear instantáneas de base de datos solo en las bases de datos secundarias que estén hospedadas por una réplica secundaria configurada para el modo de conmutación por error manual.  Si alguna vez realiza una conmutación por error manual del grupo de disponibilidad en esta réplica secundaria, puede crear un conjunto de instantáneas de base de datos en otra réplica secundaria, redirigir a los clientes a las nuevas instantáneas de base de datos y quitar todas las instantáneas de las bases de datos principales.  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Instantáneas de bases de datos &#40;SQL Server&#41;](../../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
