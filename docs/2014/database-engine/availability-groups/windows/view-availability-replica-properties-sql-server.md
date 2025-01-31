---
title: Ver las propiedades de una réplica de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- ', policies'
ms.assetid: 14fed3c4-8ecc-4e1c-931d-a7ec1e9f9e90
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a1ca87fc977ee97900be9e821cab4918064c7a44
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788011"
---
# <a name="view-availability-replica-properties-sql-server"></a>Ver las propiedades de una réplica de disponibilidad (SQL Server)
  En este tema se describe cómo pueden verse las propiedades de una réplica de un grupo disponibilidad AlwaysOn con [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para ver y cambiar las propiedades de una réplica de disponibilidad**  
  
1.  En el Explorador de objetos, conéctese a la instancia del servidor que hospeda la réplica principal y expanda el árbol.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Expanda el grupo de disponibilidad al que la pertenece la réplica de disponibilidad y expanda el nodo **Réplicas de disponibilidad** .  
  
4.  Haga clic con el botón derecho en la réplica de disponibilidad cuyas propiedades quiera ver y seleccione el comando **Propiedades** .  
  
5.  En el cuadro de diálogo **Propiedades de réplica de disponibilidad** , utilice la página **General** para ver las propiedades de esta réplica. Si está conectado a la réplica principal, puede cambiar las propiedades siguientes: modo de disponibilidad, modo de conmutación por error, acceso de conexión para el rol principal, acceso de lectura para el rol secundario (legible-secundario), y el valor de tiempo de espera de la sesión. Para obtener más información, consulte [propiedades de réplica de disponibilidad &#40;página General&#41;](availability-replica-properties-general-page.md).  
  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para ver las propiedades y estados de las réplicas de disponibilidad**  
  
 Para ver las propiedades y estados de las réplicas de disponibilidad, utilice las siguientes vistas y la función del sistema:  
  
 [sys.availability_replicas](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)  
 Devuelve una fila para cada una de las réplicas de disponibilidad en cada grupo de disponibilidad para el que la instancia local de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hospeda una réplica de disponibilidad.  
  
 **Nombres de columna:** replica_id, group_id, replica_metadata_id, replica_server_name, owner_sid, endpoint_url, availability_mode, availability_mode_desc, failover_mode, failover_mode_desc, session_timeout, primary_role_allow_connections, primary_role_allow_connections_desc, secondary_role_allow_connections, secondary_role_allow_connections_desc, create_date, modify_date, backup_priority, read_only_routing_url  
  
 [sys.availability_read_only_routing_lists](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
 Devuelve una fila para la lista de enrutamiento de solo lectura de cada réplica de disponibilidad en un grupo de disponibilidad AlwaysOn en el clúster de conmutación por error de WSFC.  
  
 **Nombres de columna:** replica_id, routing_priority, read_only_replica_id  
  
 [sys.dm_hadr_availability_replica_cluster_nodes](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql)  
 Devuelve una fila para cada réplica de disponibilidad (independientemente del estado de unión) de los grupos de disponibilidad AlwaysOn del clúster de clústeres de conmutación por error de Windows Server (WSFC).  
  
 **Nombres de columna:** group_name, replica_server_name, node_name  
  
 [sys.dm_hadr_availability_replica_cluster_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql)  
 Devuelve una fila para cada réplica (independientemente del estado de unión) de todos los grupos de disponibilidad AlwaysOn (independientemente de la ubicación de la réplica) del clúster de clústeres de conmutación por error de Windows Server (WSFC).  
  
 **Nombres de columna:** replica_id, replica_server_name, group_id, join_state, join_state_desc  
  
 [sys.dm_hadr_availability_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)  
 Devuelve una fila que muestra el estado de cada réplica de disponibilidad local y una fila para cada réplica de disponibilidad remota en el mismo grupo de disponibilidad.  
  
 **Nombres de columna:** replica_id, group_id, is_local, role, role_desc, operational_state, operational_state_desc, connected_state, connected_state_desc, recovery_health, recovery_health_desc, synchronization_health, synchronization_health_desc, last_connect_error_number, last_connect_error_description y last_connect_error_timestamp  
  
 [sys.fn_hadr_backup_is_preferred_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
 Determina si la réplica actual es la réplica de copia de seguridad preferida. Devuelve 1 si la base de datos de la instancia de servidor actual es la réplica preferida. De lo contrario, devuelve 0.  
  
> [!NOTE]  
>  Para obtener más información sobre los contadores de rendimiento para réplicas de disponibilidad (el objeto de rendimiento **SQLServer:Availability Replica**  ), vea [SQL Server, réplica de disponibilidad](../../../relational-databases/performance-monitor/sql-server-availability-replica.md).  
  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para obtener más información acerca de los grupos de disponibilidad**  
  
-   [Ver las propiedades del grupo de disponibilidad &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
-   [Ver las propiedades del agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)  
  
-   [Directivas de AlwaysOn para problemas operativos con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)
  
-   [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
 **Para administrar las réplicas de disponibilidad**  
  
-   [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Combinar una réplica secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Cambiar el modo de disponibilidad de una réplica de disponibilidad &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Cambiar el modo de conmutación por error de una réplica de disponibilidad &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Cambiar el tiempo de espera de la sesión en una réplica de disponibilidad &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
-   [Quitar una réplica secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
 **Para administrar una base de datos de disponibilidad**  
  
-   [Agregar una base de datos a un grupo de disponibilidad &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [Combinar una base de datos secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Suspender una base de datos de disponibilidad &#40;SQL Server&#41;](suspend-an-availability-database-sql-server.md)  
  
-   [Reanudar una base de datos de disponibilidad &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)  
  
-   [Quitar una base de datos secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Quitar una base de datos principal de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)   
 [Directivas de AlwaysOn para problemas operativos con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)   
 [Administración de un grupo de disponibilidad &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)  
  
  
