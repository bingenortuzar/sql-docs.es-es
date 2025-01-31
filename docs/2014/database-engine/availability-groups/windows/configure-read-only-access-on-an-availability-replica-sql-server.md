---
title: Configurar el acceso de solo lectura en una réplica de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 22387419-22c4-43fa-851c-5fecec4b049b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aaed1030d35fffb1b539339dc882cfb2d6676229
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62815378"
---
# <a name="configure-read-only-access-on-an-availability-replica-sql-server"></a>Configurar el acceso de solo lectura en una réplica de disponibilidad (SQL Server)
  De forma predeterminada, tanto el acceso de lectura y escritura como de intento de lectura se permiten en la réplica principal. No se permiten conexiones en las réplicas secundarias de un grupo de disponibilidad AlwaysOn. En este tema se describe cómo se configura el acceso de conexión de una réplica de disponibilidad de un grupo de disponibilidad AlwaysOn en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell.  
  
 Para obtener información sobre las implicaciones de habilitar el acceso de solo lectura en una réplica secundaria y una introducción al acceso de conexión, vea [Acerca del acceso de conexión de cliente a réplicas de disponibilidad &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md) y [Secundarias activas: Las réplicas secundarias legibles &#40;grupos de disponibilidad AlwaysOn&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos y restricciones  
  
-   Para configurar otro acceso de conexión, debe estar conectado a la instancia de servidor que hospeda la réplica principal.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
  
|Tarea|Permisos|  
|----------|-----------------|  
|Para configurar réplicas al crear un grupo de disponibilidad|Se requiere la pertenencia al rol fijo de servidor **sysadmin** y el permiso de servidor CREATE AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.|  
|Para modificar una réplica de disponibilidad|Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.|  
  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para configurar el acceso en una réplica de disponibilidad**  
  
1.  En el Explorador de objetos, conéctese a la instancia del servidor que hospeda la réplica principal y expanda el árbol.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Haga clic en el grupo de disponibilidad cuya réplica desea cambiar.  
  
4.  Haga clic con el botón derecho en la réplica de disponibilidad y haga clic en **Propiedades**.  
  
5.  En el cuadro de diálogo **Propiedades de réplica de disponibilidad** , puede cambiar el acceso de conexión para el rol principal y para el secundario, del siguiente modo:  
  
    -   Para el rol secundario, seleccione un nuevo valor en la lista desplegable **Secundario legible** , del siguiente modo:  
  
         **No**  
         No se permiten conexiones de usuario a las bases de datos secundarias de esta réplica. No están disponibles para acceso de lectura. Esta es la configuración predeterminada.  
  
         **Solo intento de lectura**  
         Únicamente se permiten conexiones de solo lectura a las bases de datos secundarias de esta réplica. Todas las bases de datos secundarias están disponibles para acceso de lectura.  
  
         **Sí**  
         Se permiten todas las conexiones a las bases de datos secundarias de esta réplica, pero solo para acceso de lectura. Todas las bases de datos secundarias están disponibles para acceso de lectura.  
  
    -   Para el rol principal, seleccione un nuevo valor en la lista desplegable **Conexiones de rol principal** , del siguiente modo:  
  
         **Permitir todas las conexiones**  
         Se permiten todas las conexiones con las bases de datos de la réplica principal. Esta es la configuración predeterminada.  
  
         **Permitir conexiones de lectura o escritura**  
         Cuando la propiedad Application Intent está establecida en **ReadWrite** o no tiene ningún valor, se permite la conexión. No se permiten las conexiones en las que la propiedad de conexión Application Intent esté establecida en **ReadOnly** . Esto puede ayudar a evitar que los clientes conecten por equivocación una carga de trabajo de intención de lectura a la réplica principal. Para obtener más información sobre propiedad de conexión Application Intent, vea [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para configurar el acceso en una réplica de disponibilidad**  
  
> [!NOTE]  
>  Para ver un ejemplo de este procedimiento, vea [Ejemplo (Transact-SQL)](#TsqlExample)más adelante en esta sección.  
  
1.  Conéctese a la instancia del servidor que hospeda la réplica principal.  
  
2.  Si va a especificar una réplica para un nuevo grupo de disponibilidad, use la instrucción [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Si va a agregar o modificar una réplica de un grupo de disponibilidad existente, use la instrucción [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) de [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
    -   Para configurar el acceso de conexión para el rol secundario, en la cláusula ADD REPLICA o MODIFY REPLICA WITH, especifique la opción SECONDARY_ROLE, del siguiente modo:  
  
         SECONDARY_ROLE **(** ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL } **)**  
  
         donde,  
  
         No  
         No se permiten conexiones directas a las bases de datos secundarias de esta réplica. No están disponibles para acceso de lectura. Esta es la configuración predeterminada.  
  
         READ_ONLY  
         Únicamente se permiten conexiones de solo lectura a las bases de datos secundarias de esta réplica. Todas las bases de datos secundarias están disponibles para acceso de lectura.  
  
         ALL  
         Se permiten todas las conexiones a las bases de datos secundarias de esta réplica, pero solo para acceso de lectura. Todas las bases de datos secundarias están disponibles para acceso de lectura.  
  
3.  Para configurar el acceso de conexión para el rol principal, en la cláusula ADD REPLICA o MODIFY REPLICA WITH, especifique la opción PRIMARY_ROLE, del siguiente modo:  
  
     PRIMARY_ROLE **(** ALLOW_CONNECTIONS **=** { READ_WRITE | ALL } **)**  
  
     donde,  
  
     READ_WRITE  
     No se permiten las conexiones en las que la propiedad de conexión Application Intent esté establecida en **ReadOnly** .  Cuando la propiedad Application Intent está establecida en **ReadWrite** o no tiene ningún valor, se permite la conexión. Para obtener más información sobre propiedad de conexión Application Intent, vea [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
     ALL  
     Se permiten todas las conexiones con las bases de datos de la réplica principal. Esta es la configuración predeterminada.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 En el siguiente ejemplo se agrega una réplica secundaria a un grupo de disponibilidad denominado *AG2*. Se especifica una instancia de servidor independiente, *COMPUTER03\HADR_INSTANCE*, para hospedar la nueva réplica de disponibilidad. Esta réplica configurada para permitir las conexiones de solo lectura-escritura para el rol principal y permitir las conexiones de solo intención de lectura para el rol secundario.  
  
```  
ALTER AVAILABILITY GROUP AG2   
   ADD REPLICA ON   
      'COMPUTER03\HADR_INSTANCE' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:7022',  
         PRIMARY_ROLE ( ALLOW_CONNECTIONS = READ_WRITE ),  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY )  
         );   
GO  
```  
  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para configurar el acceso en una réplica de disponibilidad**  
  
> [!NOTE]  
>  Para obtener un ejemplo de código, vea [Ejemplo (PowerShell)](#PSExample), más adelante en esta sección.  
  
1.  Cambie el directorio (`cd`) a la instancia de servidor que hospeda la réplica principal.  
  
2.  Para agregar una réplica de disponibilidad a un grupo de disponibilidad, use el cmdlet `New-SqlAvailabilityReplica`. Para modificar una réplica de disponibilidad existente, use el cmdlet `Set-SqlAvailabilityReplica`. Los parámetros pertinentes son los siguientes:  
  
    -   Para configurar el acceso de conexión para el rol secundario, especifique el `ConnectionModeInSecondaryRole` *palabra_clave_de_rol_secundario* parámetro, donde *palabra_clave_de_rol_secundario* es igual a uno de los siguientes valores:  
  
         `AllowNoConnections`  
         No se permiten conexiones directas con las bases de datos de la réplica secundaria y las bases de datos no están disponibles para acceso de lectura. Esta es la configuración predeterminada.  
  
         `AllowReadIntentConnectionsOnly`  
         Solo se permiten conexiones con las bases de datos de la réplica secundaria en las que la propiedad Application Intent está establecida en **ReadOnly**. Para obtener más información acerca de esta propiedad, vea [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         `AllowAllConnections`  
         Se permiten todas las conexiones con las bases de datos de la réplica secundaria para acceso de solo lectura.  
  
    -   Para configurar el acceso de conexión para el rol principal, especifique `ConnectionModeInPrimaryRole` *palabra_clave_de_rol_principal*, donde *palabra_clave_de_rol_principal* es igual a uno de los siguientes valores:  
  
         `AllowReadWriteConnections`  
         No se permiten las conexiones en las que la propiedad de conexión Application Intent esté establecida en ReadOnly. Cuando la propiedad Application Intent está establecida en ReadWrite o no tiene ningún valor, se permite la conexión. Para obtener más información sobre propiedad de conexión Application Intent, vea [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         `AllowAllConnections`  
         Se permiten todas las conexiones con las bases de datos de la réplica principal. Esta es la configuración predeterminada.  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet `Get-Help` en el entorno de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
###  <a name="PSExample"></a> Ejemplo (PowerShell)  
 En el siguiente ejemplo, los parámetros `ConnectionModeInSecondaryRole` y `ConnectionModeInPrimaryRole` se establecen en `AllowAllConnections`.  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
Set-SqlAvailabilityReplica -ConnectionModeInSecondaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ConnectionModeInPrimaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
  
```  
  
  
##  <a name="FollowUp"></a> Seguimiento: después de configurar el acceso de solo lectura para una réplica de disponibilidad  
 **Acceso de solo lectura a una réplica secundaria legible**  
  
-   Cuando se usa el [bcp (utilidad)](../../../tools/bcp-utility.md) o [utilidad sqlcmd](../../../tools/sqlcmd-utility.md), puede especificar el acceso de solo lectura a cualquier réplica secundaria que está habilitada para el acceso de solo lectura mediante el `-K ReadOnly` cambie.  
  
-   Para habilitar las aplicaciones cliente para conectarse a réplicas secundarias legibles:  
  
    ||Requisito previo|Vínculo|  
    |-|------------------|----------|  
    |![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Asegúrese de que el grupo de disponibilidad tiene un agente de escucha.|[Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
    |![Casilla](../../media/checkboxemptycenterxtraspacetopandright.gif "Casilla")|Configure el enrutamiento de solo lectura en un grupo de disponibilidad.|[Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)|  
  
 **Factores que podrían afectar a los desencadenadores y trabajos tras la conmutación por error**  
  
 Si tiene desencadenadores y trabajos que darán error al ejecutarse en una base de datos secundarias no legible o en una base de datos secundaria legible, tiene que escribir los desencadenadores y los trabajos para controlar una réplica dad y determinar si la base de datos es una base de datos principal o si es una base de datos secundaria legible. Para obtener esta información, use la función [DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql) para devolver la propiedad **Updatability** de la base de datos. Para identificar una base de datos de solo lectura, especifique READ_ONLY como el valor, según se indica a continuación:  
  
```  
DATABASEPROPERTYEX([db name],'Updatability') = N'READ_ONLY'  
```  
  
 Para identificar una base de datos de solo escritura, especifique READ_WRITE como el valor.  
  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [AlwaysOn: propuesta de valor de secundaria legible](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-value-proposition-of-readable-secondary.aspx)  
  
-   [AlwaysOn: ¿por qué hay dos opciones para habilitar una réplica secundaria para la carga de trabajo de lectura?](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-why-there-are-two-options-to-enable-a-secondary-replica-for-read-workload.aspx)  
  
-   [AlwaysOn: configuración de una réplica secundaria legible](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-setting-up-readable-seconary-replica.aspx)  
  
-   [AlwaysOn: acabo de habilitar una secundaria legible pero mi consulta está bloqueada](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-i-just-enabled-readble-secondary-but-my-query-is-blocked.aspx)  
  
-   [AlwaysOn: ofrecer las estadísticas más recientes de la secundaria legible, la base de datos de solo lectura y la instantánea de base de datos](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-making-upto-date-statistics-available-on-readable-secondary-read-only-database-and-database-snapshot.aspx)  
  
-   [AlwaysOn: desafíos de las estadísticas de la base de datos de solo lectura, la instantánea de base de datos y la réplica secundaria](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-challenges-with-statistics-on-readonly-database-database-snapshot-and-secondary-replica.aspx)  
  
-   [AlwaysOn: impacto sobre la carga de trabajo principal al ejecutar la carga de trabajo de informes en la réplica secundaria](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-impact-on-the-primary-workload-when-you-run-reporting-workload-on-the-secondary-replica.aspx)  
  
-   [AlwaysOn: efectos de asignar la carga de trabajo de informes de la secundaria legible al aislamiento de instantánea](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-impact-of-mapping-reporting-workload-to-snapshot-isolation-on-readable-secondary.aspx)  
  
-   [AlwaysOn: minimizar el bloqueo de subprocesos REDO al ejecutar la carga de trabajo de informes en la réplica secundaria](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-minimizing-blocking-of-redo-thread-when-running-reporting-workload-on-secondary-replica.aspx)  
  
-   [AlwaysOn: secundaria legible y latencia de datos](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson.aspx)  
  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Secundarias activas: Las réplicas secundarias legibles &#40;grupos de disponibilidad AlwaysOn&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)  
 [Acerca del acceso de conexión de cliente a réplicas de disponibilidad &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)  
  
  
