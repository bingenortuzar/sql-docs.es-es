---
title: Usar el Asistente para agregar una réplica al grupo de disponibilidad (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.addreplicawizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], wizards
ms.assetid: 60d962b6-2af4-4394-9190-61939a102bc0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7a9074c49b3e8c9d80666d3bb586ffeba225e88b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813382"
---
# <a name="use-the-add-replica-to-availability-group-wizard-sql-server-management-studio"></a>Usar el Asistente para agregar una réplica al grupo de disponibilidad (SQL Server Management Studio)
  Use el Asistente para agregar una réplica al grupo de disponibilidad como ayuda para agregar una nueva réplica secundaria a un grupo de disponibilidad AlwaysOn existente.  
  
> [!NOTE]  
>  Para obtener información sobre cómo usar [!INCLUDE[tsql](../../../includes/tsql-md.md)] o PowerShell para agregar una réplica secundaria a un grupo de disponibilidad, vea [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md).  
  

  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
 Si nunca ha agregado una réplica de disponibilidad a un grupo de disponibilidad, consulte la "Instancias del servidor" y "grupos de disponibilidad y réplicas" secciones en [requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Debe estar conectado a la instancia del servidor que hospeda la réplica principal actual.  
  
-   Antes de agregar una réplica secundaria, compruebe que la instancia del host de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está en el mismo clúster de clústeres de conmutación por error de Windows Server (WSFC) que las réplicas existentes pero reside en otro nodo de clúster. Además, compruebe que esta instancia de servidor cumple los requisitos previos de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Para más información, vea [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Si una instancia de servidor seleccionada para hospedar una réplica de disponibilidad se ejecuta bajo una cuenta de usuario de dominio y no tiene todavía un extremo de creación de reflejo de la base de datos, el asistente puede crear el extremo y conceder el permiso CONNECT a la cuenta de servicio de la instancia de servidor. Sin embargo, si el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se ejecuta como una cuenta integrada (como sistema local, servicio local o servicio de red), o una cuenta que no es de dominio, debe usar certificados para la autenticación de extremos y el asistente no podrá crear un extremo de creación de reflejo de la base de datos en la instancia de servidor. En este caso, se recomienda crear los extremos de creación de reflejo de la base de datos manualmente antes de iniciar el asistente Agregar réplica al grupo de disponibilidad.  
  
     `To use certificates for a database mirroring endpoint:`  
  
     [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
     [Usar certificados para un punto de conexión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   **Requisitos previos para usar la sincronización de datos inicial completa**  
  
    -   Todas las rutas de acceso de archivos de base de datos deben ser idénticas en todas las instancias de servidor que hospedan una réplica para el grupo de disponibilidad.  
  
    -   Ningún nombre de base de datos principal puede existir en ninguna instancia de servidor que hospede una réplica secundaria. Esto significa que ninguna de las nuevas bases de datos secundarias puede existir todavía.  
  
    -   Tendrá que especificar un recurso compartido de red para que el asistente cree y obtenga acceso a las copias de seguridad. Para la réplica principal, la cuenta usada para iniciar el [!INCLUDE[ssDE](../../../includes/ssde-md.md)] debe tener permisos del sistema de archivos de lectura y escritura en un recurso compartido de red. Para las réplicas secundarias, la cuenta debe tener permiso de lectura en el recurso compartido de red.  
  
     Si no puede utilizar el asistente para realizar la sincronización de datos inicial completa, debe preparar las bases de datos secundarias manualmente. Puede hacerlo antes o después de ejecutar el asistente. Para obtener más información, vea [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
 También se necesita el permiso CONTROL ON ENDPOINT si desea permitir que el asistente Agregar réplica a grupo de disponibilidad administre el extremo de creación de reflejo de la base de datos.  
  

  
##  <a name="SSMSProcedure"></a> Usar el Asistente para agregar una réplica al grupo de disponibilidad (SQL Server Management Studio)  
 **Para usar el Asistente para agregar una réplica al grupo de disponibilidad**  
  
1.  En el Explorador de objetos, conéctese a la instancia del servidor que hospeda la réplica principal del grupo de disponibilidad y expanda el árbol.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Haga clic con el botón secundario en el grupo de disponibilidad al que está agregando una réplica secundaria y seleccione el comando **Agregar réplica** . Esto inicia el Asistente para agregar una réplica al grupo de disponibilidad.  
  
4.  En la página **Conectar con réplicas secundarias existentes** , conéctese a cada réplica secundaria del grupo de disponibilidad. Para obtener más información, consulte [conectarse a la página réplicas secundarias existentes &#40;Agregar réplica y el Asistente para agregar las bases de datos&#41;](connect-to-existing-secondary-replicas-page.md).  
  
5.  En la página **Especificar réplicas** , especifique y configure una o varias réplicas secundarias nuevas para el grupo de disponibilidad. Esta página contiene tres pestañas: En la siguiente tabla se presentan estas pestañas. Para más información, vea [Página Especificar réplicas &#40;Asistente para nuevo grupo de disponibilidad: Asistente para agregar réplica&#41;](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md).  
  
    |Pestaña|Descripción breve|  
    |---------|-----------------------|  
    |**Réplicas**|Utilice esta pestaña para especificar cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedará una nueva réplica secundaria.|  
    |**Extremos**|Utilice esta pestaña para comprobar el extremo de creación de reflejo de la base de datos existente, si existe, para cada nueva réplica secundaria. Si este extremo no está en una instancia de servidor cuyas cuentas de servicio utilizan la autenticación de Windows, el asistente intentará crear el extremo automáticamente. **Nota:**  Si cualquier instancia de servidor se está ejecutando bajo una cuenta de usuario que no sea de dominio, deberá realizar un cambio manual a la instancia del servidor antes de continuar en el asistente. Para obtener más información, vea [Requisitos previos](#Prerequisites), anteriormente en este tema.|  
    |**Preferencias de copia de seguridad**|Utilice esta pestaña para especificar sus preferencias de copias de seguridad para el grupo de disponibilidad en conjunto, si desea modificar la configuración actual, y las prioridades de copias de seguridad para las réplicas de disponibilidad individuales.|  
  
6.  En la página **Seleccionar sincronización de datos iniciales** , elija cómo desea que las nuevas bases de datos secundarias se creen y se unan al grupo de disponibilidad. Elija una de las opciones siguientes:  
  
    -   **Completa**  
  
         Seleccione esta opción si el entorno cumple los requisitos para iniciar automáticamente la sincronización de datos iniciales (para obtener más información, vea [Requisitos previos, restricciones y recomendaciones](#Prerequisites), anteriormente en este tema).  
  
         Si selecciona **Completa**, después de crear el grupo de disponibilidad, el asistente realizará una copia de seguridad de cada base de datos principal y su registro de transacciones a un recurso compartido de red y restaurará las copias de seguridad en cada instancia de servidor que hospeda una nueva réplica secundaria. El asistente unirá entonces cada base de datos secundaria nueva al grupo de disponibilidad.  
  
         En el campo **Especificar una ubicación de red compartida accesible por todas las réplicas:** , especifique un recurso compartido de copia de seguridad al que todas las instancias del servidor que hospedan réplicas tengan acceso de lectura/escritura. Las copias de seguridad de registros serán parte de la cadena de copias de seguridad de registros. Almacene adecuadamente los archivos de copia de seguridad del registro.  
  
        > [!IMPORTANT]  
        >  Para obtener información sobre los permisos necesarios del sistema de archivos, vea [Requisitos previos](#Prerequisites), anteriormente en este tema.  
  
    -   **Solo unión**  
  
         Si ha preparado manualmente las bases de datos secundarias de las instancias de servidor que hospedarán las nuevas réplicas secundarias, puede seleccionar esta opción. El asistente unirá estas bases de datos secundarias nuevas al grupo de disponibilidad.  
  
    -   **Omitir la sincronización de datos iniciales**  
  
         Seleccione esta opción si desea usar sus propias bases de datos y copias de seguridad de registros de sus bases de datos principales. Para más información, vea [Iniciar el movimiento de datos en una base de datos secundaria AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
7.  La página **Validación** comprueba si los valores especificados en el asistente cumplen los requisitos del Asistente para agregar una réplica al grupo de disponibilidad. Para realizar un cambio, haga clic en **Anterior** para volver a una página anterior del asistente con el fin de cambiar uno o varios valores. Haga clic en **Siguiente** para volver a la página **Validación** y haga clic en **Volver a ejecutar la validación**.  
  
8.  En la página **Resumen** , revise las opciones para el nuevo grupo de disponibilidad. Para realizar un cambio, haga clic en **Anterior** para volver a la página correspondiente. Después de realizar el cambio, haga clic en **Siguiente** para volver a la página **Resumen** .  
  
     Si está satisfecho con las selecciones, puede hacer si lo desea en Script para crear un script de los pasos que ejecutará el asistente. A continuación, para crear y configurar el nuevo grupo de disponibilidad, haga clic en **Finalizar**.  
  
9. En la página **Progreso** se muestra el progreso de los pasos necesarios para crear el grupo de disponibilidad (configuración de puntos de conexión, creación del grupo de disponibilidad y unión de la réplica secundaria al grupo).  
  
10. Según se completen estos pasos, la página **Resultados** mostrará el resultado de cada paso. Si todos estos pasos se realizan correctamente, el nuevo grupo de disponibilidad se configura por completo. Si alguno de los pasos produce un error, puede que tenga que completar manualmente la configuración. Para obtener información sobre la causa de un error determinado, haga clic en el vínculo “Error” asociado de la columna **Resultado** .  
  
     Una vez completado el asistente, haga clic en **Cerrar** para salir.  
  
> [!IMPORTANT]  
>  Después de agregar una réplica, vea la sección "Seguimiento: después de agregar una réplica secundaria" en [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md).  
  

  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  

  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
