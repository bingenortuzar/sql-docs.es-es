---
title: Instalar SQL Server con el recurso compartido de archivos SMB como opción de almacenamiento | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 8b7810b2-637e-46a3-9fe1-d055898ba639
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3242f463e24322921b16a513c1b3a6905965b390
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775338"
---
# <a name="install-sql-server-with-smb-fileshare-as-a-storage-option"></a>Instalar SQL Server con el recurso compartido de archivos SMB como opción de almacenamiento
  A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], las bases de datos del sistema (Master, Model, MSDB y TempDB) y las bases de datos de usuario del [!INCLUDE[ssDE](../../includes/ssde-md.md)] se pueden instalar con el servidor de archivos del Bloque de mensajes del servidor (SMB) como opción de almacenamiento. Esto se aplica tanto a las instalaciones independientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como a las instalaciones de clústeres de conmutación por error (FCI) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Secuencia de archivos no se admite actualmente en un recurso compartido de archivos SMB.  
  
## <a name="installation-considerations"></a>Consideraciones acerca de la instalación  
  
### <a name="smb-file-share-formats"></a>Formatos del recurso compartido de archivos de SMB:  
 Al especificar el recurso compartido de archivos SMB, se admiten los siguientes formatos de la Convención de nomenclatura universal (UNC) para las bases de datos independientes y FCI.  
  
-   \\\NombreDeServidor\NombreDeRecursoCompartido\  
  
-   \\\NombreDeServidor\NombreDeRecursoCompartido  
  
 Para obtener más información acerca de la convención de nomenclatura Universal, consulte [UNC](https://go.microsoft.com/fwlink/?LinkId=245534) (https://go.microsoft.com/fwlink/?LinkId=245534).  
  
 No se permite usar la ruta UNC de bucle invertido (una ruta UNC cuyo nombre de servidor es localhost, 127.0.0.1 o el nombre del equipo local). Como caso especial, tampoco se admite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa el clúster de servidor de archivos que se hospeda en el mismo nodo en que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para evitar esta situación, se recomienda que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el clúster del servidor de archivos se creen en clústeres de Windows independientes.  
  
 Los formatos siguientes de ruta UNC no se admiten:  
  
-   Ruta de acceso de bucle invertido, por ejemplo, \\\localhost\\..\ or \\\127.0.0.1\\...\  
  
-   Recursos compartidos administrativos, por ejemplo \\\nombreDeServidor\x$  
  
-   Otros formatos de ruta de acceso UNC, como \\\\?\x:\  
  
-   Unidades de red asignadas.  
  
### <a name="supported-data-definition-language-ddl-statements"></a>Instrucciones admitidas del lenguaje de definición de datos (DDL)  
 Las instrucciones DDL [!INCLUDE[tsql](../../includes/tsql-md.md)] y los procedimientos almacenados del motor de base de datos siguientes admiten recursos compartidos de archivos de SMB:  
  
1.  [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
2.  [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
3.  [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
4.  [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)  
  
5.  [sp_attach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-db-transact-sql)  
  
6.  [sp_attach_single_file_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql)  
  
### <a name="installation-options"></a>Opción de instalación  
  
-   En la página "Configuración del Motor de base de datos" de la interfaz de usuario de la instalación, en la pestaña "Directorios de datos", establezca el parámetro "Directorio raíz de datos" como \\\fileserver1\share1\".  
  
-   En la instalación desde el símbolo del sistema, especifique "/INSTALLSQLDATADIR" como "\\\fileserver1\share1\".  
  
     A continuación se muestra la sintaxis de ejemplo para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un servidor independiente usando la opción de recurso compartido de archivos de SMB:  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="<StrongPassword>" /INSTALLSQLDATADIR="\\FileServer\Share1\" /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     Para instalar una instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de nodo único con [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], la instancia predeterminada:  
  
    ```  
    setup.exe /q /ACTION=InstallFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'" /FAILOVERCLUSTERNETWORKNAME="<Insert Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /Features=AS,SQL /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /INSTALLSQLDATADIR="\\FileServer\Share1\" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /SQLSYSADMINACCOUNTS="<DomainName\UserName> /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     Para obtener más información sobre el uso de varias opciones de parámetro de línea de comandos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte [instalar SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
## <a name="operating-system-considerations-smb-protocol-vs-includessnoversionincludesssnoversion-mdmd"></a>Consideraciones sobre el sistema operativo (protocolo SMB frente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])  
 Los distintos sistemas operativos Windows tienen diferentes versiones del protocolo SMB y la versión del protocolo SMB es transparente para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A continuación se muestran las ventajas de las distintas versiones del protocolo SMB con respecto a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
|Sistema operativo|Versión del protocolo SMB2|Ventajas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|----------------------|---------------------------|-------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP 2|2.0|Rendimiento mejorado con respecto a las versiones anteriores de SMB.<br /><br /> Durabilidad, que ayuda a recuperarse de problemas temporales de red.|  
|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1, incluido Server Core|2.1|Compatibilidad con MTU grande, lo que beneficia a las transferencias de datos grandes, como operaciones de copia de seguridad y restauración de SQL. Esta capacidad la debe habilitar el usuario. Para obtener más detalles sobre cómo habilitar esta función, vea [Novedades de SMB](https://go.microsoft.com/fwlink/?LinkID=237319) (https://go.microsoft.com/fwlink/?LinkID=237319).<br /><br /> Mejoras significativas en el rendimiento, concretamente para las cargas de trabajo de estilo OLTP de SQL. Estas mejoras de rendimiento necesitan la aplicación de una revisión. Para obtener más información sobre la revisión, vea [esto](https://go.microsoft.com/fwlink/?LinkId=237320) (https://go.microsoft.com/fwlink/?LinkId=237320).|  
|[!INCLUDE[win8srv](../../includes/win8srv-md.md)], incluido Server Core|3.0|Admite conmutación por error transparente de los recursos compartidos de archivos que proporcionan cero tiempo de inactividad sin que sea necesaria la intervención del administrador DBA o del servidor de archivos de SQL en las configuraciones de clúster de servidores de archivos.<br /><br /> Compatibilidad con E/S usando varias interfaces de red simultáneamente, así como tolerancia a errores de interfaz de red.<br /><br /> Compatibilidad con interfaces de red con funciones de RDMA.<br /><br /> Para obtener más información sobre estas características y el bloque de mensajes de servidor, vea [Información general del bloque de mensajes de servidor](https://go.microsoft.com/fwlink/?LinkId=253174) (https://go.microsoft.com/fwlink/?LinkId=253174).<br /><br /> Compatibilidad de la escala del servidor de archivos (SoFS) con disponibilidad continua.|  
|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2, incluido Server Core|3.2|Admite conmutación por error transparente de los recursos compartidos de archivos que proporcionan cero tiempo de inactividad sin que sea necesaria la intervención del administrador DBA o del servidor de archivos de SQL en las configuraciones de clúster de servidores de archivos.<br /><br /> Compatibilidad con E/S usando varias interfaces de red simultáneamente, así como tolerancia a errores de interfaz de red, con SMB multicanal.<br /><br /> Compatibilidad con interfaces de red con funciones de RDMA con SMB Direct.<br /><br /> Para obtener más información sobre estas características y el bloque de mensajes de servidor, vea [Información general del bloque de mensajes de servidor](https://go.microsoft.com/fwlink/?LinkId=253174) (https://go.microsoft.com/fwlink/?LinkId=253174).<br /><br /> Compatibilidad de la escala del servidor de archivos (SoFS) con disponibilidad continua.<br /><br /> Optimizado para E/S pequeñas de lectura/escritura aleatoria comunes para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLTP.<br /><br /> Se activa la Unidad de transmisión máxima (MTU) de forma predeterminada, lo que mejora significativamente el rendimiento en las transferencias secuenciales grandes como el almacenamiento de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la copia de seguridad o restauración de la base de datos.|  
  
## <a name="security-considerations"></a>Consideraciones de seguridad  
  
-   La cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la cuenta de servicio del agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben tener permisos de recurso compartido CONTROL TOTAL y permisos NTFS en las carpetas de recursos compartidos SMB. Si se usa un servidor de archivos SMB, la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ser una cuenta de dominio o una cuenta del sistema. Para obtener más información sobre los permisos NTFS y de uso compartido, vea [Permisos NTFS y de uso compartido en un servidor de archivos](https://go.microsoft.com/fwlink/?LinkId=245535) (https://go.microsoft.com/fwlink/?LinkId=245535).  
  
    > [!NOTE]  
    >  Los permisos de recursos compartidos y los permisos NTFS FULL CONTROL en las carpetas de recursos compartidos SMB deben limitarse a la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los usuarios de windows con roles de servidor de administración.  
  
     Se recomienda usar una cuenta de dominio como cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si la cuenta del sistema se emplea como cuenta de servicio, conceda permisos para la cuenta de equipo con el siguiente formato: _<nombre_de_dominio>_ **\\** _<nombre_de_equipo>_ **$** .  
  
    > [!NOTE]  
    >  -   Durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es necesario especificar la cuenta de dominio como una cuenta de servicio si el recurso compartido de archivos de SMB se especifica como opción de almacenamiento. Con el recurso compartido de archivos de SMB, la cuenta del sistema solo se puede especificar como una cuenta de servicio después de la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
    > -   Las cuentas virtuales no se pueden autenticar en una ubicación remota. Todas las cuentas virtuales usan el permiso de la cuenta del equipo. Aprovisione la cuenta de equipo con el formato _<nombre_dominio>_ **\\** _<nombre_equipo>_ **$** .  
  
-   La cuenta usada para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener permisos CONTROL TOTAL en la carpeta de recurso compartido de archivos de SMB empleada como directorio de datos, o cualquier otra carpeta de datos (directorio de la base de datos de usuario, directorio de registro de la base de datos de usuario, directorio de TempDB, directorio de registro de TempDB, directorio de copia de seguridad) durante la instalación del clúster.  
  
-   Al a cuenta que se usa para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se le debe conceder los privilegios SeSecurityPrivilege en el servidor de archivos SMB. Para ello, use la consola Directiva de seguridad local del servidor de archivos para agregar la cuenta de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la directiva Administrar registro de seguridad y auditoría. Esta opción está disponible en la sección Asignaciones de derechos de usuario bajo Directivas locales en la consola Directiva de seguridad local.  
  
## <a name="known-issues"></a>Problemas conocidos  
  
-   Después de separar una base de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que reside en el almacenamiento conectado a la red, pueden surgir problemas con los permisos de base de datos al intentar volver a adjuntar la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El problema se define en [este artículo de KB](https://go.microsoft.com/fwlink/?LinkId=237321) (https://go.microsoft.com/fwlink/?LinkId=237321). Para conocer una solución alternativa a este problema, vea la sección **Más información** del artículo de KB.  
  
-   Algunos sistemas de terceros, como en el caso de dispositivos de NetApp, no admiten todas las llamadas API de SQL Server. Con estos podría obtener:   
    2015-06-04 13:14:19.97 spid9s Error: 17053, Severity: 16, estado: 1.  
    2015-06-04 13:14:19.97 spid9s      DoDevIoCtlOut() GetOverlappedResult() : Sistema operativo encontrado un error 1 (función incorrecta.).  
  
     En el caso de NTFS, el error resulta inofensivo;  en el de ReFS, por el contrario, puede provocar una degradación significativa del rendimiento.  
  
-   Si se usa un recurso compartido de archivo SMB como opción de almacenamiento para una instancia en clúster de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el registro de diagnóstico del clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede escribirse de forma predeterminada en el recurso compartido de archivo porque la biblioteca DLL de recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carece de permiso de lectura y escritura en el recurso compartido de archivo. Para resolver este problema, intente uno de los métodos siguientes:  
  
    1.  Conceda permisos de lectura y escritura en el recurso compartido de archivo a todos los objetos de equipo del clúster.  
  
    2.  Establezca la ubicación de los registros de diagnóstico en una ruta de acceso de archivo local. Vea el ejemplo siguiente:  
  
        ```sql  
        ALTER SERVER CONFIGURATION  
        SET DIAGNOSTICS LOG PATH = 'C:\logs';  
        ```  
  
## <a name="see-also"></a>Vea también  
 [Planear una instalación de SQL Server](../../../2014/sql-server/install/planning-a-sql-server-installation.md)   
 [Temas de procedimientos de instalación](../../../2014/sql-server/install/installation-how-to-topics.md)   
 [Configurar los permisos y las cuentas de servicio de Windows](../configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
