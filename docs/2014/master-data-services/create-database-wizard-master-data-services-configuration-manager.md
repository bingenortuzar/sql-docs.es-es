---
title: Asistente Crear base de datos (Administrador de configuración de Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.createdbwiz.f1
ms.assetid: 45fe7a23-a46c-4d40-8bca-3431fbfc5c9d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7207cd8e3a087ed0aa85931254754d4009d73c53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479871"
---
# <a name="create-database-wizard-master-data-services-configuration-manager"></a>Asistente Crear base de datos (Administrador de configuración de Master Data Services)
  Utilice el asistente para **Crear base de datos** con el fin de crear una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
## <a name="database-server"></a>Servidor de bases de datos  
 Especifique la información de conexión a una instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] local o remota para hospedar la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para conectarse a una instancia remota, se debe estar habilitado para realizar conexiones remotas.  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|**Instancia de SQL Server**|Especifique el nombre de la instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que vaya a hospedar a la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Puede ser una instancia predeterminada o con nombre en un equipo local o remoto. Especifique la información, para ello escriba:<br /><br /> Un punto (.) para conectarse a la instancia predeterminada en su equipo local.<br /><br /> El nombre del servidor o dirección IP para conectarse a la instancia predeterminada en el equipo local o remoto especificado.<br /><br /> El nombre del servidor o dirección IP y el nombre de instancia para conectarse a la instancia con nombre en el equipo local o remoto especificado. Especifique esta información en el formato *nombre_servidor*\\*nombre_instancia*.|  
|**Tipo de autenticación**|Seleccione el tipo de autenticación a utilizar en la conexión a la instancia de SQL Server especificada. Las credenciales que utilice para conectarse deben formar parte del rol de servidor **sysadmin** para la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada. Para obtener más información sobre el rol sysadmin, consulte [Roles de nivel de servidor](../relational-databases/security/authentication-access/server-level-roles.md). Entre los tipos de autenticación se incluyen:<br /><br /> **Usuario actual: Seguridad integrada**: usa la autenticación integrada de Windows para la conexión mediante las credenciales de la cuenta de usuario de Windows actual. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] utiliza las credenciales de Windows del usuario que inició sesión en el equipo y abrió la aplicación. No puede especificar unas credenciales de Windows diferentes en la aplicación. Si desea conectarse con credenciales diferentes de Windows, debe iniciar sesión en el equipo como ese usuario y, a continuación, abrir [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].<br /><br /> **Cuenta de SQL Server**: usa una cuenta de SQL Server para la conexión. Al seleccionar esta opción, se habilitan los campos **Nombre de usuario** y **Contraseña** y es preciso que especifique las credenciales para una cuenta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada.|  
|**Nombre de usuario.**|Especifique el nombre de la cuenta de usuario que se utilizará para conectar a la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada. La cuenta debe inscribirse en el rol **sysadmin** en la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada.<br /><br /> Cuando el **Tipo de autenticación** es **Usuario actual: Seguridad integrada**, el cuadro **Nombre de usuario** es de solo lectura y muestra el nombre de la cuenta de usuario de Windows con la que se ha iniciado sesión en el equipo.<br /><br /> Cuando el **Tipo de autenticación** es **Cuenta de SQL Server**, se habilitará el cuadro **Nombre de usuario** y deberá especificar las credenciales para una cuenta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la instancia [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada.|  
|**Contraseña**|Especifique la contraseña asociada a la cuenta de usuario.<br /><br /> Cuando el **Tipo de autenticación** es **Usuario actual: Seguridad integrada**, el cuadro **Contraseña** es de solo lectura y las credenciales de la cuenta de usuario especificada de Windows se usan para conectarse.<br /><br /> Cuando el **Tipo de autenticación** sea **Cuenta de SQL Server**, se habilitará el cuadro **Contraseña** y deberá especificar la contraseña asociada a la cuenta de usuario especificada.|  
|**Probar conexión**|Compruebe que la cuenta de usuario especificada pueda conectar a la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y que la cuenta tenga permiso para crear una base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para esa instancia. Si no hace clic en **Probar conexión**, se probará la conexión cuando haga clic en **Siguiente**.|  
  
## <a name="database"></a>Base de datos  
 Especifique un nombre y las opciones de intercalación para la base de datos nueva. Las intercalaciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporcionan propiedades de distinción entre mayúsculas y minúsculas, acentos y reglas de ordenación para los datos. Las intercalaciones que se utilizan con tipos de datos de caracteres como char y varchar dictan la página de códigos y los caracteres correspondientes que se pueden representar para ese tipo de datos. Para obtener más información sobre la intercalación de base de datos, consulte [Compatibilidad con la intercalación y Unicode](../relational-databases/collations/collation-and-unicode-support.md).  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|**Nombre de la base de datos**|Especifique un nombre para la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Intercalación predeterminada de SQL Server**|Seleccione utilizar el valor de intercalación de la base de datos actual de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada para la base de datos nueva.|  
|**Intercalación de Windows**|Especifique los valores de intercalación de Windows para su uso en la base de datos nueva. Las intercalaciones de Windows definen reglas para almacenar los datos de caracteres basadas en la configuración regional de Windows asociada. Para obtener más información sobre las intercalaciones de Windows y las opciones asociadas, consulte [Nombre de intercalación de Windows &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql).<br /><br /> Nota: La lista **Intercalación de Windows** y las opciones asociadas solo se habilitarán una vez se haya desactivado la casilla **Intercalación predeterminada de SQL Server**.|  
  
## <a name="administrator-account"></a>Cuenta del administrador  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|**Nombre de usuario.**|Especifique una cuenta de usuario de dominio para ser el administrador del sistema de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para todas las [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] aplicaciones Web asociadas con esta base de datos, este usuario pueden actualizar todos los modelos y todos los datos en todas las áreas funcionales. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).|  
  
## <a name="summary"></a>Resumen  
 Muestra un resumen de las opciones seleccionadas. Compruebe sus elecciones y, a continuación, haga clic en **Siguiente** para empezar a crear la base de datos con los valores especificados.  
  
## <a name="progress-and-finish"></a>Progreso y Finalizar  
 Muestra el progreso del proceso de creación. Una vez se haya creado la base de datos, haga clic en **Finalizar** para cerrar el asistente de la base de datos y volver a la página **Bases de datos** . La nueva base de datos se habrá seleccionado y podrá ver y modificar la configuración del sistema.  
  
## <a name="see-also"></a>Vea también  
 [Página Configuración de base de datos &#40;Administrador de configuración de Master Data Services&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Configurar la base de datos y el sitio Web de Master Data Services](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Requisitos de base de datos &#40;Master Data Services&#41;](install-windows/database-requirements-master-data-services.md)  
  
  
