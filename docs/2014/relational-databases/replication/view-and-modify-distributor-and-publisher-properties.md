---
title: Ver y modificar las propiedades del distribuidor y del publicador | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- Distributors [SQL Server replication], modifying
- modifying replication properties, Distributors
- Distributors [SQL Server replication], properties
ms.assetid: 5dae1d59-c377-4c6e-adc9-b68c5b328f79
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4049cfa36020431e9cae8cbe2431c1c270d5deb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68212025"
---
# <a name="view-and-modify-distributor-and-publisher-properties"></a>Ver y modificar las propiedades del distribuidor y del publicador
  En este tema se describe cómo ver y modificar las propiedades del distribuidor y del publicador en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o Replication Management Objects (RMO).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para ver y modificar las propiedades del publicador y del distribuidor con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Para los publicadores que ejecutan versiones anteriores a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], un usuario del rol fijo de servidor **sysadmin** puede registrar suscriptores en la página **Suscriptores** . A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], ya no es necesario registrar explícitamente los suscriptores para la replicación.  
  
###  <a name="Security"></a> Seguridad  
 Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-view-and-modify-distributor-properties"></a>Para ver y modificar las propiedades del distribuidor  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y expanda el nodo de servidor.  
  
2.  Haga clic con el botón secundario en la carpeta **Replicación** y, a continuación, haga clic en **Propiedades del distribuidor**.  
  
3.  Vea y modifique las propiedades en el cuadro de diálogo **Propiedades del distribuidor: \<Distribuidor>** .  
  
    -   Para ver y modificar las propiedades de una base de datos de distribución, haga clic en el botón de propiedades ( **...** ) de la base de datos en la página **General** del cuadro de diálogo.  
  
    -   Para ver y modificar las propiedades del publicador asociado al distribuidor, haga clic en el botón de propiedades ( **...** ) del publicador en el cuadro de diálogo **publicador** .  
  
    -   Para obtener acceso a los perfiles de los agentes de replicación, haga clic en el botón **Valores predeterminados de perfil** de la página **General** del cuadro de diálogo. Para más información, consulte [Replication Agent Profiles](agents/replication-agent-profiles.md).  
  
    -   Para cambiar la contraseña de la cuenta utilizada cuando los procedimientos almacenados administrativos se ejecutan en el publicador y actualizar la información del distribuidor, escriba una contraseña nueva en los cuadros **Contraseña** y **Confirmar contraseña** de la página **Publicadores** del cuadro de diálogo. Para más información, vea [Proteger el distribuidor](security/secure-the-distributor.md).  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
#### <a name="to-view-and-modify-publisher-properties"></a>Para ver y modificar las propiedades del Publicador  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y luego expanda el nodo del servidor.  
  
2.  Haga clic con el botón secundario en la carpeta **Replicación** y, a continuación, haga clic en **Propiedades del publicador**.  
  
3.  Ver y modificar las propiedades en el **propiedades del publicador: \< Publisher >** cuadro de diálogo.  
  
    -   Un usuario del rol fijo de servidor **sysadmin** puede habilitar bases de datos de replicación en la página **Bases de datos de publicaciones** . Al habilitar una base de datos no se publica dicha base de datos, sino que permite que cualquier usuario del rol fijo de base de datos **db_owner** para esa base de datos cree una o varias publicaciones en la base de datos.  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Las propiedades del publicador y del distributor se pueden ver mediante programación usando procedimientos almacenados de replicación.  
  
#### <a name="to-view-distributor-and-distribution-database-properties"></a>Para ver las propiedades de la base de datos de distribución  
  
1.  Ejecute [sp_helpdistributor](/sql/relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql) para devolver información sobre el Distribuidor, la base de datos de distribución y el directorio de trabajo.  
  
2.  Ejecute [sp_helpdistributiondb](/sql/relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql) para devolver propiedades de una base de datos de distribución especificada.  
  
#### <a name="to-change-distributor-and-distribution-database-properties"></a>Para cambiar las propiedades de la base de datos de distribución y el distribuidor  
  
1.  En el distribuidor, ejecute [sp_changedistributor_property](/sql/relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql) para modificar las propiedades del distribuidor.  
  
2.  En el distribuidor, ejecute [sp_changedistributor_property](/sql/relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql) para modificar las propiedades del distribuidor.  
  
3.  En el distribuidor, ejecute [sp_changedistributor_password](/sql/relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql) para cambiar la contraseña del distribuidor.  
  
    > [!IMPORTANT]  
    >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
4.  En el distribuidor, ejecute [sp_changedistpublisher](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql) para cambiar las propiedades de un Publicador usando el Distribuidor.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 El siguiente script de [!INCLUDE[tsql](../../includes/tsql-md.md)] de ejemplo devuelve información acerca del Distribuidor y la base de datos de distribución.  
  
 [!code-sql[HowTo#sp_helpdistributor](../../snippets/tsql/SQL15/replication/howto/tsql/changedistpub.sql#sp_helpdistributor)]  
  
 [!code-sql[HowTo#sp_helpdistributiondb](../../snippets/tsql/SQL15/replication/howto/tsql/changedistpub.sql#sp_helpdistributiondb)]  
  
 Este ejemplo cambia los períodos de retención para el Distribuidor, la contraseña usada al conectar al Distribuidor y el intervalo en el que el Distribuidor comprueba el estado de distintos agentes de replicación (también conocido como intervalo de latidos).  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [!code-sql[HowTo#sp_changedistributor_property](../../snippets/tsql/SQL15/replication/howto/tsql/changedistpub.sql#sp_changedistributor_property)]  
  
 [!code-sql[HowTo#sp_changedistributiondb](../../snippets/tsql/SQL15/replication/howto/tsql/changedistpub.sql#sp_changedistributiondb)]  
  
 [!code-sql[HowTo#sp_changedistributor_password](../../snippets/tsql/SQL15/replication/howto/tsql/changedistpub.sql#sp_changedistributor_password)]  
  
##  <a name="RMOProcedure"></a> Uso de Replication Management Objects (RMO)  
  
#### <a name="to-view-and-modify-distributor-properties"></a>Para ver y modificar las propiedades del distribuidor  
  
1.  Cree una conexión al distribuidor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.ReplicationServer> . Pase el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1.  
  
3.  (Opcional) Compruebe la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationServer.IsDistributor%2A> para comprobar que el servidor conectado actualmente es un distribuidor.  
  
4.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> para recibir las propiedades del servidor.  
  
5.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para una o más de las propiedades del distribuidor que se pueden establecer en el objeto <xref:Microsoft.SqlServer.Replication.ReplicationServer> .  
  
6.  (Opcional) Si la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> del objeto <xref:Microsoft.SqlServer.Replication.ReplicationServer> está establecida en `true`, llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar los cambios en el servidor.  
  
#### <a name="to-view-and-modify-distribution-database-properties"></a>Para ver y modificar las propiedades de la base de datos de distribución  
  
1.  Cree una conexión al distribuidor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.DistributionDatabase> . Especifique la propiedad de nombre y pase el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1.  
  
3.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para recibir las propiedades del servidor. Si este método devuelve `false`, significa que la base de datos con el nombre especificado no existe en el servidor.  
  
4.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para una de las propiedades <xref:Microsoft.SqlServer.Replication.DistributionDatabase> que se pueden establecer.  
  
5.  (Opcional) Si la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> del objeto <xref:Microsoft.SqlServer.Replication.DistributionDatabase> está establecida en `true`, llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar los cambios en el servidor.  
  
#### <a name="to-view-and-modify-publisher-properties"></a>Para ver y modificar las propiedades del Publicador  
  
1.  Cree una conexión al publicador mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.DistributionPublisher> . Especifique la propiedad <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> y pase el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1.  
  
3.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para una de las propiedades <xref:Microsoft.SqlServer.Replication.DistributionPublisher> que se pueden establecer.  
  
4.  (Opcional) Si la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> del objeto <xref:Microsoft.SqlServer.Replication.DistributionPublisher> está establecida en `true`, llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar los cambios en el servidor.  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>Para cambiar la contraseña de la conexión administrativa del publicador al distribuidor  
  
1.  Cree una conexión al distribuidor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.ReplicationServer> .  
  
3.  Establezca la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> en la conexión creada en el paso 1.  
  
4.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> para obtener las propiedades del objeto.  
  
5.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A>. Pase el nuevo valor de contraseña para el parámetro *password* .  
  
    > [!IMPORTANT]  
    >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales, use los [servicios de cifrado](https://go.microsoft.com/fwlink/?LinkId=34733) (en inglés) proporcionados por [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
6.  (Opcional) Realice los pasos siguientes para cambiar la contraseña en cada publicador remoto que utilice este distribuidor:  
  
    1.  Cree una conexión al publicador mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
    2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.ReplicationServer> .  
  
    3.  Establezca la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> en la conexión creada en el paso 6a.  
  
    4.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> para obtener las propiedades del objeto.  
  
    5.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> . Pase el nuevo valor de contraseña del paso 5 para el parámetro *password* .  
  
###  <a name="PShellExample"></a> Ejemplo (RMO)  
 Este ejemplo muestra cómo cambiar las propiedades de Distribución y de la base de datos de distribución.  
  
> [!IMPORTANT]  
>  Para no almacenar las credenciales en el código, la nueva contraseña del distribuidor se proporciona en tiempo de ejecución.  
  
 [!code-csharp[HowTo#rmo_ChangeDistPub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changedistpub)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeDistPub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changedistpub)]  
  
## <a name="see-also"></a>Vea también  
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Disable Publishing and Distribution](disable-publishing-and-distribution.md)  (Deshabilitar la publicación y la distribución)  
 [Configurar distribución](configure-distribution.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Distributor and Publisher Information Script](administration/distributor-and-publisher-information-script.md)  (Script de información del distribuidor y del publicador)  
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)   
 [Visualización de información y realización de tareas mediante el Monitor de replicación](monitor/view-information-and-perform-tasks-replication-monitor.md)  
  
  
