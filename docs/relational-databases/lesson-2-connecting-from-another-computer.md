---
title: 'Lección 2: Conexión desde otro equipo | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: fd4ddeb8-0cb6-441b-9704-03575c07020f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0240c3e4f9f58bfb453e2537695631d8be3aa793
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073713"
---
# <a name="lesson-2-connecting-from-another-computer"></a>Lección 2: Conexión desde otro equipo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Para mejorar la seguridad, no se puede obtener acceso a [!INCLUDE[ssDE](../includes/ssde-md.md)] de las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer, Express y Evaluation desde otro equipo cuando se instala inicialmente. En esta lección se muestra cómo habilitar los protocolos, configurar los puertos y configurar el Firewall de Windows para conectarse desde otros equipos.  
  
Esta lección contiene las siguientes tareas:  
  
-   [Habilitar protocolos](#protocols)  
  
-   [Configurar un puerto fijo](#port)  
  
-   [Abrir puertos del firewall](#firewall)  
  
-   [Conectarse al motor de base de datos desde otro equipo](#otherComp)  
  
-   [Conectarse mediante el Servicio SQL Server Browser](#browser)  
  
## <a name="protocols"></a>Habilitar protocolos  
Para mejorar la seguridad, [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]Developer y Evaluation se instalan con conectividad de red limitada. Las conexiones a [!INCLUDE[ssDE](../includes/ssde-md.md)] se pueden realizar desde herramientas que se ejecuten en el mismo equipo, no desde otros equipos. Si tiene previsto realizar las tareas de desarrollo en el mismo equipo que [!INCLUDE[ssDE](../includes/ssde-md.md)], no necesita habilitar otros protocolos. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] se conectará a [!INCLUDE[ssDE](../includes/ssde-md.md)] mediante el protocolo de memoria compartida. Este protocolo ya está habilitado.  
  
Si tiene previsto conectarse a [!INCLUDE[ssDE](../includes/ssde-md.md)] desde otro equipo, debe habilitar un protocolo, como TCP/IP.  
  
#### <a name="how-to-enable-tcpip-connections-from-another-computer"></a>Cómo habilitar conexiones TCP/IP desde otro equipo  
  
1.  En el menú **Inicio** , elija **Todos los programas**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], **Herramientas de configuración**y, por último, **Administrador de configuración de SQL Server**.  
  
    > [!NOTE]  
    > Es posible que estén disponibles las opciones de 32 y 64 bits.  
  
    > [!NOTE]  
    > Como el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] es un complemento del programa [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console y no un programa independiente, el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no aparece como aplicación en las versiones más recientes de Windows. El nombre de archivo contiene un número que representa el número de versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para abrir el Administrador de configuración desde el comando Ejecutar, estas son las rutas de acceso a las últimas cuatro versiones si Windows está instalado en la unidad C:.  
  
    |||  
    |-|-|  
    |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|  
    |[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
    |[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|  
    |[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|C:\Windows\SysWOW64\SQLServerManager10.msc|  
  
2.  En **Administrador de configuración de SQL Server**, expanda **Configuración de red de SQL Server**y, después, haga clic en **Protocolos de** _<InstanceName>_ .  
  
    La instancia predeterminada (una instancia sin nombre) aparece como **MSSQLSERVER**. Si ha instalado una instancia con nombre, el nombre proporcionado aparece en la lista. [!INCLUDE[ssExpressEd11](../includes/ssexpressed11-md.md)] se instala como **SQLEXPRESS**, a menos que se haya cambiado el nombre durante la instalación.  
  
3.  En la lista de protocolos, haga clic con el botón derecho en el protocolo que quiera habilitar (**TCP/IP**) y luego haga clic en **Habilitar**.  
  
    > [!NOTE]  
    > Debe reiniciar el servicio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] después de realizar los cambios en los protocolos de red; sin embargo, esto se completa en la siguiente tarea.  

[!INCLUDE[fresh-note-steps-feedback](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="port"></a>Configurar un puerto fijo  
Para mejorar la seguridad, Windows Server 2008, [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]y Windows 7 activan el Firewall de Windows. Si desea conectarse a esta instancia desde otro equipo, debe abrir un puerto de comunicaciones en el firewall. La instancia predeterminada de [!INCLUDE[ssDE](../includes/ssde-md.md)] escucha en el puerto 1433; por tanto, no tiene que configurar un puerto fijo. No obstante, las instancias con nombre incluidas las de [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] escuchan en puertos dinámicos. Para poder abrir un puerto en el firewall, debe configurar primero [!INCLUDE[ssDE](../includes/ssde-md.md)] para que escuche en un puerto específico conocido como puerto fijo o estático; de lo contrario, es posible que [!INCLUDE[ssDE](../includes/ssde-md.md)] escuche en un puerto distinto cada vez que se inicie. Para obtener más información sobre firewalls, la configuración predeterminada de Firewall de Windows y una descripción de los puertos TCP que afectan al motor de base de datos, Analysis Services, Reporting Services e Integration Services, consulte [Configurar Firewall de Windows para permitir el acceso a SQL Server](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
> [!NOTE]  
> La Internet Assigned Numbers Authority administra las asignaciones del número de puerto, que se muestran en [https://www.iana.org](https://go.microsoft.com/fwlink/?LinkId=48844). Los números de puerto deben tener asignados números de 49152 a 65535.  
  
#### <a name="configure-sql-server-to-listen-on-a-specific-port"></a>Configurar SQL Server para escuchar en un puerto específico  
  
1.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , expanda **Configuración de red de SQL Server**y, a continuación, haga clic en la instancia de servidor que desee configurar.  
  
2.  En el panel derecho, haga doble clic en **TCP/IP**.  
  
3.  En el cuadro de diálogo **Propiedades de TCP/IP** , haga clic en la pestaña **Direcciones IP** .  
  
4.  En el cuadro **Puerto TCP** de la sección **IPAll** , escriba un número de puerto disponible. Para este tutorial, se utilizará **49172**.  
  
5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo y en **Aceptar** cuando aparezca una advertencia que indique que debe reiniciarse el servicio.  
  
6.  En el panel izquierdo, haga clic en **Servicios de SQL Server**.  
  
7.  En el panel derecho, haga clic con el botón derecho en la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]y, después, haga clic en **Reiniciar**. Cuando se reinicia [!INCLUDE[ssDE](../includes/ssde-md.md)] , escucha en el puerto **49172**.  
  
## <a name="firewall"></a>Abrir puertos del firewall  
Los sistemas de firewall ayudan a evitar el acceso no autorizado a los recursos de los equipos. Para conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] desde otro equipo cuando el firewall está activo, debe abrir un puerto en el firewall.  
  
> [!IMPORTANT]  
> El hecho de abrir puertos en el firewall puede dejar el servidor expuesto a ataques malintencionados. Asegúrese de que conoce los sistemas de firewall antes de abrir puertos. Para obtener más información, vea [Security Considerations for a SQL Server Installation](../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
Después de configurar [!INCLUDE[ssDE](../includes/ssde-md.md)] para utilizar un puerto fijo, siga estas instrucciones para abrir ese puerto en el Firewall de Windows. (No es necesario configurar un puerto fijo para la instancia predeterminada, porque ya está fijada en el puerto TCP 1433).  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access-windows-7"></a>Para abrir un puerto en el Firewall de Windows para el acceso TCP (Windows 7)  
  
1.  En el menú **Inicio** , haga clic en **Ejecutar**, escriba **WF.msc**y, a continuación, haga clic en **Aceptar**.  
  
2.  En la opción **Firewall de Windows con seguridad avanzada**del panel izquierdo, haga clic con el botón derecho en **Reglas de entrada**y luego haga clic en **Nueva regla** en el panel de acciones.  
  
3.  En el cuadro de diálogo **Tipo de regla** , seleccione **Puerto**y, a continuación, haga clic en **Siguiente**.  
  
4.  En el cuadro de diálogo **Protocolo y puertos** , seleccione **TCP**. Seleccione **Puertos locales específicos**y, a continuación, escriba el número de puerto de la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)]. Use 1433 para la instancia predeterminada. Escriba **49172** si está configurando una instancia con nombre y ha configurado un puerto fijo en la tarea anterior. Haga clic en **Siguiente**.  
  
5.  En el cuadro de diálogo **Acción** , seleccione **Permitir la conexión**y, a continuación, haga clic en **Siguiente**.  
  
6.  En el cuadro de diálogo **Perfil** , seleccione los perfiles que describan el entorno de conexión del equipo cuando desee conectarse a [!INCLUDE[ssDE](../includes/ssde-md.md)]y, a continuación, haga clic en **Siguiente**.  
  
7.  En el cuadro de diálogo **Nombre** , escriba un nombre y una descripción para esta regla. Después, haga clic en **Finalizar**.  
  
Para obtener más información sobre cómo configurar el firewall con instrucciones incluidas para [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)], consulte [Configurar Firewall de Windows para el acceso al motor de base de datos](../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md). Para obtener más información sobre la configuración predeterminada de Firewall de Windows y una descripción de los puertos TCP que afectan al motor de base de datos, Analysis Services, Reporting Services e Integration Services, vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="otherComp"></a>Conectarse al motor de base de datos desde otro equipo  
Ahora que ha configurado [!INCLUDE[ssDE](../includes/ssde-md.md)] para escuchar en un puerto fijo y ha abierto este puerto en el firewall, puede conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] desde otro equipo.  
  
Cuando el servicio Explorador de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se ejecute en el equipo servidor y el firewall haya abierto el puerto UDP 1434, la conexión se podrá realizar utilizando el nombre del equipo y el nombre de la instancia. Para mejorar la seguridad, el ejemplo no utiliza el servicio Explorador de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
#### <a name="to-connect-to-the-database-engine-from-another-computer"></a>Para conectarse al motor de base de datos desde otro equipo  
  
1.  En un segundo equipo que incluya las herramientas de cliente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , inicie una sesión con una cuenta autorizada para conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]y abra [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
2.  En el cuadro de diálogo **Conectar al servidor** , confirme **Motor de base de datos** en el cuadro **Tipo de servidor** .  
  
3.  En el cuadro **Nombre del servidor** , escriba **tcp:** para especificar el protocolo, seguido del nombre del equipo, una coma y el número de puerto. Para conectarse a la instancia predeterminada, el puerto 1433 está implícito y se puede omitir, por lo que deberá escribir **tcp:** _<nombre_equipo>_ . En nuestro ejemplo de una instancia con nombre, escriba **tcp:** _<nombre_equipo>_ **,49172**.  
  
    > [!NOTE]  
    > Si omite **tcp:** en el cuadro **Nombre del servidor**, el cliente probará todos los protocolos habilitados en el orden especificado en la configuración del cliente.  
  
4.  En el cuadro **Autenticación** , confirme **Autenticación de Windows**y luego haga clic en **Conectar**.  
  
## <a name="browser"></a>Conectarse mediante el Servicio SQL Server Browser  
El servicio Explorador de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] escucha las solicitudes entrantes de recursos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y proporciona información acerca de las instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instaladas en el equipo. Cuando el servicio Explorador de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se está ejecutando, los usuarios se pueden conectar a instancias con nombre si proporcionan el nombre del equipo y el de la instancia, en lugar del nombre del equipo y el número de puerto. Puesto que el Explorador de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] recibe solicitudes UDP no autenticadas, no está activado siempre durante la instalación. Para obtener una descripción del servicio y una explicación de cuándo está activado, consulte [Servicio SQL Server Browser &#40;motor de base de datos y SSAS&#41;](../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md).  
  
Para usar el Explorador de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , debe seguir los mismos pasos que en la tarea anterior y abrir el puerto UDP 1434 en el firewall.  
  
Con esto finaliza este breve tutorial sobre la conectividad básica.  
  
## <a name="return-to-tutorials-portal"></a>Volver al portal de tutoriales  
[Tutorial: Introducción al motor de base de datos](../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  

