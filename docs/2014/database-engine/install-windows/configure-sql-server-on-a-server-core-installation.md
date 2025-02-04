---
title: Configurar SQL Server en una instalación Server Core | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- IsHadrEnabled server property
- Server Core Installation [SQL Server]
ms.assetid: ed6e5e94-4b8d-422a-a17e-61b05a4df903
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8134b7a69df7254ce3609ddce24a15293c47efd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779738"
---
# <a name="configure-sql-server-on-a-server-core-installation"></a>Configurar SQL Server en una instalación Server Core
  En este tema se trata información detallada sobre la configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una instalación Server Core de [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1. 
  
##  <a name="configure-and-manage-server-core-on-windows-server"></a>Configurar y administrar Server Core en Windows Server  
 La sección proporciona referencias a los temas de ayuda para configurar y administrar una instalación de Server Core.  
  
 No todas las características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] son compatibles con el modo Server Core.  Algunas de estas características se pueden instalar en un equipo cliente o en otro servidor que no ejecute Server Core, y conectarse a los servicios de motor de base de datos instalados en Server Core.  
  
 Para obtener más información sobre la configuración y administración remota de una instalación de Server Core, vea los temas siguientes:  
  
-   [Windows Server 2008 R2: Procedimientos recomendados para las implementaciones de Server Core](https://go.microsoft.com/fwlink/?LinkID=245957) (https://go.microsoft.com/fwlink/?LinkID=245957)  
  
-   [Configurar una instalación Server Core: Información general sobre](https://go.microsoft.com/fwlink/?LinkId=245958) (https://go.microsoft.com/fwlink/?LinkId=245958)  
  
-   [Configuración de una instalación Server Core de Windows Server 2008 R2 con Sconfig.cmd](https://go.microsoft.com/fwlink/?LinkId=245959) (https://go.microsoft.com/fwlink/?LinkId=245959)  
  
-   [Instalar un rol de servidor en un servidor que ejecuta una instalación Server Core de Windows Server 2008 R2: Información general sobre](https://go.microsoft.com/fwlink/?LinkId=245960) (https://go.microsoft.com/fwlink/?LinkId=245960)  
  
-   [Instalar características de Windows en un servidor que ejecuta una instalación Server Core de Windows Server 2008 R2: Información general sobre](https://go.microsoft.com/fwlink/?LinkId=245961) (https://go.microsoft.com/fwlink/?LinkId=245961)  
  
-   [Administración de una instalación de Server Core: Información general sobre](https://go.microsoft.com/fwlink/?LinkId=245962) (https://go.microsoft.com/fwlink/?LinkId=245962)  
  
-   [Administración de una instalación Server Core](https://go.microsoft.com/fwlink/?LinkId=245963) (https://go.microsoft.com/fwlink/?LinkId=245963)  
  
##  <a name="install-updates"></a>Instalar actualizaciones  
 En esta sección se proporciona información sobre la instalación de actualizaciones para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en un equipo con Windows Server Core. Se recomienda que los clientes evalúen e instalen las últimas actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puntualmente para asegurarse de que los sistemas están al día con las actualizaciones de seguridad más recientes. Para obtener más información acerca de cómo instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en un equipo Windows Server Core, vea [instalar SQL Server 2014 en Server Core](install-sql-server-on-server-core.md).  
  
 Los siguientes son los dos escenarios para la instalación de actualizaciones del producto:  
  
-   [Instalar actualizaciones para SQL Server 2014 durante una instalación nueva](#installing-updates-during-a-new-installation) 
  
-   [Instalar actualizaciones para SQL Server 2014 después de que se ha instalado](#installing-updates-after-installation) 
  
### <a name="installing-updates-during-a-new-installation"></a>Instalar las actualizaciones durante una instalación nueva  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite solo instalaciones del símbolo del sistema en el sistema operativo Server Core. Para obtener más información, vea [Instalar SQL Server 2014 desde el símbolo del sistema](install-sql-server-from-the-command-prompt.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integra las últimas actualizaciones del producto con la instalación del producto principal, de modo que el producto principal y las actualizaciones aplicables se instalen al mismo tiempo.  
  
 Una vez que el programa de instalación encuentra las versiones más recientes de las actualizaciones aplicables, las descarga y las integra con el proceso de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actual. La actualización del producto puede extraer una actualización acumulativa, un Service Pack o un Service Pack más la actualización acumulativa.  
  
 Especifique los parámetros UpdateEnabled y UpdateSource para incluir las últimas actualizaciones del producto con la instalación principal del producto. Consulte el ejemplo siguiente para habilitar las actualizaciones de producto durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
```sql  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /UpdateEnabled=True /UpdateSource="<SourcePath>" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
### <a name="installing-updates-after-installation"></a>Instalación de actualizaciones después de la instalación 
 En una instancia instalada de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], se recomienda aplicar las actualizaciones de seguridad y actualizaciones críticas más recientes, incluidas las versiones generales de distribución (GDR) y los Service Pack (SP). Las actualizaciones acumulativas individuales y las actualizaciones de seguridad deben adoptarse en cada caso, 'según convenga'. Evalúe la actualización; si es necesario y aplíquela luego.  
  
 Aplique una actualización en una línea de comandos y reemplace <nombre_paquete> por el nombre del paquete de actualización:  
  
-   Actualice una única instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y todos los componentes compartidos. Puede especificar la instancia mediante el parámetro InstanceName o InstanceID.  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance  
    ```  
  
-   Actualice solo los componentes compartidos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
    ```  
  
-   Actualice todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo y todos los componentes compartidos:  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances  
    ```  
  
##  <a name="startstop-sql-server-service"></a>Servicio de inicio y detención de SQL Server  
 La aplicación [sqlservr](../../tools/sqlservr-application.md) se inicia, se detiene, se pone en pausa y continúa una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un símbolo del sistema.  
  
 También puede usar los servicios Net para iniciar y detener los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="enable-alwayson-availability-groups"></a>Habilitar los grupos de disponibilidad de AlwaysOn  
 Al estar habilitado para los Grupos de disponibilidad de AlwaysOn es un requisito previo para que una instancia de servidor use los grupos de disponibilidad como solución de alta disponibilidad y recuperación ante desastres. Para obtener más información sobre cómo administrar los Grupos de disponibilidad AlwaysOn, vea [Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
### <a name="using-sql-server-configuration-manager-remotely"></a>Usar Administrador de configuración de SQL Server de forma remota  
 Estos pasos están pensados para realizarse en un equipo que ejecuta la edición del cliente de [!INCLUDE[win7](../../includes/win7-md.md)] o posterior, o en otro servidor que tiene instalado el Shell gráfico de servidor (es decir, una instalación completa de [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] o una instalación de Windows Server 8 con la característica Shell gráfico de servidor habilitada).  
  
1.  Abra Administración de equipos. Para abrir Administración de equipos, realice una de las acciones siguientes:  
  
    1.  En [!INCLUDE[win7](../../includes/win7-md.md)], Windows Server 2008 o [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]:  
  
        1.  Haga clic en Iniciar, Todos los programas, Herramientas administrativas y, a continuación, haga clic en Administración de equipos.  
  
        2.  Haga clic en Iniciar, Ejecutar, escriba COMPMGMT.MSC y, a continuación, haga clic en Aceptar.  
  
    2.  En Windows 8 con el shell gráfico de servidor habilitado:  
  
        1.  Mueva el mouse a la esquina inferior izquierda de la pantalla y haga clic con el botón secundario cuando aparezca el icono superpuesto Iniciar.  
  
        2.  Seleccione Administración de equipos en el menú contextual.  
  
2.  En el árbol de consola, haga clic con el botón secundario en Administración de equipos y, a continuación, haga clic en Conectar con otro equipo.  
  
3.  En el cuadro de diálogo Seleccionar equipo, escriba el nombre del equipo con Server Core que desee administrar o haga clic en Examinar para buscarlo y, a continuación, haga clic en Aceptar.  
  
4.  En el árbol de consola, debajo de Administración de equipos del equipo con Server Core, haga clic en Servicios y Aplicaciones.  
  
5.  Haga doble clic en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
6.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, haga clic en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicios, haga clic en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (\<nombre de instancia >), donde \<nombre de instancia > es el nombre de una instancia del servidor local para el que desea habilitar AlwaysOn Grupos de disponibilidad y haga clic en Propiedades.  
  
7.  Seleccione la pestaña Alta disponibilidad de AlwaysOn.  
  
8.  Compruebe que el campo Nombre del clúster de conmutación por error de Windows contiene el nombre del nodo de clúster de conmutación por error local. Si el campo está en blanco, esta instancia de servidor no admite actualmente los grupos de disponibilidad de AlwaysOn. Puede ser que el equipo local no sea un nodo de clúster, que se haya cerrado el clúster de WSFC o que esta edición de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no admita los Grupos de disponibilidad de AlwaysOn.  
  
9. Active la casilla Habilitar los grupos de disponibilidad de AlwaysOn y haga clic en Aceptar.  
  
10. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] guarda el cambio. A continuación, debe reiniciarse manualmente el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esto le permite elegir una hora de reinicio que sea la mejor para sus requisitos empresariales. Al reiniciar el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , AlwaysOn se habilitará y la propiedad del servidor IsHadrEnabled se establecerá en 1.  
  
> [!NOTE]
>  -   Deberá tener los derechos de usuario adecuados o se le deberá haber delegado la autoridad adecuada en el equipo de destino para conectarse a ese equipo.  
> -   El nombre del equipo que está administrando se mostrará entre paréntesis junto a Administración de equipos en el árbol de consola.  
  
### <a name="using-powershell-cmdlets-to-enable-alwayson-availability-groups"></a>Usar cmdlets de PowerShell para habilitar los Grupos de disponibilidad AlwaysOn  
 El cmdlet de PowerShell, Enable-SqlAlwaysOn, se usa para habilitar el grupo de disponibilidad de AlwaysOn en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si Grupos de disponibilidad de AlwaysOn está habilitado mientras se ejecuta el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el servicio Motor de base de datos debe reiniciarse para que el cambio se complete. A menos que especifique el parámetro -Force, el cmdlet le pide que indique si desea reiniciar el servicio; si se cancela, no se produce ninguna operación.  
  
 Debe tener permiso de administrador para ejecutar este cmdlet.  
  
 Puede usar una de las sintaxis siguientes para habilitar los grupos de disponibilidad de AlwaysOn en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
Enable-SqlAlwaysOn [-Path <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn -InputObject <Server> [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn [-ServerInstance <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
 El comando siguiente de PowerShell habilita los grupos de disponibilidad de AlwaysOn en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Equipo\Instancia):  
  
```  
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Machine\Instance  
```  
  
## <a name="configuring-remote-access-of-sql-server-running-on-server-core"></a>Configurar el acceso remoto de SQL Server que se ejecuta en Server Core  
 Realice las acciones descritas a continuación para configurar el acceso remoto de una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que se está ejecutando en [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1.  
  
### <a name="enable-remote-connections-on-an-instance-of-sql-server"></a>Habilitar conexiones remotas en una instancia de SQL Server 
 Para habilitar las conexiones remotas, use SQLCMD.exe localmente y ejecute las instrucciones siguientes en la instancia de Server Core:  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-sql-server-browser-service"></a>Habilitar e iniciar el servicio SQL Server Browser  
 De forma predeterminada, el servicio Explorer se deshabilita.  Si se deshabilita en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta en Server Core, ejecute el siguiente comando desde el símbolo del sistema para habilitarlo:  
  
 `sc config SQLBROWSER start= auto`  
  
 Una vez habilitado, ejecute el siguiente comando desde el símbolo del sistema para iniciar el servicio:  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Crear excepciones en Firewall de Windows  
 Para crear excepciones para el acceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Firewall de Windows, siga los pasos especificados en [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
### <a name="enable-tcpip-on-an-instance-of-sql-server"></a>Habilite TCP/IP en una instancia de SQL Server
 El protocolo TCP/IP puede habilitarse a través de Windows PowerShell para una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Server Core. Siga estos pasos:  
  
1.  En el equipo que ejecuta Windows Server 2008 R2 Server Core SP1, inicie el Administrador de tareas.  
  
2.  En la pestaña **Aplicaciones** , haga clic en **Nueva tarea**.  
  
3.  En el cuadro de diálogo **Crear nueva tarea** , escriba **sqlps.exe** en el campo **Abrir** y, a continuación, haga clic en **Aceptar**. De este modo, se abre la ventana **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell**.  
  
4.  En la ventana **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell**, ejecute el siguiente script para habilitar el protocolo TCP/IP:  
  
```  
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = new-object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
##  <a name="sql-server-profiler"></a>SQL Server Profiler  
 En un equipo remoto, inicie [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] y seleccione Nuevo seguimiento en el menú Archivo; la aplicación muestra un cuadro de diálogo Conectar al servidor en el que se puede especificar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que se desea conectarse, que reside en el equipo con Server Core. Para obtener más información, vea [Start SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md).  
  
 Para obtener más información sobre los permisos necesarios para ejecutar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], vea [Permisos necesarios para ejecutar SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
 Para conocer más detalles sobre [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], vea [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md).  
  
##  <a name="sql-server-auditing"></a>Auditoría de SQL Server  
 Puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] de forma remota para definir una auditoría. Una vez creada y habilitada la auditoría, el destino comenzará a recibir entradas. Para obtener más información sobre cómo crear y administrar auditorías de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [SQL Server Audit &#40;motor de base de datos&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
##  <a name="sql-servevr-command-prompt-utilities"></a>Utilidades de símbolo del sistema de Servevr comando SQL  
 Puede usar las siguientes utilidades del símbolo del sistema que le permiten crear scripts de operaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo con Server Core. La siguiente tabla contiene una lista de utilidades de símbolo del sistema que se suministran junto con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Server Core:  
  
|**Utilidad**|**Descripción**|**Instalada en**|  
|-----------------|---------------------|----------------------|  
|[bcp (utilidad)](../../tools/bcp-utility.md)|Se usa para copiar datos entre una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un archivo de datos en un formato especificado por el usuario.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec (utilidad)](../../integration-services/packages/dtexec-utility.md)|Se usa para configurar y ejecutar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil (utilidad)](../../integration-services/dtutil-utility.md)|Se usa para administrar paquetes SSIS.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[osql (utilidad)](../../tools/osql-utility.md)|Permite especificar instrucciones, procedimientos del sistema y archivos de scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el símbolo del sistema.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 (aplicación)](../../tools/sqlagent90-application.md)|Se usa para iniciar el Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un símbolo del sistema.|\<unidad>:\Archivos de programa\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*nombre_instancia*>\MSSQL\Binn|  
|[sqlcmd Utility](../../tools/sqlcmd-utility.md)|Permite especificar instrucciones, procedimientos del sistema y archivos de scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el símbolo del sistema.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SQLdiag (utilidad)](../../tools/sqldiag-utility.md)|Se usa para recopilar información de diagnóstico para el Servicio de soporte y atención al cliente de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint (utilidad)](../../tools/sqlmaint-utility.md)|Se usa para ejecutar los planes de mantenimiento de bases de datos creados en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|\<unidad >: \Program archivos\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. MSSQLSERVER\MSSQL\Binn|  
|[Utilidad sqlps](../../tools/sqlps-utility.md)|Se usa para ejecutar comandos y scripts de PowerShell. Carga y registra el proveedor de PowerShell de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los cmdlets.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr](../../tools/sqlservr-application.md)|Se usa para iniciar y detener una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] desde el símbolo del sistema para solucionar problemas.|\<unidad >: \Program archivos\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. MSSQLSERVER\MSSQL\Binn|  
  
##  <a name="use-troubleshooting-tools"></a>Usar herramientas para la solución de problemas  
 Puede usar [SQLdiag Utility](../../tools/sqldiag-utility.md) para recopilar los archivos de datos y de registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y otros tipos de servidores, y para supervisar los servidores a lo largo del tiempo o solucionar problemas específicos de los mismos. SQLdiag tiene como fin acelerar y simplificar la recopilación de información de diagnóstico para los Servicios de soporte técnico de Microsoft.  
  
 Puede iniciar la utilidad en el símbolo del sistema de administrador en Server Core, mediante la sintaxis especificada en el tema: [SQLdiag (utilidad)](../../tools/sqldiag-utility.md).  
  
## <a name="see-also"></a>Vea también  
 [Instalar a SQL Server 2014 en Server Core](install-sql-server-on-server-core.md)   
 [Temas de procedimientos de instalación](../../sql-server/install/installation-how-to-topics.md)  
  
  
