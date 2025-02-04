---
title: Replicación de bases de datos heterogéneas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, about heterogeneous database replication
- replication [SQL Server], heterogeneous database replication
- heterogeneous database replication
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 543fd750047d171e353940bc2b4a22a4e54aed57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63022464"
---
# <a name="heterogeneous-database-replication"></a>replicación de bases de datos heterogéneas
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite los siguientes escenarios heterogéneos para la replicación de instantáneas y transaccional:  
  
-   Publicar datos de Oracle en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Publicar datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 La replicación heterogénea en suscriptores que no son SQL Server está desusada. La publicación de Oracle está desusada. Para mover datos, cree soluciones mediante captura de datos modificados y [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="publishing-data-from-oracle"></a>Publicar datos de Oracle  
 Puede usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para publicar datos de Oracle con la mayoría de características y la misma facilidad de uso que la replicación de instantáneas y transaccional de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La publicación de datos de Oracle es ideal en los siguientes escenarios:  
  
|Escenario|Descripción|  
|--------------|-----------------|  
|Implementaciones de aplicaciones de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Desarrolle con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando trabaje con datos replicados de una base de datos que no es de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Servidores provisionales de almacenamiento de datos|Mantenga las bases de datos provisionales de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sincronizadas con una base de datos que no es de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Migración a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Compruebe la aplicación en tiempo real con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mientras replica los cambios del sistema de origen. Cambie a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando esté satisfecho con la migración.|  
  
 Para obtener más información, vea [Oracle Publishing Overview](oracle-publishing-overview.md) (Información general de la publicación de Oracle).  
  
## <a name="publishing-data-to-non-sql-server-subscribers"></a>Publicar datos en suscriptores que no son de SQL Server  
 Las siguientes bases de datos que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] son compatibles como suscriptores de publicaciones de instantáneas y transaccionales:  
  
-   Oracle para todas las plataformas que admite Oracle.  
  
-   IBM DB2 para AS400, MVS, Unix, Linux y Windows  
  
 Para más información, consulte [Non-SQL Server Subscribers](non-sql-server-subscribers.md).  
  
  
