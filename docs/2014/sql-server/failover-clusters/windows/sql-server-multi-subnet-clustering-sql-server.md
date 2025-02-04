---
title: Agrupación en clústeres de varias subredes de SQL Server (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- stretch cluster
- Availability Groups [SQL Server], WSFC clusters
- failover clustering [SQL Server], AlwaysOn Availability Groups
- multi-site failover cluster
- failover clustering [SQL Server]
ms.assetid: cd909612-99cc-4962-a8fb-e9a5b918e221
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: be4125f417b6333bfcb3002b15f1319f484d22a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049478"
---
# <a name="sql-server-multi-subnet-clustering-sql-server"></a>Agrupación en clústeres de varias subredes de SQL Server (SQL Server)
  Un clúster de conmutación por error de múltiples subredes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es una configuración donde cada nodo clúster se conecta a una subred diferente o un conjunto de subredes diferente. Estas subredes pueden estar en la misma ubicación o en sitios geográficamente dispersos. A veces se hace referencia a la agrupación en clústeres en sitios geográficamente dispersos como clústeres elásticos. Como no existe ningún almacenamiento compartido al que todos los nodos puedan tener acceso, los datos se deben replicar entre el almacenamiento de datos en las diversas subredes. Con la replicación de datos, hay más de una copia de los datos disponible. Por consiguiente, un clúster de conmutación por error de múltiples subredes proporciona una solución de recuperación ante desastres además de alta disponibilidad.  
  
 
  
##  <a name="VisualElement"></a> Clúster de conmutación por error de múltiples subredes de SQL Server (dos nodos, dos subredes)  
 La ilustración siguiente representa una instancia de clúster de conmutación por error (FCI) con dos nodos y dos subredes en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 ![Arquitectura de múltiples subredes con MultiSubnetFailover](../../../database-engine/media/multi-subnet-architecture-withmultisubnetfailoverparam.gif "Arquitectura de múltiples subredes con MultiSubnetFailover")  
  

  
##  <a name="Configurations"></a> Configuraciones de instancias de clúster de conmutación por error de múltiples subredes.  
 Los siguientes son algunos ejemplos de configuraciones de clúster de conmutación por error (FCI) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que usan múltiples subredes:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQLCLUST1 incluye Nodo1 y Nodo2. Nodo1 se conecta a Subred1. Nodo2 se conecta a Subred2. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] El programa de instalación ve esta configuración como un clúster de múltiples subredes y establece la dependencia de recursos de la dirección IP en **OR**.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQLCLUST1 incluye Nodo1, Nodo2 y Node3. Nodo1 y Nodo2 se conectan a Subred1. Nodo 3 se conecta a Subred2. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] El programa de instalación ve esta configuración como un clúster de múltiples subredes y establece la dependencia de recursos de la dirección IP en **OR**. Dado que Nodo1 y Nodo2 están en la misma subred, esta configuración proporciona alta disponibilidad local adicional.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQLCLUST1 incluye Nodo1 y Nodo2. Nodo1 están en Subred1. Nodo2 está conectado a Subred1 y Subred2. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] El programa de instalación ve esta configuración como un clúster de múltiples subredes y establece la dependencia de recursos de la dirección IP en **OR**.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQLCLUST1 incluye Nodo1 y Nodo2. Nodo1 está conectado a Subred1 y Subred2. Nodo2 también está conectado a Subred1 y Subred2. La dependencia de recurso de dirección IP la establece en **AND** el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    > [!NOTE]  
    >  Esta configuración no se considera una configuración de clúster de conmutación por error de múltiples subredes porque los nodos clúster están en el mismo conjunto de subredes.  
  
##  <a name="ComponentsAndConcepts"></a> Consideraciones de recursos de dirección IP  
 En una configuración de clúster de conmutación por error de múltiples subredes, no todos los nodos clúster de conmutación por error poseen las direcciones IP y puede que no todos estén con conexión durante el inicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], se puede establecer la dependencia de recurso de dirección IP en **OR**. Esto permite que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esté con conexión cuando hay al menos una dirección IP válida a la que se puede enlazar.  
  
> [!NOTE]  
>  En las versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], se utilizaba una tecnología de V-LAN elástica en las configuraciones de clúster de varios sitios para exponer una sola dirección IP para la conmutación por error entre sitios. Con la nueva capacidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para agrupar los nodos de clúster entre diferentes subredes, ahora se pueden configurar los clústeres de conmutación por error [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] entre varios sitios sin necesidad de implementar la tecnología de V-LAN elástica.  
  
### <a name="ip-address-resource-or-dependency-considerations"></a>Consideraciones acerca de la dependencia OR del recurso de dirección IP  
 Es conveniente considerar el siguiente comportamiento de la conmutación por error si se establece en **OR**la dependencia de recurso de dirección IP:  
  
-   Cuando se produce un error de una de las direcciones IP en el nodo que actualmente posee el grupo de recursos del clúster [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , no se activa automáticamente una conmutación por error hasta que produzcan un error todas las direcciones IP válidas en ese nodo.  
  
-   Cuando se produce una conmutación por error, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se pondrán con conexión si se puede enlazar al menos a una dirección IP que sea válida en el nodo actual. Las direcciones IP que no se enlazan a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el inicio se enumerarán en el registro de errores.  
  
  
  
 Al instalar una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en paralelo con una instancia independiente de [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)], tenga cuidado para evitar conflictos de número de puerto TCP en las direcciones IP. Los conflictos suelen suceder cuando se configuran dos instancias de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para usar el puerto TCP (1433). Para evitar conflictos, configure una instancia para que utilice un puerto fijo predeterminado. La configuración de un puerto fijo es normalmente lo más sencillo en el caso de la instancia independiente. La configuración del [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para usar puertos diferentes evitará un conflicto inesperado entre el puerto TCP y la dirección IP que bloquea la instancia cuando una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] produce un error en el nodo en espera.  
  
##  <a name="DNS"></a> Latencia de recuperación de cliente durante conmutaciones por error  
 Una instancia de clúster de conmutación por error de múltiples subredes habilita de forma predeterminada el recurso de clúster RegisterAllProvidersIP para el nombre de red. En una configuración de múltiples subredes, las direcciones IP en línea y sin conexión del nombre red se registra en el servidor DNS. La aplicación cliente recupera a continuación todas las direcciones IP registradas del servidor DNS e intenta la conexión con las direcciones en orden o en paralelo. Esto significa que el tiempo de recuperación de cliente en clústeres de conmutación por error de múltiples subredes deja de depender de las latencias de actualización de DNS. De forma predeterminada, el cliente intenta las direcciones IP en orden. Cuando el cliente utiliza el nuevo parámetro opcional `MultiSubnetFailover=True` en la cadena de conexión, intentará en su lugar las direcciones IP simultáneamente y las conexiones al primer servidor que responda. Esto puede ayudar a reducir al mínimo la latencia de recuperación de cliente cuando se produzcan conmutaciones por error. Para obtener más información, consulte [conectividad de cliente de AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md) y [crear o configurar un agente de escucha del grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
 Con las bibliotecas de cliente heredadas o con proveedores de datos de terceros, no puede utilizar el parámetro `MultiSubnetFailover` en la cadena de conexión. Para asegurarse de que la aplicación cliente funcione de manera óptima con instancias de conmutación por error de múltiples subredes en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], intente ajustar el tiempo de espera de conexión en la cadena de conexión de cliente en 21 segundos para cada dirección IP adicional. Esto garantiza que el intento de reconexión del cliente no supere el tiempo de espera antes de poder recorrer todas las direcciones IP en la instancia de conmutación por error de múltiples subredes.  
  
 El período de tiempo de espera predeterminado de la conexión de cliente para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio y **sqlcmd** es de 15 segundos.  
  
 
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
|Descripción del contenido|Tema|  
|-------------------------|-----------|  
|Instalar un clúster de conmutación por error de SQL Server|[Crear un nuevo clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../install/create-a-new-sql-server-failover-cluster-setup.md)|  
|Actualización en contexto del clúster de conmutación por error existente de SQL Server|[Actualizar una instancia de clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|Mantener el clúster de conmutación por error existente de SQL Server|[Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
|Clústeres de conmutación por error de Windows|[Prácticas recomendadas de clúster de conmutación por error de varios sitios de Microsoft Windows](https://secureinfra.blog/2013/11/09/microsoft-windows-multi-site-failover-cluster-best-practices/)|  
|Usar el complemento Administración del clúster de conmutación por error para ver eventos y registros de WSFC|[View Events and Logs for a Failover Cluster](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)|  
|Usar Windows PowerShell para crear un archivo de registro para todos los nodos (o un determinado nodo) en un clúster de conmutación por error de WSFC|[Cmdlet de clúster de conmutación por error Get-ClusterLog](https://technet.microsoft.com/library/ee461045.aspx)|  
  
 
  
  
