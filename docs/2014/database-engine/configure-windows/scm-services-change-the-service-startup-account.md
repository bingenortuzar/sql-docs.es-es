---
title: Cambiar la cuenta de inicio de servicio para SQL Server (Administrador de configuración de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server services, startup account changes
- startup accounts [SQL Server]
- changing startup accounts for services
ms.assetid: d721c796-0397-46a7-901b-1a9a3c3fb385
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a2a830ad4d6fa87cd754910baf8be53216086cab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62810446"
---
# <a name="change-the-service-startup-account-for-sql-server-sql-server-configuration-manager"></a>Cambiar la cuenta de inicio del servicio para SQL Server (Administrador de configuración de SQL Server)
  En este tema se describe cómo usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cambiar las opciones de inicio de los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las cuentas de servicio usadas por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o PowerShell. Para obtener más información sobre cómo seleccionar la cuenta de servicio adecuada, vea [Configurar los permisos y las cuentas de servicio de Windows](configure-windows-service-accounts-and-permissions.md).  
  
> [!IMPORTANT]  
>  Cuando cambie la cuenta de inicio del servicio para [!INCLUDE[ssDE](../../includes/ssde-md.md)] y el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssDE](../../includes/ssde-md.md)]) debe reiniciarse para que se aplique el cambio. Cuando se reinicia el servicio, todas las bases de datos asociadas a dicha instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no estarán disponibles hasta que se reinicie el servicio correctamente. Si tiene que cambiar la cuenta de inicio del servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], asegúrese de que lo hace durante el mantenimiento programado o cuando se pueden poner las bases de datos sin conexión sin interrumpir las operaciones diarias.  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Servidores en clúster  
  
     El cambio de la cuenta de servicio usada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe realizarse desde el nodo activo del clúster de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Cuando se ejecuta en Windows Server 2008 (en una configuración no predeterminada que usa grupos de dominio), el cambio de la cuenta de servicio usada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere que el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detenga [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poniendo los grupos de recursos en modo sin conexión.  
  
-   Actualización de SKU (de[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] a SKU no Express)  
  
     Durante la instalación de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se configura para usar la cuenta Servicio de red, pero está deshabilitado. El Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede cambiar la cuenta asignada para el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero el servicio no se puede habilitar ni iniciar. Después de la actualización de SKU de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] a no Express, el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se habilita automáticamente, pero se puede habilitar cuando sea necesario usando el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cambiando el modo de inicio del servicio a Manual o Automático.  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-change-the-sql-server-service-startup-account"></a>Para cambiar la cuenta de inicio del servicio de SQL Server  
  
1.  En el menú **Inicio** , elija **Todos los programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Herramientas de configuración**y, por último, **Administrador de configuración de SQL Server**.  
  
    > [!NOTE]  
    >  Como el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un complemento del programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console y no un programa independiente, el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aparece como aplicación en las versiones más recientes de Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, en el **página de inicio**, escriba SQLServerManager12.msc (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). Para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , reemplace el 12 por un número inferior. Haga clic en SQLServerManager12.msc abrir el Administrador de configuración. Para anclar el Administrador de configuración a la página de inicio o la barra de tareas, haga clic en SQLServerManager12.msc y, a continuación, haga clic en **Abrir ubicación del archivo**. En el Explorador de archivos de Windows, haga clic en SQLServerManager12.msc y, a continuación, haga clic en **anclar a inicio** o **anclar a la barra de tareas**.  
    > -   **Windows 8**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, en el **búsqueda** acceso a **aplicaciones**, tipo **SQLServerManager\<versión > .msc** como `SQLServerManager12.msc`y, a continuación, presione **ENTRAR**.  
  
2.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en **Servicios de SQL Server**.  
  
3.  En el panel de detalles, haga clic con el botón derecho en el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la que quiera cambiar la cuenta de inicio del servicio y, después, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de \<***nombredeinstancia***> de SQL Server**, haga clic en la pestaña **Iniciar sesión** y seleccione un tipo de cuenta **Iniciar sesión como**.  
  
5.  Tras seleccionar la nueva cuenta de inicio de servicio, haga clic en **Aceptar**.  
  
     Un cuadro de mensaje le pregunta si desea reiniciar el servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
6.  Haga clic en **Sí**y, a continuación, cierre el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](start-stop-pause-resume-restart-sql-server-services.md)   
 [Configurar WMI para mostrar el estado del servidor en Herramientas de SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
