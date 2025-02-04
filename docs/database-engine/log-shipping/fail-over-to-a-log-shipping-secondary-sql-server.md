---
title: Conmutar por error a una base de datos secundaria de trasvase de registros (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- primary databases [SQL Server]
- secondary data files [SQL Server], manual fail over
- log shipping [SQL Server], failover
- failover [SQL Server], log shipping
ms.assetid: edfe5d59-4287-49c1-96c9-dd56212027bc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 76ab259ef9f87e9b2cc10eb616e1511d087d1fe6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057861"
---
# <a name="fail-over-to-a-log-shipping-secondary-sql-server"></a>Conmutar por error a una base de datos secundaria de trasvase de registros (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La conmutación por error a una base de datos secundaria de trasvase de registros es útil si la instancia del servidor principal produce un error o requiere mantenimiento.  
  
## <a name="preparing-for-a-controlled-failover"></a>Preparación para una conmutación por error controlada  
 Las bases de datos principal y secundaria no suelen estar sincronizadas, ya que la base de datos principal continúa actualizándose después del último trabajo de copia de seguridad. Además, en algunos casos, es posible que las copias de seguridad recientes del registro de transacciones no se hayan copiado en las instancias del servidor secundario, o bien que algunas copias de seguridad de registros copiadas aún no se hayan aplicado a la base de datos secundaria. Si es posible, se recomienda comenzar por la sincronización de todas las bases de datos secundarias con la base de datos principal.  
  
 Para obtener más información sobre los trabajos de trasvase de registros, vea [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="failing-over"></a>Realizar una conmutación por error  
 Para realizar una conmutación por error a una base de datos secundaria:  
  
1.  Copie los archivos de copia de seguridad que aún no se hayan copiado del recurso compartido de copia de seguridad en la carpeta de destino de la copia de cada servidor secundario.  
  
2.  Aplique, por orden, las copias de seguridad del registro de transacciones que aún no se hayan aplicado a las bases de datos secundarias. Para obtener más información, vea [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
3.  Si se puede tener acceso a la base de datos principal, realice una copia de seguridad del registro de transacciones activo y aplíquela a las bases de datos secundarias.  
  
     Si la instancia del servidor principal original no está dañada, realice una copia de seguridad del final del registro de transacciones de la base de datos principal mediante WITH NORECOVERY. Esto deja la base de datos en estado restauración y, por consiguiente, no disponible a los usuarios. Finalmente, podrá poner al día esta base de datos mediante la aplicación de copias de seguridad del registro de transacciones desde la base de datos principal de sustitución.  
  
     Para obtener más información, vea [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
4.  Una vez sincronizados los servidores secundarios, podrá realizar una conmutación por error al servidor que prefiera mediante la recuperación de su base de datos secundaria y la redirección de los clientes a dicha instancia de servidor. La recuperación coloca a la base de datos en un estado coherente y en línea.  
  
    > [!NOTE]  
    >  Cuando haga que una base de datos secundaria esté disponible, debe asegurarse de que sus metadatos sean coherentes con los metadatos de la base de datos principal original. Para obtener más información, vea [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
5.  Una vez que haya recuperado una base de datos secundaria, puede configurarla de nuevo para que actúe como base de datos principal para otras bases de datos secundarias.  
  
     Si no hay ninguna otra base de datos secundaria disponible, vea [Configurar el trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Cambiar los roles entre el servidor de trasvase de registros primario y secundario &#40;SQL Server&#41;](../../database-engine/log-shipping/change-roles-between-primary-and-secondary-log-shipping-servers-sql-server.md)  
  
-   [Administración de inicios de sesión y trabajos tras la conmutación de roles &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [Tablas y procedimientos almacenados de trasvase de registros](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)   
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Copias del final del registro &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)  
  
  
