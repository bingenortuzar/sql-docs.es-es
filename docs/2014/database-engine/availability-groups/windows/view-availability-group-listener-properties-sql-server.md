---
title: Ver las propiedades del agente de escucha del grupo de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygrouplistenerproperties.general.f1
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
ms.assetid: aca0d016-3228-40b8-bdc3-285ed6d9b280
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bdec432699b7d0a6152509ec6a53ddf452376d5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788044"
---
# <a name="view-availability-group-listener-properties-sql-server"></a>Ver las propiedades del agente de escucha del grupo de disponibilidad (SQL Server)
  En este tema se describe cómo ver las propiedades de un *agente de escucha del grupo de disponibilidad* AlwaysOn mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Para ver las propiedades del agente de escucha, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para ver las propiedades del agente de escucha**  
  
1.  En el Explorador de objetos, conéctese a una instancia del servidor que hospeda una réplica de disponibilidad del grupo disponibilidad cuyo agente de escucha desea ver. Haga clic en el nombre del servidor para expandir el árbol.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Expanda el nodo del grupo de disponibilidad y expanda el nodo **Agentes de escucha de grupos de disponibilidad** .  
  
4.  Haga clic con el botón derecho en el agente de escucha que quiere ver y seleccione el comando **Propiedades** .  
  
5.  Se abrirá el cuadro de diálogo de **Propiedades del agente de escucha del grupo de disponibilidad** . Para obtener más información, vea [Propiedades del agente de escucha de grupo de disponibilidad (cuadro de diálogo)](#AgListenerPropertiesDialog), más adelante en este tema.  
  
###  <a name="AgListenerPropertiesDialog"></a> Propiedades del agente de escucha de grupo de disponibilidad (cuadro de diálogo)  
 **Nombre DNS del agente de escucha**  
 El nombre de red del agente de escucha del grupo de disponibilidad.  
  
 **Puerto**  
 El puerto TCP usado por este agente de escucha.  
  
> [!NOTE]  
>  Si está conectado a la réplica principal, puede utilizar este campo para modificar el número de puerto del agente de escucha. Esto requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
 **Modo de red**  
 Indica el protocolo TCP utilizado por el agente de escucha; puede ser:  
  
 **DHCP**  
 El agente de escucha utiliza una dirección IP dinámica asignada por un servidor que ejecute el protocolo DHCP (Protocolo de configuración dinámica de host).  
  
 **Dirección IP estática**  
 El agente de utiliza una o más direcciones IP estáticas. Para tener acceso a las diferentes subredes, un agente de escucha del grupo de disponibilidad debe utilizar direcciones IP estáticas.  
  
 La cuadrícula muestra cada una de las subredes en que el agente de escucha escucha y la dirección IP asociada a esa subred.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para ver las propiedades del agente de escucha**  
  
 Para supervisar los agentes de escucha del grupo de disponibilidad, utilice las vistas siguientes:  
  
 [sys.availability_group_listener_ip_addresses](/sql/relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql)  
 Devuelve una fila para cada dirección IP virtual conforme que está actualmente en línea para un agente de escucha del grupo de disponibilidad.  
  
 **Nombres de columna:** listener_id, ip_address, ip_subnet_mask, is_dhcp, network_subnet_ip, network_subnet_prefix_length, network_subnet_ipv4_mask, state, state_desc  
  
 [sys.availability_group_listeners](/sql/relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql)  
 Para un grupo de disponibilidad determinado, devuelve cero filas que indican que no hay ningún nombre de red asociado al grupo de disponibilidad o devuelve una fila por cada configuración de agente de escucha del grupo de disponibilidad del clúster de WSFC.  
  
 **Nombres de columna:** group_id, listener_id, dns_name, port, is_conformant, ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)  
 Devuelve una fila que contiene la información de estado dinámico para cada agente de escucha TCP.  
  
 **Nombres de columna:** listener_id, ip_address, is_ipv4, port, type, type_desc, state, state_desc, start_time  
  
> [!NOTE]  
>  Para obtener más información sobre cómo usar [!INCLUDE[tsql](../../../includes/tsql-md.md)] para supervisar el entorno de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , vea [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Quitar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](remove-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
  
