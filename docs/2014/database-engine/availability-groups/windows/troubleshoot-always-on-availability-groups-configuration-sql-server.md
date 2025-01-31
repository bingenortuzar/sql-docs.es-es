---
title: Solución de problemas de configuración de grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [SQL Server], deploying
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], configuring
ms.assetid: 8c222f98-7392-4faf-b7ad-5fb60ffa237e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d1756c80b86ec9b8c16792bf488cc1d3d19b590d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813168"
---
# <a name="troubleshoot-alwayson-availability-groups-configuration-sql-server"></a>Solucionar problemas de configuración de grupos de disponibilidad AlwaysOn (SQL Server)
  En este tema se proporciona información para ayudarle a solucionar los problemas más habituales relacionados con la configuración de las instancias de servidor para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Entre los problemas de configuración más habituales se incluyen los siguientes: [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] está deshabilitado, las cuentas no están configuradas correctamente, el extremo de creación de reflejo de la base de datos no existe, el extremo no es accesible (error 1418 de SQL Server), el acceso de red no existe y un comando de unión genera el error 35250 de SQL Server.  
  
> [!NOTE]  
>  Asegúrese de que cumple los requisitos previos de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Para más información, vea [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
 **En este tema:**  
  
|Section|Descripción|  
|-------------|-----------------|  
|[Grupos de disponibilidad AlwaysOn no está habilitado](#IsHadrEnabled)|Si una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no está habilitada para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], la instancia no admite la creación de grupos de disponibilidad y no puede hospedar réplicas de disponibilidad.|  
|[Cuentas](#Accounts)|Analiza los requisitos para configurar correctamente las cuentas en que se ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|[Extremos](#Endpoints)|Analiza cómo diagnosticar problemas relativos al extremo de creación de reflejo de la base de datos de una instancia de servidor.|  
|[Nombre del sistema](#SystemName)|Resume las alternativas para especificar el nombre del sistema de una instancia de servidor en una dirección URL del extremo.|  
|[Acceso de red](#NetworkAccess)|Documenta el requisito de que cada instancia de servidor que hospeda una réplica de disponibilidad debe tener acceso al puerto de cada una de las demás instancias de servidor en TCP.|  
|[Acceso al extremo (error 1418 de SQL Server)](#Msg1418)|Contiene información sobre este mensaje de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|[Error de unión de la base de datos (error 35250 de SQL Server)](#JoinDbFails)|Analiza las posibles causas y la resolución de un error al unir las bases de datos secundarias a un grupo de disponibilidad porque la conexión a la réplica principal no está activa.|  
|[El enrutamiento de solo lectura no funciona correctamente](#ROR)||  
|[Tareas relacionadas](#RelatedTasks)|Contiene una lista de temas orientados a tareas de los Libros en pantalla de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que son particularmente especialmente pertinentes para solucionar problemas de configuración de un grupo de disponibilidad.|  
|[Contenido relacionado](#RelatedContent)|Contiene una lista de recursos importantes externos a los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
  
##  <a name="IsHadrEnabled"></a> Grupos de disponibilidad AlwaysOn no está habilitado  
 La característica [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] debe estar habilitada en cada instancia de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Para obtener más información, vea [Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md).  
  
##  <a name="Accounts"></a> Cuentas  
 Las cuentas en las que se ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deben estar configuradas correctamente.  
  
1.  ¿Tienen las cuentas los permisos adecuados?  
  
    1.  Si los asociados se ejecutan como la misma cuenta de usuario de dominio, automáticamente existen los inicios de sesión de usuario correctos en ambas bases de datos **maestra** . Esto simplifica la configuración de seguridad de la base de datos y es recomendable su aplicación.  
  
    2.  Si dos instancias del servidor se ejecutan como cuentas diferentes, el inicio de sesión en cada cuenta debe crearse en la base de datos **maestra** en la instancia del servidor remoto, y se deben conceder a ese inicio de sesión permisos CONNECT para conectarse al extremo de creación de reflejo de la base de datos de esa instancia del servidor. Para obtener más información, consulte[configurar inicio de sesión de cuentas para la creación de reflejo de base de datos o grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md).  
  
2.  Si [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se ejecuta como una cuenta integrada, (como sistema local, servicio local o servicio de red), o una cuenta que no es de dominio, debe utilizar certificados para la autenticación de extremos. Si las cuentas de servicio utilizan cuentas de dominio en el mismo dominio, puede elegir conceder acceso CONNECT para cada cuenta de servicio en todas las ubicaciones de réplica o puede utilizar certificados. Para obtener más información, vea [Usar certificados para un punto de conexión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md).  
  
##  <a name="Endpoints"></a> Extremos  
 Los extremos deben estar configurados correctamente.  
  
1.  Asegúrese de que cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que vaya a hospedar una réplica de disponibilidad (cada *ubicación de réplica*) tenga un punto de conexión de creación de reflejo de la base de datos. Para determinar si existe un punto de conexión de creación de reflejo de la base de datos en una instancia de servidor determinada, use la vista de catálogo [sys.database_mirroring_endpoints](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql). Para obtener más información, vea [Crear un punto de conexión de creación de reflejo de la base de datos para la autenticación de Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md) o [Permitir que un punto de conexión de creación de reflejo de la base de datos utilice certificados para las conexiones entrantes &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md).  
  
2.  Compruebe que los números de puerto son correctos.  
  
     Para identificar el puerto asociado actualmente al extremo de creación de reflejo de la base de datos de una instancia de servidor, utilice la siguiente instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] :  
  
    ```  
    SELECT type_desc, port FROM sys.tcp_endpoints;  
    GO  
    ```  
  
3.  En caso de problemas de configuración de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] difíciles de explicar, se recomienda que compruebe cada una de las instancias de servidor para determinar si escuchan en los puertos correctos. Para obtener más información sobre la comprobación de disponibilidad de puertos, vea [MSSQLSERVER_1418](../../../relational-databases/errors-events/mssqlserver-1418-database-engine-error.md).  
  
4.  Asegúrese de que se han iniciado los extremos (STATE=STARTED). En cada una de las instancias de servidor, utilice la siguiente instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)]:  
  
    ```  
    SELECT state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
     Para obtener más información sobre la columna **state_desc**, vea [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql).  
  
     Para iniciar un extremo, utilice la siguiente instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)]:  
  
    ```  
    ALTER ENDPOINT Endpoint_Mirroring   
    STATE = STARTED   
    AS TCP (LISTENER_PORT = <port_number>)  
    FOR database_mirroring (ROLE = ALL);  
    GO  
    ```  
  
     Para obtener más información, vea [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql).  
  
5.  Asegúrese de que el inicio de sesión del otro servidor dispone de permiso CONNECT. Para determinar quién tiene permiso CONNECT para un extremo, utilice la siguiente instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] en cada instancia de servidor:  
  
    ```  
    SELECT 'Metadata Check';  
    SELECT EP.name, SP.STATE,   
       CONVERT(nvarchar(38), suser_name(SP.grantor_principal_id))   
          AS GRANTOR,   
       SP.TYPE AS PERMISSION,  
       CONVERT(nvarchar(46),suser_name(SP.grantee_principal_id))   
          AS GRANTEE   
       FROM sys.server_permissions SP , sys.endpoints EP  
       WHERE SP.major_id = EP.endpoint_id  
       ORDER BY Permission,grantor, grantee;   
    GO  
  
    ```  
  
##  <a name="SystemName"></a> System Name  
 Como nombre del sistema de una instancia de servidor en una dirección URL del extremo, se puede utilizar cualquier nombre que identifique el sistema de forma inequívoca. La dirección del sistema puede ser un nombre del sistema (si los sistemas se encuentran en el mismo dominio), un nombre de dominio completo o una dirección IP (de preferencia, una dirección IP estática). Se garantiza que el uso de un nombre de dominio completo funciona correctamente. Para obtener más información, vea [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
##  <a name="NetworkAccess"></a> Network Access  
 Cada instancia de servidor que hospeda una réplica de disponibilidad debe tener acceso al puerto de cada una de las demás instancias de servidor en TCP. Esto es especialmente importante si las instancias de servidor están en distintos dominios que no confían unos en otros (dominios que no son de confianza).  
  
##  <a name="Msg1418"></a> Acceso al extremo (error 1418 de SQL Server)  
 Este mensaje de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] indica que la dirección de red del servidor especificada en la dirección URL del extremo no se encuentra o no existe, y recomienda que se compruebe el nombre de dirección de red y se vuelva a emitir el comando. Para obtener más información, vea [MSSQLSERVER_1418](../../../relational-databases/errors-events/mssqlserver-1418-database-engine-error.md).  
  
##  <a name="JoinDbFails"></a> Error de unión de la base de datos (error 35250 de SQL Server)  
 En esta sección se analiza las posibles causas y la resolución de un error al unir las bases de datos secundarias al grupo de disponibilidad porque la conexión a la réplica principal no está activa.  
  
 **Solución:**  
  
1.  Compruebe la configuración de firewall para ver si permite la comunicación de puerto del extremo entre las instancias de servidor que hospedan la réplica principal y la réplica secundaria (puerto 5022 de forma predeterminada).  
  
2.  Compruebe si la cuenta de servicio de red tiene permiso de conexión para el extremo.  
  
##  <a name="ROR"></a> El enrutamiento de solo lectura no funciona correctamente  
 Compruebe los siguientes valores de configuración y corríjalos si es necesario.  
  
||En...|Acción|Comentarios|Vínculo|  
|------|---------|------------|--------------|----------|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Réplica principal actual|Asegúrese de que el agente de escucha del grupo de disponibilidad está en línea.|**Para comprobar si el agente de escucha está en línea:**<br /><br /> `SELECT * FROM sys.dm_tcp_listener_states;`<br /><br /> **Para reiniciar un agente de escucha sin conexión:**<br /><br /> `ALTER AVAILABILITY GROUP myAG RESTART LISTENER 'myAG_Listener';`|[sys.dm_tcp_listener_states &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Réplica principal actual|Asegúrese de que READ_ONLY_ROUTING_LIST contiene solo instancias de servidor que hospedan una réplica secundaria legible.|**Para identificar réplicas secundarias legibles:** sys.availability_replicas (columna**secondary_role_allow_connections_desc** )<br /><br /> **Para ver una lista de enrutamiento de solo lectura:** sys.availability_read_only_routing_lists<br /><br /> **Para cambiar una lista de enrutamiento de solo lectura:** ALTER AVAILABILITY GROUP|[sys.availability_replicas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)<br /><br /> [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Todas las réplicas de read_only_routing_list|Asegúrese de que el firewall de Windows no está bloqueando el puerto de READ_ONLY_ROUTING_URL.|-|[Configurar Firewall de Windows para el acceso al motor de base de datos](../../configure-windows/configure-a-windows-firewall-for-database-engine-access.md)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Todas las réplicas de read_only_routing_list|En el Administrador de configuración [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , compruebe lo siguiente:<br /><br /> La conectividad remota de SQL Server está habilitada.<br /><br /> TCP/IP está habilitado.<br /><br /> Las direcciones IP están configuradas correctamente.|-|[Ver o cambiar las propiedades del servidor &#40;SQL Server&#41;](../../configure-windows/view-or-change-server-properties-sql-server.md)<br /><br /> [Configurar un servidor para que escuche en un puerto TCP específico &#40;Administrador de configuración de SQL Server&#41;](../../configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Todas las réplicas de read_only_routing_list|Asegúrese de que READ_ONLY_ROUTING_URL (TCP<strong>:// *`system-address`* :</strong>*puerto*) contiene el nombre correcto de dominio completo (FQDN) y el número de puerto.|-|[Calcular read_only_routing_url para AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)<br /><br /> [sys.availability_replicas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)|  
|![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Sistema cliente|Compruebe que el controlador cliente admite el enrutamiento de solo lectura.|-|[Conectividad de cliente de AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md)|  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Crear un punto de conexión de creación de reflejo de la base de datos para la autenticación de Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Solución de problemas de una operación de agregar archivos con error &#40;grupos de disponibilidad AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
-   [Administración de inicios de sesión y de trabajos para las bases de datos de un grupo de disponibilidad &#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)  
  
-   [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](../../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Ver eventos y registros para un clúster de conmutación por error](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Cmdlet de clúster de conmutación por error Get-ClusterLog](https://technet.microsoft.com/library/ee461045.aspx)  
  
-   [Blog del equipo de AlwaysOn SQL Server: El blog del equipo de AlwaysOn oficial SQL Server](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de transporte para la creación de reflejo de base de datos y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Configuración de red de cliente](../../configure-windows/client-network-configuration.md)   
 [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
