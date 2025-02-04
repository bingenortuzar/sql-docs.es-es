---
title: Configurar los permisos y las cuentas de servicio de Windows | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- startup service states [SQL Server]
- Setup [SQL Server], user accounts
- Windows permissions [SQL Server]
- modifying user accounts
- default accounts
- domains [SQL Server], user accounts
- startup accounts [SQL Server]
- system accounts [SQL Server]
- services [SQL Server], permissions
- ACL (access control list)
- local system accounts [SQL Server]
- instance-aware services [SQL Server]
- permissions [SQL Server], services
- SQL Server Agent service, user accounts
- Windows NT permissions [SQL Server]
- user accounts [SQL Server]
- identifying instance-unaware services [SQL Server]
- installing SQL Server, user accounts
- disabled startup state [SQL Server]
- user accounts [SQL Server], users
- Local Service account [SQL Server]
- SQL Server Installation Wizard
- instance-unaware services [SQL Server]
- services [SQL Server], configuring at installation
- Windows accounts [SQL Server]
- SQL Server services, user accounts
- user accounts [SQL Server], services
- MSSQLServer
- identifying instance-aware services [SQL Server]
- services [SQL Server], accounts
- access control lists
- optional accounts [SQL Server]
- service accounts [SQL Server]
- accounts [SQL Server], services
- built-in system accounts [SQL Server]
- automatic startup state
- domains [SQL Server]
- manual startup state [SQL Server]
- accounts [SQL Server], user
ms.assetid: 309b9dac-0b3a-4617-85ef-c4519ce9d014
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 329903c084872be2a51ec9a79f72759d503f63dd
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889457"
---
# <a name="configure-windows-service-accounts-and-permissions"></a>Configurar los permisos y las cuentas de servicio de Windows
  Cada servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] representa a un proceso o conjunto de procesos para administrar la autenticación de las operaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con Windows. En este tema se describe la configuración predeterminada de los servicios en esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como las opciones de configuración de los servicios [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se pueden establecer durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y después.  
  
##  <a name="Top"></a>Contenido  
 Este tema se divide en las siguientes secciones:  
  
-   [Servicios instalados por SQL Server](#Service_Details)  
  
-   [Propiedades y configuración del servicio](#Serv_Prop)  
  
    -   [Cuentas de servicio predeterminadas](#Default_Accts)  
  
        -   [Cambiar las propiedades de la cuenta](#Changing_Accounts)  
  
    -   [Nuevos tipos de cuenta disponibles con Windows 7 y Windows Server 2008 R2](#New_Accounts)  
  
    -   [Inicio automático](#Auto_Start)  
  
    -   [Configuración de servicios durante la instalación desatendida](#Configure_services)  
  
    -   [Puerto de firewall](#Firewall)  
  
-   [Permisos de servicio](#Serv_Perm)  
  
    -   [Configuración del servicio y control de acceso](#Serv_SID)  
  
    -   [Derechos y privilegios de Windows](#Windows)  
  
    -   [Permisos del sistema de archivos concedidos a SQL Server SID por servicio o grupos locales de Windows](#Reviewing_ACLs)  
  
    -   [Permisos del sistema de archivos concedidos a otras cuentas de usuario o grupos de Windows](#File_System_Other)  
  
    -   [Permisos del sistema de archivos relacionados con las ubicaciones inusuales de los discos](#Unusual_Locations)  
  
    -   [Revisar las consideraciones adicionales](#Review_additional_considerations)  
  
    -   [Permisos del Registro](#Registry)  
  
    -   [WMI](#WMI)  
  
    -   [Canalizaciones con nombre](#Pipes)  
  
-   [Aprovisionamiento](#Provisioning)  
  
    -   [Aprovisionamiento del motor de base de datos](#DE_Prov)  
  
        -   [Entidades de seguridad de Windows](#Win_Principals)  
  
        -   [Cuenta sa](#sa)  
  
        -   [Privilegios e inicio de sesión de SID por servicio de SQL Server](#Logins)  
  
        -   [Privilegios e inicio de sesión del Agente SQL Server](#Agent)  
  
        -   [Instancia y privilegios de los clústeres de conmutación por error de SQL y HADRON](#Hadron)  
  
        -   [Objeto de escritura SQL y privilegios](#Writer)  
  
        -   [WMI y privilegios de SQL](#SQLWMI)  
  
    -   [Aprovisionamiento de SSAS](#SSAS)  
  
    -   [Aprovisionamiento de SSRS](#SSRS)  
  
-   [Actualizar desde versiones anteriores](#Upgrade)  
  
-   [ICE](#Appendix)  
  
    -   [Descripción de las cuentas de servicio](#Serv_Accts)  
  
    -   [Identificar los servicios que reconocen y que no reconocen instancias](#Identify_instance_aware_and_unaware)  
  
    -   [Nombres de servicio traducidos](#Localized_service_names)  
  
##  <a name="Service_Details"></a> Servicios instalados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 En función de los componentes que decida instalar, el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalará los servicios siguientes:  
  
-   **Servicios de bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : servicio de [!INCLUDE[ssDE](../../includes/ssde-md.md)] relacional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El archivo ejecutable es \<MSSQLPATH>\MSSQL\Binn\sqlservr.exe.  
  
-   **Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : ejecuta trabajos, supervisa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], activa alertas y habilita la automatización de algunas tareas administrativas. El servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está presente pero deshabilitado en las instancias de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. El archivo ejecutable es \<MSSQLPATH>\MSSQL\Binn\sqlagent.exe.  
  
-   **[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]**  : proporciona funciones de procesamiento analítico en línea (OLAP) y minería de datos para aplicaciones de Business Intelligence. El archivo ejecutable es \<MSSQLPATH>\OLAP\Bin\msmdsrv.exe.  
  
-   **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  : administra, ejecuta, crea, programa y envía informes. El archivo ejecutable es \<MSSQLPATH>\Reporting Services\ReportServer\Bin\ReportingServicesService.exe.  
  
-   **[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]**  : proporciona compatibilidad de administración para el almacenamiento y la ejecución de paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . La ruta de acceso del \<archivo ejecutable es MSSQLPATH > \120\DTS\Binn\MsDtsSrvr.exe  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser** : servicio de resolución de nombres que proporciona información de conexión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a los equipos cliente. La ruta de acceso ejecutable es c:\Archivos de programa (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe  
  
-   **Búsqueda de texto completo** : crea rápidamente índices de texto completo del contenido y de las propiedades de los datos estructurados y semiestructurados para permitir el filtrado de documentos y la separación de palabras en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Objeto de escritura de SQL** : permite que las aplicaciones de copia de seguridad y restauración funcionen en el marco del Servicio de instantáneas de volumen (VSS).  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller** : proporciona la orquestación de la reproducción de seguimiento en varios equipos cliente de Distributed Replay.  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client** : uno o más equipos cliente de Distributed Replay que funcionan con un Distributed Replay Controller para simular cargas de trabajo simultáneas en una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
##  <a name="Serv_Prop"></a> Propiedades de servicio y configuración  
 Las cuentas de inicio usadas para iniciar y ejecutar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden ser [cuentas de usuario de dominio](#Domain_User), [cuentas de usuario local](#Local_User), [cuentas de servicio administradas](#MSA), [cuentas virtuales](#VA_Desc)o [cuentas del sistema integradas](#Local_Service). Para poder iniciarse y ejecutarse, cada servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener una cuenta de inicio que se configura durante la instalación.  
  
 En esta sección se describen las cuentas que se pueden configurar para iniciar los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los valores predeterminados que usa el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el concepto de SID por servicio, las opciones de inicio y la configuración del firewall.  
  
-   [Cuentas de servicio predeterminadas](#Default_Accts)  
  
-   [Inicio automático](#Auto_Start)  
  
-   [Configurar el tipo de inicio del servicio](#Configure_services)  
  
-   [Puerto de firewall](#Firewall)  
  
###  <a name="Default_Accts"></a> Cuentas de servicio predeterminadas  
 En la tabla siguiente se enumeran las cuentas de servicio predeterminadas que utiliza el programa de instalación para instalar todos los componentes. Las cuentas predeterminadas enumeradas son las recomendadas, si no se especifica lo contrario.  
  
 **Servidor independiente o controlador de dominio**  
  
|Componente|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]|Windows 7 y [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 y posterior|  
|---------------|------------------------------------|----------------------------------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]|[SERVICIO DE RED](#Network_Service)|[Cuenta virtual](#VA_Desc)<sup>*</sup>|  
|e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[SERVICIO DE RED](#Network_Service)|[Cuenta virtual](#VA_Desc)<sup>*</sup>|  
|[!INCLUDE[ssAS](../../includes/ssas-md.md)]|[SERVICIO DE RED](#Network_Service)|[Cuenta virtual](#VA_Desc)<sup>*</sup>|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)]|[SERVICIO DE RED](#Network_Service)|[Cuenta virtual](#VA_Desc)<sup>*</sup>|  
|[!INCLUDE[ssRS](../../includes/ssrs.md)]|[SERVICIO DE RED](#Network_Service)|[Cuenta virtual](#VA_Desc)<sup>*</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller|[SERVICIO DE RED](#Network_Service)|[Cuenta virtual](#VA_Desc)<sup>*</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client|[SERVICIO DE RED](#Network_Service)|[Cuenta virtual](#VA_Desc)<sup>*</sup>|  
|Selector de FD (búsqueda de texto completo)|[SERVICIO LOCAL](#Local_Service)|[Cuenta virtual](#VA_Desc)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|[SERVICIO LOCAL](#Local_Service)|[SERVICIO LOCAL](#Local_Service)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer|[SISTEMA LOCAL](#Local_System)|[SISTEMA LOCAL](#Local_System)|  
  
 <sup>*</sup>Cuando se necesitan recursos externos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al equipo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda el uso de una cuenta de servicio administrada (MSA), configurada con los privilegios mínimos necesarios.  
  
 **Instancia de clústeres de conmutación por error de SQL Server**  
  
|Componente|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2|  
|---------------|------------------------------------|---------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]|Ninguno. Proporcione una cuenta de [usuario de dominio](#Domain_User) .|Proporcione una cuenta de [usuario de dominio](#Domain_User) .|  
|e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Ninguno. Proporcione una cuenta de [usuario de dominio](#Domain_User) .|Proporcione una cuenta de [usuario de dominio](#Domain_User) .|  
|[!INCLUDE[ssAS](../../includes/ssas-md.md)]|Ninguno. Proporcione una cuenta de [usuario de dominio](#Domain_User) .|Proporcione una cuenta de [usuario de dominio](#Domain_User) .|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)]|[SERVICIO DE RED](#Network_Service)|[Cuenta virtual](#VA_Desc)|  
|[!INCLUDE[ssRS](../../includes/ssrs.md)]|[SERVICIO DE RED](#Network_Service)|[Cuenta virtual](#VA_Desc)|  
|Selector de FD (búsqueda de texto completo)|[SERVICIO LOCAL](#Local_Service)|[Cuenta virtual](#VA_Desc)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|[SERVICIO LOCAL](#Local_Service)|[SERVICIO LOCAL](#Local_Service)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer|[SISTEMA LOCAL](#Local_System)|[SISTEMA LOCAL](#Local_System)|  
  
####  <a name="Changing_Accounts"></a> Cambiar las propiedades de las cuentas  
  
> [!IMPORTANT]
>  -   Utilice siempre herramientas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cambiar la cuenta utilizada por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] o los servicios del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o para cambiar la contraseña de la cuenta. Además de cambiar el nombre de cuenta, el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza una configuración adicional como actualizar la seguridad local de Windows almacenada que protege la clave maestra de servicio para el [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Otras herramientas, como el Administrador de control de servicios de Windows, pueden cambiar el nombre de la cuenta, pero no toda la configuración requerida.  
> -   Para las instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se implementen en una granja de SharePoint, utilice siempre Administración central de SharePoint para cambiar las cuentas de servidor para las aplicaciones de [!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)] y de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]. Se actualizan la configuración y los permisos asociados para usar la nueva información de cuenta cuando utilice Administración central.  
> -   Para cambiar las opciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , utilice la herramienta configuración de Reporting Services.  
  
###  <a name="New_Accounts"></a>Nuevos tipos de cuenta disponibles con Windows 7 y Windows Server 2008 R2  
 Windows 7 y Windows Server 2008 R2 tienen dos nuevos tipos de cuentas de servicio denominadas cuentas de servicio administradas (MSA) y cuentas virtuales. Las cuentas de servicio administradas y las cuentas virtuales están diseñadas para proporcionar a aplicaciones cruciales como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el aislamiento de sus propias cuentas, mientras se elimina la necesidad de que un administrador administre manualmente el nombre de entidad de servicio (SPN) y las credenciales de estas cuentas. Estas cuentas facilitan en gran medida la administración a largo plazo de los usuarios de cuentas de servicio, las contraseñas y los SPN.  
  
-   <a name="MSA"></a> **Managed Service Accounts**  
  
     Una cuenta de servicio administrada (MSA) es un tipo de cuenta de dominio creada y administrada por el controlador de dominio. Se asigna a un solo equipo de miembro para usarla al ejecutar un servicio. El controlador de dominio administra la contraseña automáticamente. No puede utilizar MSA para iniciar sesión en un equipo, pero un equipo puede utilizar MSA para iniciar un servicio de Windows. Una MSA puede registrar el nombre principal de servicio (SPN) con Active Directory. Una MSA se denomina con un sufijo **$** , por ejemplo, **DOMINIO\NOMBREDECUENTA$** . Al especificar MSA, deje en blanco la contraseña. Debido a que una MSA se asigna a un único equipo, no se puede utilizar en nodos diferentes de un clúster de Windows.  
  
    > [!NOTE]  
    >  El administrador de dominio debe crear la MSA en Active Directory para que la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda usarla para los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
    
-  <a name="GMSA"></a> **Cuentas de servicio administradas de grupo**  
  
     Una cuenta de servicio administrada de grupo es una MSA para varios servidores. Windows administra una cuenta de servicio para los servicios que se ejecutan en un grupo de servidores. Active Directory actualiza automáticamente la contraseña de la cuenta de servicio administrada de grupo sin necesidad de reiniciar los servicios. Puede configurar servicios de SQL Server para usar una entidad de seguridad de cuenta de servicio administrada de grupo. A partir de SQL Server 2014, SQL Server admite cuentas de servicio administradas de grupo en Windows Server 2012 R2 y posterior para instancias independientes, instancias de clúster de conmutación por error y grupos de disponibilidad.  
  
    Para usar una cuenta de servicio administrada de grupo para SQL Server 2014 o posterior, el sistema operativo debe ser Windows Server 2012 R2 o posterior. Los servidores con Windows Server 2012 R2 necesitan que [KB 2998082](https://support.microsoft.com/kb/2998082) esté aplicado para que los servicios puedan iniciar sesión sin interrumpirse inmediatamente después de un cambio de contraseña.  
  
    Para obtener más información, vea [Group Managed Service Accounts (Cuentas de servicio administradas de grupo)](https://technet.microsoft.com/library/hh831782.aspx).  
      
    > [!NOTE]  
    >  El administrador de dominio debe crear la cuenta de servicio administrada de grupo en Active Directory para que la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda usarla para los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 
  
-   <a name="VA_Desc"></a>**Cuentas virtuales**  
  
     Las cuentas virtuales (a partir de Windows Server 2008 R2 y Windows 7) son *cuentas locales administradas* que proporcionan las siguientes características para simplificar la administración del servicio. La cuenta virtual se administra automáticamente y la cuenta virtual puede tener acceso a la red en un entorno de dominio. Si se usa el valor predeterminado de las cuentas de servicio durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se usará una cuenta virtual con el nombre de instancia como nombre del servicio, con el formato **NT SERVICE\\** _\<NOMBRE DEL SERVICIO>_ . Los servicios que se ejecutan como cuentas virtuales acceden a los recursos de red mediante las credenciales de la cuenta del equipo con el formato _<nombre_dominio>_ **\\** _<nombre_equipo>_ **$** .  Al especificar una cuenta virtual para iniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deje en blanco la contraseña. Si la cuenta virtual no puede registrar el nombre principal de servicio (SPN), registre el SPN manualmente. Para más información sobre cómo registrar un SPN manualmente, consulte [Registro manual de SPN](register-a-service-principal-name-for-kerberos-connections.md#Manual).  
  
    > [!NOTE]  
    >  No se pueden usar cuentas virtuales para la instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ya que la cuenta virtual no tendría el mismo SID en cada nodo del clúster.  
  
     En la tabla siguiente se muestran ejemplos de nombres de cuenta virtuales.  
  
    |Servicio|Nombre de cuenta virtual|  
    |-------------|--------------------------|  
    |Instancia predeterminada del servicio del [!INCLUDE[ssDE](../../includes/ssde-md.md)] .|**NT SERVICE\MSSQLSERVER**|  
    |Instancia con nombre de un servicio de [!INCLUDE[ssDE](../../includes/ssde-md.md)] denominado **PAYROLL**|**NT SERVICE\MSSQL$PAYROLL**|  
    |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|**NT SERVICE\SQLSERVERAGENT**|  
    |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada **PAYROLL**|**NT SERVICE\SQLAGENT$PAYROLL**|  
  
 Para obtener más información sobre las cuentas de servicio administradas y las cuentas virtuales, vea la sección **Managed service account and virtual account concepts (Conceptos de cuentas de servicio administradas y cuentas virtuales)** de [Service Accounts Step-by-Step Guide (Guía paso a paso de cuentas de servicio)](https://technet.microsoft.com/library/dd548356\(WS.10\).aspx) y [Managed Service Accounts Frequently Asked Questions (FAQ) (P+F sobre cuentas de servicio administradas)](https://technet.microsoft.com/library/ff641729\(WS.10\).aspx).  
  
 **Nota de seguridad:** [!INCLUDE[ssNoteLowRights](../../includes/ssnotelowrights-md.md)] Use una [MSA](#MSA) o una [cuenta virtual](#VA_Desc) siempre que sea posible. Cuando no se puedan usar MSA ni cuentas virtuales, emplee una cuenta de usuario específica con privilegios bajos o la cuenta de dominio en lugar de una cuenta compartida para los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Utilice cuentas independientes para los diferentes servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No otorgue permisos adicionales a la cuenta de servicio ni a los grupos de servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los permisos se concederán a través de la pertenencia a un grupo o se concederán directamente a un SID por servicio, siempre que se admita su uso.  
  
###  <a name="Auto_Start"></a> Inicio automático  
 Además de las cuentas de usuario, cada servicio tiene tres posibles estados de inicio que los usuarios pueden controlar:  
  
-   **Deshabilitado** El servicio se ha instalado, pero no se ejecuta actualmente.  
  
-   **Manual** : el servicio se ha instalado, pero solo se iniciará cuando otro servicio o aplicación necesite su funcionalidad.  
  
-   **Automático** : el sistema operativo inicia automáticamente el servicio.  
  
 El estado de inicio se selecciona durante la instalación. Al instalar una instancia con nombre, el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser debe establecerse para iniciarse automáticamente.  
  
###  <a name="Configure_services"></a> Servicios de configuración durante la instalación desatendida  
 En la tabla siguiente se muestran los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se pueden configurar durante la instalación. En instalaciones desatendidas, puede usar los modificadores en un archivo de configuración o en el símbolo del sistema.  
  
|Nombre de servicio SQL Server|Modificadores para instalaciones desatendidas<sup>1</sup>|  
|-----------------------------|-------------------------------------------------------|  
|MSSQLSERVER|SQLSVCACCOUNT, SQLSVCPASSWORD, SQLSVCSTARTUPTYPE|  
|SQLServerAgent<sup>2</sup>|AGTSVCACCOUNT, AGTSVCPASSWORD, AGTSVCSTARTUPTYPE|  
|MSSQLServerOLAPService|ASSVCACCOUNT, ASSVCPASSWORD, ASSVCSTARTUPTYPE|  
|ReportServer|RSSVCACCOUNT, RSSVCPASSWORD, RSSVCSTARTUPTYPE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|ISSVCACCOUNT, ISSVCPASSWORD, ISSVCSTARTUPTYPE|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller|DRU_CTLR, CTLRSVCACCOUNT, CTLRSVCPASSWORD, CTLRSTARTUPTYPE, CTLRUSERS|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client|DRU_CLT, CLTSVCACCOUNT, CLTSVCPASSWORD, CLTSTARTUPTYPE, CLTCTLRNAME, CLTWORKINGDIR, CLTRESULTDIR|  
  
 <sup>1</sup> Para obtener más información y la sintaxis de ejemplo de las instalaciones desatendidas, vea [Install SQL Server 2014 desde el símbolo del sistema](../install-windows/install-sql-server-from-the-command-prompt.md).  
  
 <sup>2</sup> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio del agente está deshabilitado [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] las instancias de y con Advanced Services.  
  
###  <a name="Firewall"></a> Puerto de firewall  
 En la mayoría de los casos, cuando se instala inicialmente, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] puede conectarse con herramientas como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] instaladas en el mismo equipo que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no abre los puertos en el firewall de Windows. Las conexiones desde otros equipos pueden no ser posibles hasta que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] se configura para escuchar en un puerto TCP y el puerto adecuado se abre para las conexiones en el firewall de Windows. Para obtener más información vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
##  <a name="Serv_Perm"></a> Permisos de servicio  
 En esta sección se describen los permisos que el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura para el SID por servicio de los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   [Configuración del servicio y control de acceso](#Serv_SID)  
  
-   [Derechos y privilegios de Windows](#Windows)  
  
-   [Permisos del sistema de archivos concedidos a SQL Server por SID por servicio o grupos locales de Windows](#Reviewing_ACLs)  
  
-   [Permisos del sistema de archivos concedidos a otras cuentas de usuario o grupos de Windows](#File_System_Other)  
  
-   [Permisos del sistema de archivos relacionados con las ubicaciones inusuales de los discos](#Unusual_Locations)  
  
-   [Revisar las consideraciones adicionales](#Review_additional_considerations)  
  
-   [Permisos del Registro](#Registry)  
  
-   [WMI](#WMI)  
  
-   [Canalizaciones con nombre](#Pipes)  
  
###  <a name="Serv_SID"></a> Configuración del servicio y control de acceso  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] habilita un SID por servicio por cada uno de sus servicios para permitir el aislamiento del servicio y proporcionar una defensa optimizada. El SID por servicio se deriva del nombre del servicio y es único para ese servicio. Por ejemplo, el nombre de un SID del servicio [!INCLUDE[ssDE](../../includes/ssde-md.md)] podría ser **NT Service\MSSQL$** _\<nombreDeInstancia>_ . El aislamiento del servicio permite obtener acceso a objetos concretos sin necesidad de ejecutar una cuenta con un alto nivel de privilegios ni debilitar la protección de seguridad del objeto. Mediante el uso de una entrada de control de acceso que contenga un SID por servicio, un servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede restringir el acceso a sus recursos.  
  
> [!NOTE]  
>  En Windows 7 y [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 (y posteriores) el SID por servicio puede ser la cuenta virtual que utiliza el servicio.  
  
 Para la mayoría de los componentes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura la ACL para la cuenta del servicio directamente, con lo que el cambio de la cuenta de servicio puede realizarse sin tener que repetir el proceso de la ACL de recursos.  
  
 Al instalar [!INCLUDE[ssAS](../../includes/ssas-md.md)], se crea un SID por servicio para el servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se crea un grupo de Windows local y se le asigna un nombre con el formato **SQLServerMSASUser$** _computer_name_ **$** _instance_name_ . Al SID por servicio **NT SERVICE\MSSQLServerOLAPService** se le concede la pertenencia al grupo local de Windows y al grupo local de Windows se le conceden los permisos adecuados en la ACL. Si la cuenta utilizada para iniciar el servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se cambia, el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe cambiar algunos permisos de Windows (como el derecho de iniciar sesión como servicio), pero los permisos asignados al grupo local de Windows no estarán disponibles sin actualizar, porque el SID por servicio no ha cambiado. Este método permite cambiar el nombre del servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durante las actualizaciones.  
  
 Durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea grupos de Windows locales para [!INCLUDE[ssAS](../../includes/ssas-md.md)] y el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser. Para estos servicios, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura la ACL para los grupos de Windows locales.  
  
 En función de la configuración del servicio, la cuenta de servicio o el SID por servicio se agregará como miembro del grupo de servicios durante el proceso de instalación o actualización.  
  
###  <a name="Windows"></a> Derechos y privilegios de Windows  
 La cuenta asignada para iniciar un servicio necesita el **permiso de inicio, detener y pausar** para el servicio. El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna esto automáticamente.  Primera instalación de las Herramientas de administración remota del servidor (RSAT). Vea las [Herramientas de administración remota del servidor para Windows 7](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=7d2f6ad7-656b-4313-a005-4e344e43997d).  
  
 En la tabla siguiente se muestran los permisos que el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicita para las SID por servicio o los grupos locales de Windows que usan los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Servicio[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Permisos concedidos por el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|---------------------------------------|------------------------------------------------------------|  
|**[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]:**<br /><br /> (Todos los derechos se conceden al SID por servicio. Instancia predeterminada: **NT SERVICE\MSSQLSERVER**. Instancia con nombre: **NT SERVICE\MSSQL$** nombreDeInstancia).|**Iniciar sesión como servicio** (SeServiceLogonRight)<br /><br /> **Reemplazar un token de nivel de proceso** (SeAssignPrimaryTokenPrivilege)<br /><br /> **Omitir comprobación de recorrido** (SeChangeNotifyPrivilege)<br /><br /> **Ajustar las cuotas de la memoria para un proceso** (SeIncreaseQuotaPrivilege)<br /><br /> Permiso para iniciar el objeto de escritura de SQL<br /><br /> Permiso para leer el servicio Registro de eventos<br /><br /> Permiso para leer el servicio Llamada a procedimiento remoto|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Directivas** <sup>1</sup><br /><br /> (Todos los derechos se conceden al SID por servicio. Instancia predeterminada: **NT Service\SQLSERVERAGENT**. Instancia con nombre: **NT Service\SQLAGENT$** _nombreDeInstancia_ ).|**Iniciar sesión como servicio** (SeServiceLogonRight)<br /><br /> **Reemplazar un token de nivel de proceso** (SeAssignPrimaryTokenPrivilege)<br /><br /> **Omitir comprobación de recorrido** (SeChangeNotifyPrivilege)<br /><br /> **Ajustar las cuotas de la memoria para un proceso** (SeIncreaseQuotaPrivilege)|  
|**[!INCLUDE[ssAS](../../includes/ssas-md.md)]:**<br /><br /> (Todos los derechos se conceden a un grupo local de Windows. Instancia predeterminada: **SQLServerMSASUser$** _NombreDeEquipo_ **$MSSQLSERVER**. Instancia con nombre: **SQLServerMSASUser$** _NombreDeEquipo_ **$** _NombreDeInstancia_ . Instancia de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]: **SQLServerMSASUser$** _NombreDeEquipo_ **$** _PowerPivot_ ).|**Iniciar sesión como servicio** (SeServiceLogonRight)<br /><br /> Solo para modo tabular:<br /><br /> **Aumentar el espacio de trabajo de un proceso** (SeIncreaseWorkingSetPrivilege)<br /><br /> **Ajustar las cuotas de la memoria para un proceso** (SeIncreaseQuotaSizePrivilege)<br /><br /> **Bloquear páginas en la memoria** (SeLockMemoryPrivilege): solo es necesario cuando la paginación está completamente desactivada.<br /><br /> Solo para la instalación de clústeres de conmutación por error:<br /><br /> **Aumentar prioridad de programación** (SeIncreaseBasePriorityPrivilege)|  
|**[!INCLUDE[ssRS](../../includes/ssrs.md)]:**<br /><br /> (Todos los derechos se conceden al SID por servicio. Instancia predeterminada: **NT SERVICE\ReportServer**. Instancia con nombre: **NT Service\\InstanceName).$**|**Iniciar sesión como servicio** (SeServiceLogonRight)|  
|**[!INCLUDE[ssIS](../../includes/ssis-md.md)]:**<br /><br /> (Todos los derechos se conceden al SID por servicio. Instancia predeterminada e instancia con nombre: **SERVICE\MsDtsServer120 NT**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no tiene un proceso independiente para una instancia con nombre).|**Iniciar sesión como servicio** (SeServiceLogonRight)<br /><br /> Permiso para escribir en el registro de eventos de la aplicación<br /><br /> **Omitir comprobación de recorrido** (SeChangeNotifyPrivilege)<br /><br /> **Suplantar a un cliente tras la autenticación** (SeImpersonatePrivilege)|  
|**Búsqueda de texto completo:**<br /><br /> (Todos los derechos se conceden al SID por servicio. Instancia predeterminada: **NT Service\MSSQLFDLauncher**. Instancia con nombre: **NT Service\ MSSQLFDLauncher$** _nombreDeInstancia_ ).|**Iniciar sesión como servicio** (SeServiceLogonRight)<br /><br /> **Ajustar las cuotas de la memoria para un proceso** (SeIncreaseQuotaPrivilege)<br /><br /> **Omitir comprobación de recorrido** (SeChangeNotifyPrivilege)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser:**<br /><br /> (Todos los derechos se conceden a un grupo local de Windows. Instancia con nombre o predeterminada: **SQLServer2005SQLBrowserUser** _$NombreEquipo_ . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser no tiene un proceso independiente para una instancia con nombre).|**Iniciar sesión como servicio** (SeServiceLogonRight)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer:**<br /><br /> (Todos los derechos se conceden al SID por servicio. Instancia con nombre o predeterminada: **NT Service\SQLWriter**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer no tiene un proceso independiente para una instancia con nombre).|El servicio SQLWriter se ejecuta en la cuenta de sistema local que tiene todos los permisos necesarios. El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no comprueba ni concede permisos para este servicio.|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller:**|**Iniciar sesión como servicio** (SeServiceLogonRight)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client:**|**Iniciar sesión como servicio** (SeServiceLogonRight)|  
  
 <sup>1</sup> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio del agente está deshabilitado [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]en las instancias de.  
  
###  <a name="Reviewing_ACLs"></a> Permisos del sistema de archivos concedidos a SID por servicio de SQL Server o grupos locales de Windows  
 Las cuentas de servicio de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben tener acceso a los recursos. Las listas de control de acceso se establecen para el SID por servicio o el grupo local de Windows.  
  
> [!IMPORTANT]  
>  En las instalaciones de clústeres de conmutación por error, los recursos de discos compartidos se deben establecer en una ACL de una cuenta local.  
  
 En la tabla siguiente se muestran las ACL establecidas mediante el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Cuenta de servicio para|Archivos y carpetas|Acceso|  
|-------------------------|-----------------------|------------|  
|MSSQLServer|Instid\MSSQL\backup|Control total|  
||Instid\MSSQL\binn|Lectura, Ejecución|  
||Instid\MSSQL\data|Control total|  
||Instid\MSSQL\FTData|Control total|  
||Instid\MSSQL\Install|Lectura, Ejecución|  
||Instid\MSSQL\Log|Control total|  
||Instid\MSSQL\Repldata|Control total|  
||120\shared|Lectura, Ejecución|  
||Instid\MSSQL\Template Data (solo[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] )|Lectura|  
|SQLServerAgent<sup>1</sup>|Instid\MSSQL\binn|Control total|  
||Instid\MSSQL\binn|Control total|  
||Instid\MSSQL\Log|Lectura, Escritura, Eliminación, Ejecución|  
||120\com|Lectura, Ejecución|  
||120\shared|Lectura, Ejecución|  
||120\shared\Errordumps|Lectura, Escritura|  
||ServerName\EventLog|Control total|  
|FTS|Instid\MSSQL\FTData|Control total|  
||Instid\MSSQL\FTRef|Lectura, Ejecución|  
||120\shared|Lectura, Ejecución|  
||120\shared\Errordumps|Lectura, Escritura|  
||Instid\MSSQL\Install|Lectura, Ejecución|  
||Instid\MSSQL\jobs|Lectura, Escritura|  
|MSSQLServerOLAPService|120\shared\ASConfig|Control total|  
||Instid\OLAP|Lectura, Ejecución|  
||Instid\Olap\Data|Control total|  
||Instid\Olap\Log|Lectura, Escritura|  
||Instid\OLAP\Backup|Lectura, Escritura|  
||Instid\OLAP\Temp|Lectura, Escritura|  
||120\shared\Errordumps|Lectura, Escritura|  
|SQLServerReportServerUser|Instid\Reporting Services\Log Files|Lectura, Escritura, Eliminación|  
||Instid\Reporting Services\ReportServer|Lectura, Ejecución|  
||Instid\Reportingservices\Reportserver\global.asax|Control total|  
||Instid\Reportingservices\Reportserver\Reportserver.config|Lectura|  
||Instid\Reporting Services\reportManager|Lectura, Ejecución|  
||Instid\Reporting Services\RSTempfiles|Lectura, Escritura, Ejecución, Eliminación|  
||120\shared|Lectura, Ejecución|  
||120\shared\Errordumps|Lectura, Escritura|  
|MSDTSServer100|120\dts\binn\MsDtsSrvr.ini.xml|Lectura|  
||120\dts\binn|Lectura, Ejecución|  
||120\shared|Lectura, Ejecución|  
||120\shared\Errordumps|Lectura, Escritura|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|120\shared\ASConfig|Lectura|  
||120\shared|Lectura, Ejecución|  
||120\shared\Errordumps|Lectura, Escritura|  
|SQLWriter|N/D (Se ejecuta como sistema local)||  
|Usuario|Instid\MSSQL\binn|Lectura, Ejecución|  
||Instid\Reporting Services\ReportServer|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||Instid\Reportingservices\Reportserver\global.asax|Lectura|  
||Instid\Reporting Services\reportManager|Lectura, Ejecución|  
||Instid\Reporting Services\ReportManager\pages|Lectura|  
||Instid\Reporting Services\ReportManager\Styles|Lectura|  
||120\dts|Lectura, Ejecución|  
||120\tools|Lectura, Ejecución|  
||100\tools|Lectura, Ejecución|  
||90\tools|Lectura, Ejecución|  
||80\tools|Lectura, Ejecución|  
||120\sdk|Lectura|  
||Microsoft SQL Server\120\Setup Bootstrap|Lectura, Ejecución|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller|\<ToolsDir>\DReplayController\Log\ (directorio vacío)|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayController\DReplayController.exe|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayController\resources\|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayController\\{todas las DLL}|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayController\DReplayController.config|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayController\IRTemplate.tdf|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayController\IRDefinition.xml|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client|\<ToolsDir>\DReplayClient\Log\|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayClient\DReplayClient.exe|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayClient\resources\|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayClient\ (todas las DLL)|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayClient\DReplayClient.config|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayClient\IRTemplate.tdf|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
||\<ToolsDir>\DReplayClient\IRDefinition.xml|Lectura, Ejecución, Mostrar el contenido de la carpeta|  
  
 <sup>1</sup> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio del agente está deshabilitado [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] las instancias de y con Advanced Services.  
  
 Cuando los archivos de base de datos se almacenan en una ubicación definida por el usuario, se debe conceder acceso a dicha ubicación al SID por servicio. Para obtener más información sobre la concesión de permisos del sistema de archivos a un SID por servicio, vea [Configurar permisos del sistema de archivos para el acceso al motor de base de datos](configure-file-system-permissions-for-database-engine-access.md).  
  
###  <a name="File_System_Other"></a> Permisos del sistema de archivos concedidos a otras cuentas de usuario o grupos de Windows  
 Es posible que sea necesario conceder algunos permisos de control de acceso a cuentas integradas o a otras cuentas de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La tabla siguiente muestra las ACL adicionales que son establecidas mediante el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Componente que realiza la solicitud|Cuenta|Resource|Permisos|  
|--------------------------|-------------|--------------|-----------------|  
|MSSQLServer|Usuarios del registro de rendimiento|Instid\MSSQL\binn|Mostrar el contenido de la carpeta|  
||Usuarios del monitor de sistema|Instid\MSSQL\binn|Mostrar el contenido de la carpeta|  
||Usuarios del registro de rendimiento, Usuarios del monitor de rendimiento|\WINNT\system32\sqlctr120.dll|Lectura, Ejecución|  
||Solo el administrador|\\\\.\root\Microsoft\SqlServer\ServerEvents\\<sql_instance_name><sup>1</sup>|Control total|  
||Administradores, sistema|\tools\binn\schemas\sqlserver\2004\07\showplan|Control total|  
||Usuarios|\tools\binn\schemas\sqlserver\2004\07\showplan|Lectura, Ejecución|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|\<Cuenta de servicio web del servidor de informes>|*\<instalación>* \Reporting Services\LogFiles|SUPRIMIR<br /><br /> READ_CONTROL<br /><br /> SYNCHRONIZE<br /><br /> FILE_GENERIC_READ<br /><br /> FILE_GENERIC_WRITE<br /><br /> FILE_READ_DATA<br /><br /> FILE_WRITE_DATA<br /><br /> FILE_APPEND_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_WRITE_EA<br /><br /> FILE_READ_ATTRIBUTES<br /><br /> FILE_WRITE_ATTRIBUTES|  
||Identidad del grupo de aplicaciones del Administrador de informes, cuenta [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] , Todos|*\<instalación>* \Reporting Services\ReportManager, *\<instalación>* \Reporting Services\ReportManager\Pages\\\*.\*, *\<instalación>* \Reporting Services\ReportManager\Styles\\\*.\*, *\<instalación>* \Reporting Services\ReportManager\webctrl_client\1_0\\*.\*|Lectura|  
||Identidad del grupo de aplicaciones del Administrador de informes|*\<instalación>* \Reporting Services\ReportManager\Pages\\*.\*|Lectura|  
||\<Cuenta de servicio web del servidor de informes>|*\<instalación>* \Reporting Services\ReportServer|Lectura|  
||\<Cuenta de servicio web del servidor de informes>|*\<instalación>* \Reporting Services\ReportServer\global.asax|Completo|  
||Todos|*\<instalación>* \Reporting Services\ReportServer\global.asax|READ_CONTROL<br /><br /> FILE_READ_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_READ_ATTRIBUTES|  
||SERVICIO DE RED|*\<instalación>* \Reporting Services\ReportServer\ReportService.asmx|Completo|  
||Todos|*\<instalación>* \Reporting Services\ReportServer\ReportService.asmx|READ_CONTROL<br /><br /> SYNCHRONIZE FILE_GENERIC_READ<br /><br /> FILE_GENERIC_EXECUTE<br /><br /> FILE_READ_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_EXECUTE<br /><br /> FILE_READ_ATTRIBUTES|  
||Cuenta de servicios de Windows ReportServer|*\<instalación>* \Reporting Services\ReportServer\RSReportServer.config|SUPRIMIR<br /><br /> READ_CONTROL<br /><br /> SYNCHRONIZE<br /><br /> FILE_GENERIC_READ<br /><br /> FILE_GENERIC_WRITE<br /><br /> FILE_READ_DATA<br /><br /> FILE_WRITE_DATA<br /><br /> FILE_APPEND_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_WRITE_EA<br /><br /> FILE_READ_ATTRIBUTES<br /><br /> FILE_WRITE_ATTRIBUTES|  
||Todos|Claves del Servidor de informes (subárbol Instid)|Consultar valor<br /><br /> Enumerar subclaves<br /><br /> Notificar<br /><br /> Controles de lectura|  
||Usuario de Terminal Services|Claves del Servidor de informes (subárbol Instid)|Consultar valor<br /><br /> Establecer valor<br /><br /> Crear subclave<br /><br /> Enumerar subclave<br /><br /> Notificar<br /><br /> DELETE<br /><br /> Controles de lectura|  
||Usuarios avanzados|Claves del Servidor de informes (subárbol Instid)|Consultar valor<br /><br /> Establecer valor<br /><br /> Crear subclave<br /><br /> Enumerar subclaves<br /><br /> Notificar<br /><br /> DELETE<br /><br /> Controles de lectura|  
  
 <sup>1</sup> Este es el espacio de nombres del proveedor WMI.  
  
###  <a name="Unusual_Locations"></a> Permisos del sistema de archivos relacionados con las ubicaciones inusuales de los discos  
 La unidad predeterminada para las ubicaciones de instalación es **systemdrive**, normalmente la unidad C: al instalar bases de datos tempdb o de usuario  
  
 **Unidad de disco no predeterminada**  
  
 Cuando se instala una unidad local que no es la predeterminada, el SID por servicio debe tener acceso a la ubicación del archivo. El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporcionará el acceso necesario.  
  
 **Recurso compartido de red**  
  
 Cuando las bases de datos se instalan en un recurso compartido de red, la cuenta de servicio debe tener acceso a la ubicación del archivo de las bases de datos de usuario y tempdb. El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede proporcionar acceso a un recurso compartido de red. El usuario debe proporcionar acceso a una ubicación de tempdb para la cuenta de servicio antes de ejecutar el programa de instalación. El usuario debe proporcionar acceso a la ubicación de la base de datos de usuario antes de crear la base de datos.  
  
> [!NOTE]  
>  Las cuentas virtuales no se pueden autenticar en una ubicación remota. Todas las cuentas virtuales usan el permiso de la cuenta del equipo. Aprovisione la cuenta de equipo con el formato _<nombre_dominio>_ **\\** _<nombre_equipo>_ **$** .  
  
###  <a name="Review_additional_considerations"></a> Revisar las consideraciones adicionales  
 En la tabla siguiente se muestran los permisos que necesitan los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para proporcionar una funcionalidad adicional.  
  
|Servicio/Aplicación|Funcionalidad|Permiso necesario|  
|--------------------------|-------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)|Escribir en un buzón de correo mediante xp_sendmail.|Permisos de escritura de la red.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)|Ejecute xp_cmdshell para un usuario que no sea administrador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Actuar como parte del sistema operativo y reemplazar un token de nivel de proceso.|  
|Agente[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)|Usar la característica de reinicio automático.|Debe ser un miembro del grupo local Administradores.|  
|Asistente para la optimización de[!INCLUDE[ssDE](../../includes/ssde-md.md)]|Optimiza las bases de datos para un rendimiento óptimo de las consultas.|Al utilizarla por primera vez, un usuario que tenga credenciales administrativas debe inicializar la aplicación. Después de la inicialización, los usuarios de dbo pueden usar el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para optimizar solo aquellas tablas de las que son propietarios. Para obtener más información, vea el tema que trata sobre cómo inicializar el Asistente para la optimización del [!INCLUDE[ssDE](../../includes/ssde-md.md)] en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  
> [!IMPORTANT]  
>  Antes de actualizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], habilite la autenticación de Windows para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y compruebe la configuración predeterminada necesaria: que la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sea miembro del grupo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sysadmin.  
  
###  <a name="Registry"></a> Permisos del Registro  
 El subárbol del Registro se crea en **HKLM\Software\Microsoft\Microsoft SQL Server\\** _<Id_instancia>_ para los componentes que dependen de la instancia. Por ejemplo  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSSQL12.MyInstance**  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSASSQL12.MyInstance**  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSSQL.120**  
  
 El Registro también mantiene una asignación de identificador de instancia a nombre de instancia. La asignación de identificador de instancia a nombre de instancia se mantiene de la siguiente forma:  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Servidor\instancia Names\SQL] "NombreDeInstancia" = "MSSQL12"**  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\OLAP] "InstanceName"="MSASSQL12"**  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\RS] "InstanceName"="MSRSSQL12"**  
  
###  <a name="WMI"></a> WMI  
 El Instrumental de administración de Windows (WMI) debe poder conectarse al [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para admitir esto, el SID por servicio del proveedor WMI de Windows (**NT SERVICE\winmgmt**) se aprovisiona en [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 El proveedor WMI de SQL requiere los siguientes permisos:  
  
-   Pertenencia a los roles fijos de base de datos **db_ddladmin** o **db_owner** en la base de datos msdb.  
  
-   El permiso**CREATE DDL EVENT NOTIFICATION** en el servidor.  
  
-   El permiso**CREATE TRACE EVENT NOTIFICATION** en el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Permiso de nivel de servidor**VIEW ANY DATABASE** .  
  
     El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un espacio de nombres WMI SQL y concede el permiso de lectura al SID por servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
###  <a name="Pipes"></a> Canalizaciones con nombre  
 En toda la instalación, el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona acceso al [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] a través del protocolo de memoria compartida, que es una canalización con nombre local.  
  
##  <a name="Provisioning"></a> Aprovisionamiento  
 En esta sección se describe el modo en que se aprovisionan las cuentas dentro de los distintos componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [Aprovisionamiento del motor de base de datos](#DE_Prov)  
  
    -   [Entidades de seguridad de Windows](#Win_Principals)  
  
    -   [Cuenta sa](#sa)  
  
    -   [Privilegios e inicio de sesión de SID por servicio de SQL Server](#Logins)  
  
    -   [Privilegios e inicio de sesión del Agente SQL Server](#Agent)  
  
    -   [Instancia y privilegios de los clústeres de conmutación por error de SQL y HADRON](#Hadron)  
  
    -   [Objeto de escritura SQL y privilegios](#Writer)  
  
    -   [WMI y privilegios de SQL](#SQLWMI)  
  
-   [Aprovisionamiento de SSAS](#SSAS)  
  
-   [Aprovisionamiento de SSRS](#SSRS)  
  
###  <a name="DE_Prov"></a> Aprovisionamiento del motor de base de datos  
 Las cuentas siguientes se agregan como inicios de sesión en el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
####  <a name="Win_Principals"></a> Entidades de seguridad de Windows  
 Durante la instalación, el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere al menos que una cuenta de usuario se denomine como un miembro del rol fijo de servidor **sysadmin** .  
  
####  <a name="sa"></a> Cuenta sa  
 La cuenta **sa** está siempre presente como inicio de sesión de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y es miembro del rol fijo de servidor **sysadmin** . Cuando [!INCLUDE[ssDE](../../includes/ssde-md.md)] se instala solo con autenticación de Windows (es decir, cuando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no está habilitada), el inicio de sesión de **sa** aún está presente, aunque deshabilitado. Para obtener información sobre cómo habilitar la cuenta **sa** , vea [Cambiar el modo de autenticación del servidor](change-server-authentication-mode.md).  
  
####  <a name="Logins"></a> Privilegios e inicio de sesión de SID por servicio de SQL Server  
 El SID por servicio del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se proporciona como inicio de sesión del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . El inicio de sesión del SID por servicio es un miembro del rol fijo de servidor **sysadmin** .  
  
####  <a name="Agent"></a> Privilegios e inicio de sesión del Agente SQL Server  
 El SID por servicio del servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se proporciona como un inicio de sesión del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . El inicio de sesión del SID por servicio es un miembro del rol fijo de servidor **sysadmin** .  
  
####  <a name="Hadron"></a> [!INCLUDE[ssHADRc](../../includes/sshadrc-md.md)]  
 Al instalar [!INCLUDE[ssDE](../../includes/ssde-md.md)] como una instancia de los clústeres de conmutación por error de SQL (SQL FCI) o [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] , **LOCAL SYSTEM** se proporciona en [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Al inicio de sesión a **LOCAL SYSTEM** se le concede el permiso **ALTER ANY AVAILABILITY GROUP** (para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]) y el permiso **VIEW SERVER STATE** (para SQL FCI).  
  
####  <a name="Writer"></a> Objeto de escritura SQL y privilegios  
 El SID por servicio del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer se proporciona como un inicio de sesión del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . El inicio de sesión del SID por servicio es un miembro del rol fijo de servidor **sysadmin** .  
  
####  <a name="SQLWMI"></a> WMI y privilegios de SQL  
 El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aprovisiona la cuenta **NT SERVICE\Winmgmt** como un inicio de sesión de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y la agrega al rol fijo de servidor **sysadmin** .  
  
#### <a name="ssrs-provisioning"></a>Aprovisionamiento de SSRS  
 La cuenta especificada durante la instalación se aprovisiona como miembro del rol de base de datos **RSExecRole** . Para obtener más información, vea [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
###  <a name="SSAS"></a> Aprovisionamiento de SSAS  
 Los requisitos de cuentas de servicio de[!INCLUDE[ssAS](../../includes/ssas-md.md)] varían en función de cómo se implementa en el servidor. Si va a instalar [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere que se configure el servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para ejecutarse en una cuenta de dominio. Las cuentas de dominio son necesarias para admitir la facilidad administrada de la cuenta que está integrada en SharePoint. Por esta razón, el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no proporciona una cuenta de servicio predeterminada, como una cuenta virtual, para una instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Para más información sobre el aprovisionamiento de PowerPivot para SharePoint, vea [Configurar las cuentas de servicio PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts).  
  
 Para todas las demás instalaciones independientes de [!INCLUDE[ssAS](../../includes/ssas-md.md)], puede aprovisionar el servicio para ejecutarse en una cuenta de dominio, una cuenta del sistema integrada, una cuenta administrada o una cuenta virtual. Para obtener más información sobre el aprovisionamiento de cuentas, vea [Configurar las cuentas de servicio &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/instances/configure-service-accounts-analysis-services).  
  
 Para instalaciones en clúster, debe especificar una cuenta de dominio o una cuenta del sistema integrada. Ni las cuentas administradas ni las cuentas virtuales se admiten en los clústeres de conmutación por error de [!INCLUDE[ssAS](../../includes/ssas-md.md)] .  
  
 Todas las instalaciones de [!INCLUDE[ssAS](../../includes/ssas-md.md)] requieren que especifique un administrador del sistema de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Los privilegios de administrador se aprovisionan en el rol **Servidor** de Analysis Services.  
  
###  <a name="SSRS"></a> Aprovisionamiento de SSRS  
 La cuenta especificada durante la instalación se aprovisiona en el [!INCLUDE[ssDE](../../includes/ssde-md.md)] como miembro del rol de base de datos **RSExecRole** . Para obtener más información, vea [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
##  <a name="Upgrade"></a> Actualización de versiones anteriores  
 En esta sección se describen los cambios realizados durante la actualización de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] requiere [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 SP1, Windows Server 2012, Windows 8.0, Windows Server 2012 R2 o Windows 8.1. Cualquier versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta en una versión de sistema operativo inferior debe tener el sistema operativo actualizado antes de actualizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Durante la actualización de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del modo siguiente.  
  
    -   El [!INCLUDE[ssDE](../../includes/ssde-md.md)] se ejecuta con el contexto de seguridad del SID por servicio. Al SID por servicio se el concede el acceso a las carpetas de archivos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (como DATA) y las claves del Registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   El SID por servicio de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se aprovisiona en [!INCLUDE[ssDE](../../includes/ssde-md.md)] como miembro del rol fijo de servidor **sysadmin** .  
  
    -   Los SID por servicio se agregan a los grupos de Windows locales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a menos que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sea una instancia de clústeres de conmutación por error.  
  
    -   Los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siguen aprovisionados para los grupos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows locales.  
  
    -   El nombre del grupo de Windows local de los servicios se cambia de **SQLServer2005MSSQLUser$** _<nombre_equipo>_ **$** _<nombre_instancia>_ a **SQLServerMSSQLUser$** _<nombre_equipo>_ **$** _<nombre_instancia>_ . Las ubicaciones de archivos de las bases de datos migradas tendrán entradas de control de acceso (ACE) para los grupos de Windows locales. Las ubicaciones de archivos para las nuevas bases de datos tendrán ACE para el SID por servicio.  
  
-   Durante la actualización de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conservará las ACE para el SID por servicio de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
-   Para una instancia de los clústeres de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se conservará la ACE de la cuenta de dominio configurada para el servicio.  
  
##  <a name="Appendix"></a> Apéndice  
 Esta sección contiene información adicional sobre los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [Descripción de las cuentas de servicio](#Serv_Accts)  
  
-   [Identificar los servicios que reconocen y que no reconocen instancias](#Identify_instance_aware_and_unaware)  
  
-   [Nombres de servicio traducidos](#Localized_service_names)  
  
###  <a name="Serv_Accts"></a> Descripción de las cuentas de servicio  
 La cuenta de servicio es la que se usa para iniciar un servicio de Windows, como [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
####  <a name="Any_OS"></a> Cuentas disponibles con cualquier sistema operativo  
 Además de las nuevas cuentas [MSA](#MSA) y las [cuentas virtuales](#VA_Desc) descritas anteriormente, pueden usarse las siguientes cuentas.  
  
 <a name="Domain_User"></a> **Cuenta de usuario de dominio**  
  
 Si el servicio debe interactuar con servicios de red o tener acceso a recursos de un dominio como los recursos compartidos de archivos, o si utiliza conexiones con el servidor vinculadas a otros equipos que ejecutan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], podría utilizar una cuenta de servidor de dominio con privilegios mínimos. Muchas actividades de servidor a servidor solo se pueden realizar con una cuenta de usuario de dominio. El administrador del dominio del entorno debe haber creado esta cuenta previamente.  
  
> [!NOTE]  
>  Si configura la aplicación para utilizar una cuenta de dominio, puede aislar los privilegios de la aplicación, pero debe administrar manualmente contraseñas o crear una solución personalizada para administrar estas contraseñas. Muchas aplicaciones de servidor usan esta estrategia para mejorar la seguridad, pero requiere una administración adicional y conlleva una mayor complejidad. En estas implementaciones, los administradores de servicios emplean un tiempo considerable en las tareas de mantenimiento como la administración de las contraseñas de servicio y los nombres principales de servicio (SPN), que son necesarios para la autenticación Kerberos. Además, estas tareas de mantenimiento pueden interrumpir el servicio.  
  
 <a name="Local_User"></a> **Local User Accounts**  
  
 Si el equipo no forma parte de un dominio, se recomienda usar una cuenta de usuario local sin permisos de administrador de Windows.  
  
 <a name="Local_Service"></a> **Cuenta de servicio local**  
  
 La cuenta de servicio local es una cuenta integrada que tiene el mismo nivel de acceso a los recursos y objetos que los miembros del grupo Usuarios. Este acceso limitado ayuda a proteger el sistema en caso de que los servicios o procesos individuales se vean comprometidos. Los servicios que se ejecutan en la cuenta de servicio local obtienen acceso a los recursos de la red como una sesión nula sin credenciales. Tenga en cuenta que la cuenta de servicio local no se admite para los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ni de Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No se admite el servicio local como la cuenta que ejecuta los servicios porque es un servicio compartido y cualquier otro servicio que se ejecute bajo el servicio local tendrá acceso de administrador del sistema a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El nombre real de la cuenta es **NT AUTHORITY\LOCAL SERVICE**.  
  
 <a name="Network_Service"></a> **Cuenta de servicio de red**  
  
 La cuenta de servicio de red es una cuenta integrada que tiene un mayor nivel de acceso a los recursos y a los objetos que los miembros del grupo Usuarios. Los servicios que se ejecutan como cuenta de servicio de red acceden a los recursos de red mediante las credenciales de la cuenta de equipo con el formato _<nombre_dominio>_ **\\** _<nombre_equipo>_ **$** . El nombre real de la cuenta es **NT AUTHORITY\NETWORK SERVICE**.  
  
 <a name="Local_System"></a> **Cuenta de sistema local**  
  
 Sistema local es una cuenta integrada con un alto nivel de privilegios. Tiene amplios privilegios en el sistema local y actúa como el equipo en la red. El nombre real de la cuenta es **NT AUTHORITY\SYSTEM**.  
  
###  <a name="Identify_instance_aware_and_unaware"></a> Identificar los servicios que reconocen y que no reconocen instancias  
 Los servicios que reconocen instancias se asocian a una instancia específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y tienen su propio subárbol del Registro. Puede instalar varias copias de servicios que reconocen instancias mediante la ejecución del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalar cada componente o servicio. Los servicios que no reconocen instancias se comparten entre todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas. No se asocian a una instancia concreta, se instalan solamente una vez y no se pueden instalar en paralelo.  
  
 Entre los servicios que reconocen instancias en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se incluyen los siguientes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
     Tenga en cuenta que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se deshabilita en instancias de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] y [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] con Advanced Services.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] <sup>1</sup>  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Búsqueda de texto completo  
  
 Entre los servicios que no reconocen instancias en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se incluyen los siguientes:  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
  
-   Objeto de escritura de SQL  
  
 <sup>1</sup> Analysis Services en modo integrado de SharePoint se ejecuta como ' PowerPivot ' como una instancia con nombre única. El nombre de instancia es fijo. No puede especificar un nombre diferente. Solamente puede instalar una instancia de Analysis Services que se ejecute como 'PowerPivot' en cada servidor físico.  
  
###  <a name="Localized_service_names"></a> Nombres de servicio traducidos  
 En la tabla siguiente, se muestran los nombres de servicio que se ven en las versiones traducidas de Windows.  
  
|Lenguaje|Nombre de Servicio local|Nombre de Servicio de red|Nombre del sistema local|Nombre del grupo de administradores|  
|--------------|----------------------------|------------------------------|---------------------------|--------------------------|  
|Inglés<br /><br /> Chino simplificado<br /><br /> Chino tradicional<br /><br /> Coreano<br /><br /> Japonés|NT AUTHORITY\LOCAL SERVICE|NT AUTHORITY\NETWORK SERVICE|NT AUTHORITY\SYSTEM|BUILTIN\Administrators|  
|Alemán|NT-AUTORITÄT\LOKALER DIENST|NT-AUTORITÄT\NETZWERKDIENST|NT-AUTORITÄT\SYSTEM|VORDEFINIERT\Administratoren|  
|Francés|AUTORITE NT\SERVICE LOCAL|AUTORITE NT\SERVICE RÉSEAU|AUTORITE NT\SYSTEM|BUILTIN\Administrators|  
|Italiano|NT AUTHORITY\SERVIZIO LOCALE|NT AUTHORITY\SERVIZIO DI RETE|NT AUTHORITY\SYSTEM|BUILTIN\Administrators|  
|Español|NT AUTHORITY\SERVICIO LOC|NT AUTHORITY\SERVICIO DE RED|NT AUTHORITY\SYSTEM|BUILTIN\Administradores|  
|Ruso|NT AUTHORITY\LOCAL SERVICE|NT AUTHORITY\NETWORK SERVICE|NT AUTHORITY\SYSTEM|BUILTIN\Администраторы|  
  
## <a name="related-content"></a>Contenido relacionado  
 [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
 [Ubicaciones de archivos para las instancias predeterminadas y con nombre de SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
 [Instalar Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  