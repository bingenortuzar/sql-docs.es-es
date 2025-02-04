---
title: Archivo de configuración RSReportServer | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 60e0a0b2-8a47-4eda-a5df-3e5e403dbdbc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1939e3b1f09e6afbc63ba0565e244e66a7cff26f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103229"
---
# <a name="rsreportserver-configuration-file"></a>RSReportServer Configuration File
  El archivo **RsReportServer.config** almacena valores que utiliza el Administrador de informes, el servicio web del servidor de informes y los procesamientos en segundo plano. Todas las aplicaciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se ejecutan dentro de un proceso único que lee la configuración almacenada en el archivo RSReportServer.config. Los servidores de informes de modo nativo y SharePoint usan el archivo RSReportServer.config, pero los dos modos no usan los mismos valores en el archivo de configuración. La versión del modo de SharePoint del archivo es más pequeña porque muchas de las configuraciones del modo de SharePoint se almacenan en las bases de datos de configuración de SharePoint y no en el archivo. En este tema se describe el archivo de configuración predeterminado que se instala en el modo nativo y en el modo de SharePoint, y algunos de los valores y comportamientos importantes que se controlan mediante el archivo de configuración.  
  
 En el modo de SharePoint, el archivo de configuración contiene los valores que se aplican a todas las instancias de aplicación de servicio que se ejecutan en ese equipo. La base de datos de configuración de SharePoint contiene los valores de configuración correspondientes a las aplicaciones de servicio concretas. Los valores que se almacenan en la base de datos de configuración y que se administran a través de las páginas de administración de SharePoint pueden ser diferentes en cada aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 A continuación se muestran los valores en el orden en que aparecen en el archivo de configuración que se instala de forma predeterminada. Para obtener instrucciones sobre cómo editar este archivo, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
 **En este tema:**  
  
-   [Ubicación del archivo](#bkmk_file_location)  
  
-   [Opciones de configuración general (rsreportserver.config)](#bkmk_generalconfiguration)  
  
-   [URLReservations (archivo RSReportServer.config)](#bkmk_URLReservations)  
  
-   [Autenticación (archivo RSReportServer.config)](#bkmk_Authentication)  
  
-   [Servicio (archivo RSReportServer.config)](#bkmk_service)  
  
-   [Configuración General de las extensiones de entrega la interfaz de usuario](#bkmk_ui)  
  
-   [Extensions (archivo RSReportServer.config) de modo nativo](#bkmk_extensions)  
  
    -   [Configuración General de las extensiones de entrega](#bkmk_extensionsgeneral)  
  
        -   [Opciones de configuración de extensión de entrega de recurso compartido de archivos](#bkmk_fileshare_extension)  
  
        -   [Opciones de configuración de extensión de correo electrónico de servidor de informes](#bkmk_email_extension)  
  
        -   [Configuración de extensión de biblioteca de documentos de SharePoint de servidor de informes](#bkmk_documentlibrary_extension)  
  
        -   [Configuración de la extensión de entrega NULL](#bkmk_null_extension)  
  
    -   [Configuración General de las extensiones de entrega la interfaz de usuario](#bkmk_ui)  
  
    -   [Configuración General de las extensiones de representación](#bkmk_rendering)  
  
    -   [Configuración General de las extensiones de datos](#bkmk_data)  
  
    -   [Configuración General de las extensiones de consultas semánticas](#bkmk_semantic)  
  
    -   [Configuración de generación de modelos](#bkmk_model)  
  
    -   [Configuración de la extensión de seguridad](#bkmk_security)  
  
    -   [Configuración de la extensión de autenticación](#bkmk_authentication)  
  
    -   [Procesamiento de eventos](#bkmk_eventprocessing)  
  
    -   [Personalización de definición de informe](#bkmk_reportdefinition)  
  
    -   [RDLSandboxing](#bkmk_rdlsandboxing)  
  
-   [MapTileServerConfiguration (archivo RSReportServer.config)](#bkmk_MapTileServer)  
  
-   [Archivo de configuración predeterminado para un servidor de informes de modo nativo](#bkmk_nativedefaultfile)  
  
-   [Archivo de configuración predeterminado para un servidor de informes de modo de SharePoint](#bkmk_sharepointdefaultfile)  
  
##  <a name="bkmk_file_location"></a> Ubicación del archivo  
  
-   El archivo RSReportServer.config se encuentra en las siguientes carpetas, según el modo del servidor de informes:  
  
     **Servidor de informes de modo nativo:**  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
-   **Servidor de informes de modo de SharePoint:**  
  
    ```  
    C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
    ```  
  
 Para obtener más información sobre cómo editar el archivo, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
##  <a name="bkmk_generalconfiguration"></a> Opciones de configuración general (rsreportserver.config)  
 La tabla siguiente proporciona información sobre las opciones de configuración generales que aparecen en la primera parte del archivo. Los parámetros se presentan en el orden en que aparecen en el archivo de configuración. La última columna de la tabla indica si el valor se aplica a un servidor de informes en modo nativo **(N)** , un servidor de informes en modo de SharePoint **(S)** o ambos.  
  
> [!NOTE]  
>  En este tema, "entero máximo" hace referencia al valor INT_MAX de 2147483647.  Para más información, consulte [Límites de enteros](https://msdn.microsoft.com/library/296az74e\(v=vs.110\).aspx) (https://msdn.microsoft.com/library/296az74e(v=vs.110).aspx).  
  
|Parámetro|Descripción|Modo|  
|-------------|-----------------|----------|  
|**Dsn**|Especifica la cadena de conexión al servidor de base de datos que hospeda la base de datos del servidor de informes. Este valor está cifrado y se agrega al archivo de configuración al crear la base de datos del servidor de informes. Para SharePoint, la información de conexión de la base de datos se toma de la base de datos de configuración de SharePoint.|N,S|  
|**ConnectionType**|Especifica el tipo de credenciales que el servidor de informes utiliza para conectarse a la base de datos del servidor de informes. Los valores válidos son `Default` y `Impersonate`. `Default` se especifica si el servidor de informes se configura para utilizar un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la cuenta de servicio para conectarse con la base de datos del servidor de informes. `Impersonate` se especifica si el servidor de informes usa una cuenta de Windows para conectarse con la base de datos del servidor de informes.|N|  
|**LogonUser, LogonDomain, LogonCred**|Almacena el dominio, el nombre de usuario y la contraseña de una cuenta de dominio utilizada por un servidor de informes para conectarse a una base de datos del servidor de informes. Los valores de `LogonUser`, `LogonDomain` y `LogonCred` se crean cuando la conexión del servidor de informes se ha configurado para utilizar una cuenta de dominio. Para obtener más información sobre la conexión de base de datos del servidor de informes, vea [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).|N|  
|**InstanceID**|Identificador de la instancia de servidor de informes. Los nombres de instancia del servidor de informes se basan en nombres de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este valor especifica un nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . De forma predeterminada, este valor es `MSRS12`  *\<instancename >* . No modifique este parámetro. A continuación, se ofrece un ejemplo del valor completo: `<InstanceId>MSRS12.MSSQLSERVER</InstanceId>`<br /><br /> A continuación, se ofrece un ejemplo del modo de SharePoint:<br /><br /> `<InstanceId>MSRS12.@Sharepoint</InstanceId>`|N,S|  
|**InstallationID**|Identificador para la instalación del servidor de informes que crea el programa de instalación. Este valor se establece en un GUID. No modifique este parámetro.|N|  
|**SecureConnectionLevel**|Especifica el grado en que las llamadas al servicio web deben usar Capa de sockets seguros (SSL). Este valor se utiliza para el servicio web del servidor de informes y el Administrador de informes. Este valor se establece cuando se configura una dirección URL para utilizar HTTP o HTTPS en la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . El intervalo de valores válidos es de 0 a 3, donde 0 es el menos seguro. Para obtener más información, vea [Usar métodos de servicio web seguros](../report-server-web-service/net-framework/using-secure-web-service-methods.md) y [Configurar conexiones SSL en un servidor de informes en modo nativo](../security/configure-ssl-connections-on-a-native-mode-report-server.md).|N,S|  
|**DisableSecureFormsAuthenticationCookie**|El valor predeterminado es False.<br /><br /> Especifica si se deshabilita el forzado de la cookie usada para que la autenticación mediante formularios y personalizada se marquen como seguras. A partir de SQL Server 2012, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] marcará automáticamente las cookies de autenticación de formularios usadas con extensiones de autenticación personalizada como cookies seguras cuando se envíen al cliente. Al cambiar esta propiedad, los administradores del servidor de informes y los autores de extensiones de seguridad personalizadas pueden revertir al comportamiento anterior que permitía al autor de una extensión de seguridad personalizada determinar si se debía marcar la cookie como segura. Se recomienda usar cookies seguras para la autenticación de formularios con el fin de ayudar a evitar ataques de examen de red y reproducción.|N|  
|**CleanupCycleMinutes**|Especifica los minutos tras los que se eliminarán las sesiones antiguas y las instantáneas expiradas de las bases de datos del servidor de informes. El intervalo de valores válidos es de 0 al entero máximo. El valor predeterminado es 10. Si el valor se establece en 0, se deshabilita el proceso de limpieza de la base de datos.|N,S|  
|**MaxActiveReqForOneUser**|Especifica el número máximo de informes que puede procesar a la vez un usuario. Una vez alcanzado el límite, se deniegan las demás solicitudes de procesamiento de informes. Los valores válidos son de 1 al entero máximo. El valor predeterminado es 20.<br /><br /> Tenga en cuenta que la mayoría de las solicitudes se procesan con mucha rapidez, por lo que no es probable que un solo usuario tenga más de 20 conexiones abiertas al mismo tiempo. Si los usuarios abren más de 15 informes con un uso intensivo de procesos al mismo tiempo, puede que sea necesario aumentar este valor.<br /><br /> Este parámetro se omite en el caso de los servidores de informes que se ejecutan en el modo integrado de SharePoint.|N,S|  
|**DatabaseQueryTimeout**|Especifica los segundos de tiempo de espera de la conexión con la base de datos del servidor de informes. Este valor se pasa a la propiedad System.Data.SQLClient.SQLCommand.CommandTimeout. Los valores válidos oscilan entre 0 y 2147483647. El valor predeterminado es 120. Un valor de 0 especifica un tiempo de espera ilimitado y, por consiguiente, no se recomienda.|N|  
|**AlertingCleanupCycleMinutes**|El valor predeterminado es 20.<br /><br /> Determina la frecuencia con la que se limpian los datos temporales almacenados en la base de datos de alertas.|S|  
|**AlertingDataCleanupMinutes**|El valor predeterminado es 360.<br /><br /> Determina durante cuánto tiempo se conservan los datos de sesión usados para crear o editar una definición de alerta dentro de la base de datos de alertas. El valor predeterminado es 6 horas.|S|  
|**AlertingExecutionLogCleanup**Minutes|El valor predeterminado es 10080.<br /><br /> Determina durante cuánto tiempo se conservan los valores del registro de ejecución de alertas. El valor predeterminado es 7 días.|S|  
|**AlertingMaxDataRetentionDays**|El valor predeterminado es 180.<br /><br /> Determina durante cuánto tiempo se conservan los datos de alerta necesarios para evitar mensajes de alerta duplicados cuando los datos de la alerta no han cambiado.|S|  
|**RunningRequestsScavengerCycle**|Especifica la frecuencia con la que se cancelan las solicitudes huérfanas y expiradas. El valor debe especificarse en segundos. El intervalo de valores válidos es de 0 al entero máximo. El valor predeterminado es 60.|N,S|  
|**RunningRequestsDbCycle**|Especifica la frecuencia con la que el servidor de informes evalúa los trabajos en ejecución para comprobar si han superado los tiempos de espera de ejecución de informes, así como el momento en el que se debe presentar la información del trabajo en curso en la página Administrar trabajos del Administrador de informes. El valor debe especificarse en segundos. Los valores válidos oscilan entre 0 y 2147483647. El valor predeterminado es 60.|N,S|  
|**RunningRequestsAge**|Especifica un intervalo, en segundos, tras el que el estado de un trabajo en ejecución cambia de "nuevo" a "en ejecución". Los valores válidos oscilan entre 0 y 2147483647. El valor predeterminado es 30.|N,S|  
|**MaxScheduleWait**|Especifica los segundos que espera el servicio del servidor de informes de Windows para que el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actualice una programación cuando se solicita la **hora siguiente de ejecución** . Los valores válidos oscilan entre 1 y 60.<br /><br /> En el archivo de configuración predeterminado, MaxScheduleWait se establece en **5**.<br /><br /> Si el servidor de informes no puede encontrar o leer el archivo de configuración, el servidor usa el valor predeterminado 1 para MaxScheduleWait.|N,S|  
|**DisplayErrorLink**|Indica si se muestra un vínculo al sitio de Ayuda y soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] cuando se producen errores. Este vínculo aparece en los mensajes de error. Los usuarios pueden hacer clic en el vínculo para abrir el contenido actualizado de mensajes de error de este sitio. Los valores válidos incluyen `True` (predeterminado) y `False`.|N,S|  
|**WebServiceuseFileShareStorage**|Especifica si se deben almacenar las instantáneas temporales y los informes en caché (creados por el servicio web del servidor de informes para la duración de una sesión de usuario) en el sistema de archivos. Los valores válidos son `True` y `False` (predeterminado). Si el valor se establece en false, los datos temporales se almacenan en la base de datos reportservertempdb.|N,S|  
|**WatsonFlags**|Especifica la cantidad de información que se registra para las condiciones de error que se notifican a [!INCLUDE[msCoName](../../includes/msconame-md.md)].<br /><br /> 0x0430 = volcado completo<br /><br /> 0x0428 = minivolcado<br /><br /> 0x0002 = sin volcado|N,S|  
|**WatsonDumpOnExceptions**|Especifica una lista de excepciones que se van notificar en un registro de errores. Esto resulta útil cuando hay un problema que se repite y desea crear un volcado con información para enviarlo a [!INCLUDE[msCoName](../../includes/msconame-md.md)] para su análisis. La creación de volcados afecta al rendimiento, por lo que solo debe cambiar esta configuración al diagnosticar un problema.|N,S|  
|**WatsonDumpExcludeIfContainsExceptions**|Especifica una lista de excepciones que no se van notificar en un registro de errores. Esto resulta útil cuando se diagnostica un problema y no se desea que el servidor cree volcados para una excepción específica.|N,S|  
  
##  <a name="bkmk_URLReservations"></a> URLReservations (archivo RSReportServer.config)  
 `URLReservations` define el acceso HTTP al servicio web del servidor de informes y al Administrador de informes para la instancia actual. Las direcciones URL se reservan y almacenan en HTTP.SYS al configurar el servidor de informes.  
  
> [!WARNING]  
>  En el modo de SharePoint, las reservas de direcciones URL se configuran en Administración central de SharePoint. Para más información, consulte [Configurar las asignaciones de acceso alternativas (https://technet.microsoft.com/library/cc263208(office.12).aspx)](https://technet.microsoft.com/library/cc263208\(office.12\).aspx).  
  
 No modifique directamente las reservas de URL en el archivo de configuración. Utilice siempre el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o el proveedor WMI del servidor de informes para crear o modificar las reservas de URL para un servidor de informes de modo nativo. Si modifica los valores del archivo de configuración, puede dañar la reserva, lo que producirá errores de servidor en tiempo de ejecución o dejará reservas huérfanas en HTTP.SYS que no se quitan si desinstala el software. Para obtener más información, vea [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md) y [Direcciones URL en archivos de configuración &#40;Administrador de configuración de SSRS&#41;](../install-windows/urls-in-configuration-files-ssrs-configuration-manager.md).  
  
 `URLReservations` es un elemento opcional. Si no se incluye en el archivo RSReportServer.config, puede que el servidor no esté configurado. Si se especifica, se requieren todos los elementos secundarios salvo los de `AccountName`.  
  
 La última columna de la tabla indica si el valor se aplica a un servidor de informes de modo nativo (N), un servidor de modo de SharePoint (S) o ambos.  
  
|Parámetro|Descripción|Modo|  
|-------------|-----------------|----------|  
|**Aplicación**|Contiene la configuración para las aplicaciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|N|  
|**Name**|Especifica las aplicaciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Los valores válidos son ReportServerWebService o ReportManager.|N|  
|**VirtualDirectory**|Especifica el nombre del directorio virtual de la aplicación.|N|  
|**URLs, URL**|Contiene una o más reservas de URL para la aplicación.|N|  
|**UrlString**|Especifica la sintaxis de URL que es válida para HTTP.SYS. Para obtener más información sobre la sintaxis, vea [Sintaxis de reserva de direcciones URL &#40;Administrador de configuración de SSRS&#41;](../install-windows/url-reservation-syntax-ssrs-configuration-manager.md).|N|  
|`AccountSid`|Especifica el identificador de seguridad (SID) de la cuenta para la que se creó la reserva de direcciones URL. Ésta debería ser la cuenta en la que se ejecuta el servicio del servidor de informes. Si el SID no coincide con el de la cuenta de servicio, es posible que el servidor de informes no pueda escuchar las solicitudes de dicha dirección URL.|N|  
|`AccountName`|Especifica un nombre de cuenta legible que corresponde a `AccountSid`. No se utiliza, pero aparece en el archivo para poder determinar con facilidad la cuenta de servicio de la cuenta que se utiliza para la reserva de direcciones URL.|N|  
  
##  <a name="bkmk_Authentication"></a> Authentication (archivo RSReportServer.config)  
 `Authentication` especifica uno o más tipos de autenticación aceptados por el servidor de informes. La configuración predeterminada es un subconjunto de la configuración posible para esta sección. Solo se agrega automáticamente la configuración predeterminada. Para agregar otros valores, debe utilizar un editor de texto para agregar la estructura de los elementos al archivo RSReportServer.config y establecer los valores.  
  
 Los valores predeterminados incluyen `RSWindowsNegotiate` y `RSWindowsNTLM` con `EnableAuthPersistance` establecido en `True`:  
  
```  
   <Authentication>  
      <AuthenticationTypes>  
         <RSWindowsNegotiate/>  
         <RSWindowsNTLM/>  
      </AuthenticationTypes>  
      <EnableAuthPersistence>true</EnableAuthPersistence>  
   </Authentication>  
```  
  
 Los valores restantes deben agregarse manualmente. Para obtener más información y ejemplos, consulte [Autenticación con el servidor de informes](../security/authentication-with-the-report-server.md).  
  
 La última columna de la tabla siguiente indica si el valor se aplica a un servidor de informes de modo nativo (N), un servidor de modo de SharePoint (S) o ambos.  
  
|Parámetro|Descripción|Modo|  
|-------------|-----------------|----------|  
|**AuthenticationTypes**|Especifica uno o más tipos de autenticación. Los valores válidos son: `RSWindowsNegotiate`, `RSWindowsKerberos`, `RSWindowsNTLM`, `RSWindowsBasic` y `Custom`.<br /><br /> Los tipos `RSWindows` y `Custom` se excluyen mutuamente.<br /><br /> `RSWindowsNegotiate`, `RSWindowsKerberos`, `RSWindowsNTLM` y `RSWindowsBasic` son acumulativos y se pueden utilizar juntos, como se muestra en el ejemplo de valor predeterminado anteriormente en esta sección.<br /><br /> Es necesario especificar varios tipos de autenticación si espera las solicitudes de una variedad de exploradores o aplicaciones cliente que utilizan diferentes tipos de autenticación.<br /><br /> No quite `RSWindowsNTLM`, de lo contrario limitará la compatibilidad del explorador a una parte de los tipos de explorador compatibles. Para obtener más información, consulte [planeamiento para Reporting Services y compatibilidad con exploradores de Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md).|N|  
|`RSWindowsNegotiate`|El servidor de informes acepta tokens de seguridad de Kerberos o NTLM. Esta es la configuración predeterminada cuando el servidor de informes se ejecuta en modo nativo y la cuenta de servicio es de tipo Servicio de red. Dicha configuración se omite cuando el servidor de informes se ejecuta en modo nativo y la cuenta de servicio está configurada como cuenta de usuario de dominio.<br /><br /> Si se ha configurado una cuenta de dominio para la cuenta de servicio del servidor de informes y no se ha configurado un Nombre principal de servicio (SPN) para el servidor de informes, puede que esta configuración impida a los usuarios iniciar sesión en el servidor.|N|  
|`RSWindowsNTLM`|El servidor acepta los tokens de seguridad NTLM.<br /><br /> Si elimina esta configuración, la compatibilidad de explorador de algunos de los tipos de explorador admitidos será limitada. Para obtener más información, consulte [planeamiento para Reporting Services y compatibilidad con exploradores de Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md).|N, S|  
|`RSWindowsKerberos`|El servidor acepta los tokens de seguridad de Kerberos.<br /><br /> Utilice esta configuración o RSWindowsNegotiate cuando use la autenticación Kerberos en un esquema de autenticación de delegación restringida.|N|  
|`RSWindowsBasic`|El servidor acepta las credenciales básicas y emite un desafío/respuesta si se realiza una conexión sin credenciales.<br /><br /> La autenticación básica pasa las credenciales de las solicitudes HTTP en texto no cifrado. Si utiliza la autenticación básica, use SSL para cifrar el tráfico de red hacia y desde el servidor de informes. Si quiere consultar una sintaxis de configuración de ejemplo para la autenticación básica en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Autenticación con el servidor de informes](../security/authentication-with-the-report-server.md).|N|  
|`Custom`|Especifique este valor si implementó una extensión de seguridad personalizada en el equipo del servidor de informes. Para obtener más información, vea [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md).|N|  
|**LogonMethod**|Este valor especifica el tipo de inicio de sesión para `RSWindowsBasic`. Si especifica `RSWindowsBasic`, este valor es obligatorio. Los valores válidos son 2 ó 3, donde cada valor representa lo siguiente:<br /><br /> `2`: servidores de alto rendimiento de inicio de sesión de red para autenticar las contraseñas de texto simple.<br /><br /> `3`: inicio de sesión con texto no cifrado, que conserva las credenciales de inicio de sesión en el paquete de autenticación que se envía con cada solicitud HTTP. Esto permite que el servidor suplante al usuario a la hora de establecer la conexión con otros servidores de la red.<br /><br /> Nota: Los valores 0 (para el inicio de sesión interactivo) y 1 (para el inicio de sesión por lotes) no se admiten en [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].|N|  
|**Realm**|Este valor se utiliza para `RSWindowsBasic`. Especifica una partición de recurso que incluye características de autorización y de autenticación que se utilizan para controlar el acceso a los recursos protegidos de su organización.|N|  
|**DefaultDomain**|Este valor se utiliza para `RSWindowsBasic`. Se usa para determinar el dominio que utiliza el servidor para autenticar al usuario. Este valor es opcional, pero si lo omite, el servidor de informes utilizará el nombre de equipo como dominio. Si instaló el servidor de informes en un controlador de dominio, el dominio que se utilizará será el controlado por el equipo .|N|  
|**RSWindowsExtendedProtectionLevel**|El valor predeterminado es **off**. Para obtener más información, vea [Extended Protection for Authentication with Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md).|N|  
|**RSWindowsExtendedProtectionScenario**|El valor predeterminado es **Proxy**.|N|  
|**EnableAuthPersistence**|Determina si la autenticación se realiza en la conexión o para cada solicitud.<br /><br /> Los valores válidos son `True` (predeterminado) o `False`. Si se establece en `True`, las solicitudes subsiguientes de la misma conexión asumen el contexto de suplantación de la primera solicitud.<br /><br /> Este valor debe establecerse en `False` si utiliza el software del servidor proxy (como ISA Server) para tener acceso al servidor de informes. Utilizar un servidor proxy permite una conexión única del servidor proxy que van a utilizar varios usuarios. Para este escenario debería deshabilitar la persistencia de autenticación con el fin de que cada solicitud de usuario se pueda autenticar por separado. Si no establece **EnableAuthPersistence** a `False`, todos los usuarios se conectarán mediante el contexto de suplantación de la primera solicitud.|N,S|  
  
##  <a name="bkmk_service"></a> Service (archivo RSReportServer.config)  
 `Service` especifica los valores de aplicación que se aplican al servicio en su conjunto.  
  
 La última columna de la tabla siguiente indica si el valor se aplica a un servidor de informes de modo nativo (N), un servidor de modo de SharePoint (S) o ambos.  
  
|Parámetro|Descripción|Modo|  
|-------------|-----------------|----------|  
|**IsSchedulingService**|Especifica si el servidor de informes mantiene un conjunto de trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondientes a las programaciones y las suscripciones creadas por usuarios de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Los valores válidos incluyen `True` (predeterminado) y `False`.<br /><br /> Este valor se ve afectado si se habilitan o deshabilitan características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando la faceta Configuración de área expuesta para Reporting Services de Administración basada en directivas. Para obtener más información, vea [Iniciar y detener el servicio del servidor de informes](start-and-stop-the-report-server-service.md).|N,S|  
|**IsNotificationService**|Especifica si el servidor de informes procesa notificaciones y entregas. Los valores válidos incluyen `True` (predeterminado) y `False`. Cuando el valor es `False`, no se entregan suscripciones.<br /><br /> Este valor se ve afectado si se habilitan o deshabilitan características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando la faceta Configuración de área expuesta para Reporting Services de Administración basada en directivas. Para obtener más información, vea [Iniciar y detener el servicio del servidor de informes](start-and-stop-the-report-server-service.md).|N,S|  
|**IsEventService**|Especifica si el servicio debe procesar o no los eventos de la cola de eventos. Los valores válidos incluyen `True` (predeterminado) y `False`. Cuando el valor es `False`, el servidor de informes no realiza operaciones para programaciones o suscripciones.<br /><br /> Este valor se ve afectado si se habilitan o deshabilitan características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando la faceta Configuración de área expuesta para Reporting Services de Administración basada en directivas. Para obtener más información, vea [Iniciar y detener el servicio del servidor de informes](start-and-stop-the-report-server-service.md).|N,S|  
|**IsAlertingService**|El valor predeterminado es `True`|S|  
|**PollingInterval**|Especifica el intervalo, en segundos, entre los sondeos de la tabla de eventos realizados por el servidor de informes. El intervalo de valores válidos es de 0 al entero máximo. El valor predeterminado es 10.|N,S|  
|**WindowsServiceUseFileShareStorage**|Especifica si se deben almacenar las instantáneas temporales y los informes en caché (creados por el servicio del servidor de informes para la duración de una sesión de usuario) en el sistema de archivos. Los valores válidos son `True` y `False` (predeterminado).|N,S|  
|`MemorySafetyMargin`|Especifica un porcentaje de `WorkingSetMaximum` que define el límite entre el los escenarios de presión media y baja. El valor predeterminado es 80. Para obtener más información acerca de `WorkingSetMaximum` y configuración de memoria disponible, vea [configurar la memoria disponible para las aplicaciones de servidor de informes](../report-server/configure-available-memory-for-report-server-applications.md).|N,S|  
|**MemoryThreshold**|Especifica un porcentaje de `WorkingSetMaximum` que define el límite entre los escenarios de presión alta y media. El valor predeterminado es **90**. Este valor debería ser mayor que el valor establecido para `MemorySafetyMargin`. Para obtener más información, vea [Configurar la memoria disponible para las aplicaciones del servidor de informes](../report-server/configure-available-memory-for-report-server-applications.md).|N,S|  
|**RecycleTime**|Especifica un tiempo de reciclamiento para el dominio de aplicación, indicado en minutos. El intervalo de valores válidos es de 0 al entero máximo. El valor predeterminado es 720.|N,S|  
|**MaxAppDomainUnloadTime**|Especifica un intervalo en el que se permite la descarga del dominio de aplicación durante una operación de reciclaje. Si el reciclaje no se completa durante este período, se detiene todo el procesamiento en el dominio de aplicación. Para obtener más información, vea [Application Domains for Report Server Applications](application-domains-for-report-server-applications.md).<br /><br /> El valor debe especificarse en minutos. El intervalo de valores válidos es de 0 al entero máximo. El valor predeterminado es **30**.|N,S|  
|**MaxQueueThreads**|Especifica el número de subprocesos que utiliza el servicio Servidor de informes de Windows para el procesamiento simultáneo de suscripciones y notificaciones. El intervalo de valores válidos es de 0 al entero máximo. El valor predeterminado es 0. Si elige 0, el servidor de informes determinará el número máximo de subprocesos. Si especifica un entero, el valor especificado establecerá el límite máximo de subprocesos que se pueden crear a la vez. Para obtener más información sobre la forma en que el servicio Servidor de informes de Windows administra la memoria para los procesos en ejecución, vea [Configurar la memoria disponible para las aplicaciones del servidor de informes](../report-server/configure-available-memory-for-report-server-applications.md).|N,S|  
|**UrlRoot**|Lo utilizan las extensiones de entrega del servidor de informes para crear direcciones URL que utilizan los informes enviados por correo electrónico y las suscripciones a recursos compartidos de archivos. El valor debe ser una dirección URL válida al servidor de informes desde el que se tiene acceso al informe publicado. Lo utiliza el servidor de informes para generar direcciones URL para el acceso sin conexión o desatendido. Estas direcciones URL se utilizan en los informes exportados y por parte de las extensiones de entrega para crear una dirección URL que se incluye en los mensajes de entrega como los vínculos en correos electrónicos. El servidor de informes determina las direcciones URL de los informes en función del comportamiento siguiente:<br /><br /> Si **UrlRoot** está en blanco (el valor predeterminado) y hay reservas de direcciones URL, el servidor de informes determina automáticamente las direcciones URL de la misma forma en que estas se generan para el método ListReportServerUrls. Se utiliza la primera dirección URL que devuelve el método ListReportServerUrls. Sin embargo, si SecureConnectionLevel es mayor que cero (0), se utiliza la primera dirección URL de SSL.<br /><br /> Si **UrlRoot** se ha establecido en un valor específico, se utiliza el valor explícito.<br /><br /> Si **UrlRoot** está en blanco y no se han configurado reservas de direcciones URL, las direcciones URL usadas en informes representados y en vínculos de correo electrónico son incorrectas.|N,S|  
|**UnattendedExecutionAccount**|Especifica un nombre de usuario, una contraseña y un dominio que utiliza el servidor de informes para ejecutar un informe. Estos valores están cifrados. Use la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o la utilidad **rsconfig** para establecer estos valores. Para obtener más información, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).<br /><br /> Para el modo de SharePoint, la cuenta de ejecución se establece para una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mediante Administración central de SharePoint. Para obtener más información, vea [Administrar una aplicación de servicio de SharePoint para Reporting Services](../manage-a-reporting-services-sharepoint-service-application.md).|N|  
|**PolicyLevel**|Especifica el archivo de configuración de la directiva de seguridad. El valor válido es Rssrvrpolicy.config. Para obtener más información, vea [Using Reporting Services Security Policy Files](../extensions/secure-development/using-reporting-services-security-policy-files.md).|N,S|  
|**IsWebServiceEnabled**|Especifica si el servicio web del servidor de informes responde a las solicitudes de acceso de SOAP y dirección URL. Se establece este valor al habilitar o deshabilitar el servicio utilizando la faceta Configuración de área expuesta para Reporting Services en Administración basada en directivas.|N,S|  
|**IsReportManagerEnabled**|Especifica si la aplicación Administrador de informes está disponible en el servidor de informes. Los valores válidos son `True` (predeterminado) y `False`. Si el valor se establece en `True`, el Administrador de informes está disponible. Tenga en cuenta que todavía debe configurar una reserva de direcciones URL para el Administrador de informes antes de poder utilizarlo.|N|  
|**FileShareStorageLocation**|Especifica una sola carpeta en el sistema de archivos para almacenar instantáneas temporales. Aunque se puede especificar la ruta de carpeta como una ruta de acceso UNC, no es recomendable. El valor predeterminado está vacío.<br /><br /> `<FileShareStorageLocation>`<br /><br /> `<Path>`<br /><br /> `</Path>`<br /><br /> `</FileShareStorageLocation>`|N,S|  
|**IsRdceEnabled**|Especifica si está habilitada la extensión de personalización de definición de informe (Report Definition Customization Extension, RDCE). Los valores válidos son `True` y `False`.|N,S|  
  
##  <a name="bkmk_UI"></a> UI (archivo RSReportServer.config)  
 `UI` especifica la configuración que se establece para la aplicación Administrador de informes.  
  
 La última columna de la tabla siguiente indica si el valor se aplica a un servidor de informes de modo nativo (N), un servidor de modo de SharePoint (S) o ambos.  
  
|Parámetro|Descripción|Modo|  
|-------------|-----------------|----------|  
|**ReportServerUrl**|Especifica la URL del servidor de informes a la que se conecta el Administrador de informes. Solo modifique este valor si configura el Administrador de informes para conectarse a un servidor de informes en otra instancia o en un equipo remoto. Para obtener más información, vea [Configurar el Administrador de informes &#40;modo nativo&#41;](configure-web-portal.md).|N,S|  
|**ReportBuilderTrustLevel**|No modifique este valor; no es configurable. En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y versiones posteriores, el generador de informes se ejecuta solo en `FullTrust`. Para obtener más información, vea [Configurar el acceso al Generador de informes](configure-report-builder-access.md) . Para obtener más información sobre cómo interrumpir el modo de confianza parcial, consulte [funcionalidad no incluida en SQL Server Reporting Services en SQL Server 2014](../discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md).|N,S|  
|`PageCountMode`|Solo para el Administrador de informes, este valor especifica si el servidor calcula un valor de recuento de páginas antes de que se represente el informe o en el momento de verse. Los valores válidos son `Estimate` (predeterminado) y `Actual`. Utilice `Estimate` para calcular la información del recuento de páginas tal y como el usuario ve el informe. Inicialmente, el recuento de páginas está establecido en 2 (para la página actual más una página adicional), pero ajusta hacia arriba conforme el usuario se desplaza por las páginas del informe. Use `Actual` si desea calcular el recuento de páginas antes de mostrar el informe. `Actual` se proporciona para mantener la compatibilidad con versiones anteriores. Tenga en cuenta que si establece `PageCountMode` en `Actual`, debe procesarse todo el informe para obtener un recuento de páginas válido, aumentando el tiempo de espera previo a que se muestre el informe.|N,S|  
  
##  <a name="bkmk_extensions"></a> Extensions (archivo RSReportServer.config) de modo nativo  
 La sección Extensions aparece en el archivo rsreportserver.config **únicamente para los servidores de informes de modo nativo** . La información de extensión para los servidores de informes de modo de SharePoint se almacena en la base de datos de configuración de SharePoint y se configura con aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 `Extensions` especifica la configuración para los módulos extensibles siguientes de una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
-   Extensiones de entrega  
  
-   Extensiones de DeliveryUI  
  
-   Extensiones de representación  
  
-   Extensiones de procesamiento de datos  
  
-   Extensiones de consultas semánticas (solo interno)  
  
-   Extensiones de generación de modelos (solo interno)  
  
-   Extensiones de seguridad  
  
-   Extensiones de autenticación  
  
-   Extensiones de procesamiento de eventos (solo interno)  
  
-   Extensiones de personalización de definición de informe  
  
 Algunas de estas extensiones son estrictamente para uso interno del servidor de informes. No están documentados los valores de configuración para las extensiones exclusivamente de uso interno. Las secciones siguientes describen la configuración para las extensiones predeterminadas. Si utiliza un servidor de informes que tenga extensiones personalizadas, puede que sus archivos de configuración contengan valores que no se describen aquí. Esta sección muestra las extensiones en el orden en que aparecen. Las configuraciones que aparecen repetidamente para varias instancias del mismo tipo de extensión se describen solo una vez.  
  
###  <a name="bkmk_extensionsgeneral"></a> Configuración general de las extensiones de entrega  
 Especifica las extensiones de entrega predeterminadas, y posiblemente personalizadas, que se utilizan para entregar informes mediante suscripciones. El archivo RSReportServer.config incluye la configuración de aplicación para cuatro extensiones de entrega:  
  
1.  Correo electrónico del servidor de informes  
  
2.  Entrega a recursos compartidos de archivos.  
  
3.  Biblioteca de documentos del servidor de informes usada para un servidor de informes que se ejecuta en modo integrado de SharePoint.  
  
4.  Proveedor de entrega NULL usado para cargar previamente la memoria caché de informes.  
  
 Para obtener más información sobre las extensiones de entrega, vea [Suscripciones y entrega &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
 Todas las extensiones de entrega contienen **Extension Name**, **MaxRetries**, **SecondsBeforeRetry**y **Configuration**. Primero se documentan estos valores de configuración compartidos. Las descripciones de los valores específicos de cada extensión se muestran en una segunda tabla.  
  
|Parámetro|Descripción|  
|-------------|-----------------|  
|**Extension Name**|Especifica un ensamblado y un nombre descriptivo de la extensión de entrega. No modifique este valor.|  
|**MaxRetries**|Especifica el número de veces que un servidor de informes reintentará una entrega si se produce un error en el primer intento. El valor predeterminado es 3.|  
|**SecondsBeforeRetry**|Especifica el intervalo de tiempo (en segundos) entre cada reintento. El valor predeterminado es 900.|  
|**Configuración**|Contiene el valor de configuración específico de cada extensión de entrega.|  
  
####  <a name="bkmk_fileshare_extension"></a> Opciones de configuración para de la extensión de entrega a recursos compartidos de archivos  
 La entrega a recursos compartidos de archivos envía un informe exportado a un formato de archivo de aplicación a una carpeta compartida de la red. Para obtener más información, vea [File Share Delivery in Reporting Services](../subscriptions/file-share-delivery-in-reporting-services.md).  
  
|Parámetro|Descripción|  
|-------------|-----------------|  
|**ExcludedRenderFormats**, **RenderingExtension**|Esta configuración se utiliza para excluir de forma intencionada los formatos de exportación que no funcionan correctamente con la entrega a recursos compartidos de archivos. Estos formatos se utilizan normalmente para informes interactivos, vistas previas o la carga previa de la caché de informes. No generan archivos de aplicación que puedan verse fácilmente desde una aplicación de escritorio. Los valores válidos son:<br /><br /> **HTMLOWC**<br /><br /> **RGDI**<br /><br /> **Null**|  
  
####  <a name="bkmk_email_extension"></a> Opciones de configuración de la extensión de correo electrónico del servidor de informes  
 El correo electrónico del servidor de informes utiliza un dispositivo de red SMTP para enviar los informes a las direcciones de correo electrónico. Esta extensión de entrega se debe configurar antes de poderse utilizar. Para obtener más información, consulte [configurar un servidor de informes para la entrega de correo electrónico &#40;SSRS Configuration Manager&#41; ](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) y [entrega por correo electrónico en Reporting Services](../subscriptions/e-mail-delivery-in-reporting-services.md).  
  
|Parámetro|Descripción|  
|-------------|-----------------|  
|**SMTPServer**|Especifica un valor de cadena que indica la dirección de un servidor SMTP remoto o un reenviador. Este valor se requiere para un servicio SMTP remoto. Puede ser una dirección IP, un nombre UNC de un equipo de la intranet corporativa o un nombre de dominio completo.|  
|**SMTPServerPort**|Especifica un valor entero que indica el puerto que utiliza el servicio SMTP para enviar el correo saliente. El puerto 25 se suele utilizar para enviar correo electrónico.|  
|**SMTPAccountName**|Contiene un valor de cadena que asigna un nombre de cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook Express. Puede establecer este valor si el servidor SMTP está configurado para utilizarlo de alguna manera; de lo contrario, puede dejarlo en blanco. Use **De** para especificar una cuenta de correo electrónico usada para enviar informes.|  
|**SMTPConnectionTimeout**|Especifica un valor entero que indica el número de segundos que se esperará a una conexión de socket válida con el servicio SMTP antes de superarse el tiempo de espera. El valor predeterminado es 30 segundos, pero este valor se omite si **SendUsing** está establecido en 2.|  
|**SMTPServerPickupDirectory**|Especifica un valor de cadena que indica el directorio de recogida para el servicio SMTP local. Este valor debe ser una ruta de acceso de carpeta local completa (por ejemplo, d:\rs-emails).|  
|**SMTPUseSSL**|Especifica un valor booleano que se puede establecer para que utilice Capa de sockets seguros (SSL) al enviar un mensaje SMTP a través de la red. El valor predeterminado es 0 (o false). Este parámetro se puede utilizar cuando el elemento **SendUsing** está establecido en 2.|  
|**SendUsing**|Especifica el método que se utilizará para enviar mensajes. Los valores válidos son:<br /><br /> 1 = Envía un mensaje desde el directorio de recogida del servicio SMTP local.<br /><br /> 2 = Envía el mensaje desde el servicio SMTP de la red.|  
|**SMTPAuthenticate**|Especifica un valor entero que indica el tipo de autenticación que se utilizará al enviar mensajes a un servicio SMTP a través de una conexión TCP/IP. Los valores válidos son:<br /><br /> 0 = Sin autenticación.<br /><br /> 1 = (no compatible).<br /><br /> 2 = Autenticación NTLM (NT LanMan). El contexto de seguridad del servicio Servidor de informes de Windows se utiliza para conectarse al servidor SMTP de la red.|  
|**De**|Especifica una dirección de correo electrónico desde la que se envían informes, en el formato *abc@host.xyz* . La dirección aparece en la línea **De** de un mensaje de correo electrónico saliente. Este valor se requiere si se utiliza un servicio SMTP remoto. Debe ser una cuenta de correo electrónico válida que tenga permiso para enviar mensajes.|  
|**EmbeddedRenderFormats, RenderingExtension**|Especifica el formato de representación utilizado para encapsular un informe en el cuerpo de un mensaje de correo electrónico. Las imágenes dentro del informe se incrustan a continuación en el mismo. Los valores válidos son MHTML y HTML4.0.|  
|**PrivilegedUserRenderFormats**|Especifica los formatos de representación que puede seleccionar un usuario para la suscripción a un informe cuando la suscripción se haya habilitado mediante la tarea "Administrar todas las suscripciones". Si no se ha establecido este valor, todos los formatos de representación que no se hayan excluido de forma intencionada estarán disponibles.|  
|**ExcludedRenderFormats, RenderingExtension**|Excluye explícitamente los formatos que no funcionan bien con una extensión de entrega determinada. No se pueden excluir varias instancias de la misma extensión de representación. Si se excluyen varias instancias, se producirá un error cuando el servidor de informes lea el archivo de configuración. De forma predeterminada, las siguientes extensiones se excluyen para la entrega por correo electrónico:<br /><br /> **HTMLOWC**<br /><br /> **Null**<br /><br /> **RGDI**|  
|**SendEmailToUserAlias**|Este valor funciona con **DefaultHostName**.<br /><br /> Cuando **SendEmailToUserAlias** está establecido en `True`, los usuarios que definan suscripciones individuales se especificarán automáticamente como destinatarios del informe. El campo **Para** está oculto. Si este valor es `False`, **a** campo está visible. Establezca este valor en `True` si desea ejercer el máximo control sobre la distribución de informes. Los valores válidos incluyen los siguientes:<br /><br /> `True`= Se usa la dirección de correo electrónico del usuario que crea la suscripción. Este es el valor predeterminado.<br /><br /> `False` = Se puede especificar cualquier dirección de correo electrónico.|  
|**DefaultHostName**|Este valor funciona con **SendEmailToUserAlias**.<br /><br /> Especifica un valor de cadena que indica el nombre de host que se anexará al alias de usuario cuando se haya establecido **SendEmailToUserAlias** en True. Este valor puede ser un nombre del Sistema de nombres de dominio (DNS) o una dirección IP.|  
|**PermittedHosts**|Limita la distribución de informes especificando explícitamente qué hosts pueden recibir entregas por correo electrónico. En **PermittedHosts**, cada host se especifica como un elemento **HostName** , donde el valor es una dirección IP o un nombre DNS.<br /><br /> Los únicos destinatarios válidos son las cuentas de correo electrónico definidas para el host. Si especificó **DefaultHostName**, asegúrese de incluir ese host como elemento **HostName** de **PermittedHosts**. Este valor debe ser uno o varios nombres DNS o direcciones IP. De manera predeterminada, este valor no está establecido. En ese caso, no existen restricciones sobre quién puede recibir informes por correo electrónico.|  
  
####  <a name="bkmk_documentlibrary_extension"></a> Configuración de la extensión de la biblioteca de documentos de SharePoint del servidor de informes  
 La biblioteca de documentos del servidor de informes envía un informe exportado a un formato de archivo de aplicación a una biblioteca de documentos. Esta extensión de entrega solo puede utilizarla un servidor de informes que esté configurado para ejecutarse en modo integrado de SharePoint. Para obtener más información, vea [SharePoint Library Delivery in Reporting Services](../subscriptions/sharepoint-library-delivery-in-reporting-services.md).  
  
|Parámetro|Descripción|  
|-------------|-----------------|  
|**ExcludedRenderFormats, RenderingExtension**|Esta configuración se utiliza para excluir de forma intencionada los formatos de exportación que no funcionan correctamente con la entrega a la biblioteca de documentos. Se excluyen las extensiones de entrega HTMLOWC, RGDI y NULL. Estos formatos se utilizan normalmente para informes interactivos, vistas previas o la carga previa de la caché de informes. No generan archivos de aplicación que puedan verse fácilmente desde una aplicación de escritorio.|  
  
####  <a name="bkmk_null_extension"></a> Configuración de la extensión de entrega NULL  
 El proveedor de entrega NULL se utiliza para cargar previamente la caché con informes generados previamente para cada uno de los usuarios. No hay valores de configuración para esta extensión de entrega. Para más información, vea [Informes almacenados en caché &#40;SSRS&#41;](caching-reports-ssrs.md).  
  
###  <a name="bkmk_ui"></a> Configuración general de las extensiones de la interfaz de usuario de entrega  
 Especifica las extensiones de entrega que contienen un componente de la interfaz de usuario que aparece en las páginas de definición de suscripciones utilizadas al definir cada suscripción en el Administrador de informes. Si crea e implementa una extensión de entrega personalizada que tenga opciones definidas por el usuario y desea utilizar el Administrador de informes, debe registrar la extensión de entrega en esta sección. De forma predeterminada, hay valores de configuración para el correo electrónico del servidor de informes y el recurso compartido de archivos del servidor de informes. Esta sección no incluye los valores para las extensiones de entrega utilizadas únicamente en suscripciones controladas por datos o en páginas de la aplicación de SharePoint.  
  
|Parámetro|Descripción|  
|-------------|-----------------|  
|**DefaultDeliveryExtension**|Esta configuración determina qué extensión de entrega aparece en primer lugar en la lista de tipos de entrega de la página de definición de suscripciones. Esta configuración solo puede contenerla una extensión de entrega. Los valores válidos son `True` o `False`. Cuando este valor se establece en `True`, dicha extensión es la selección predeterminada.|  
|**Configuración**|Especifica las opciones de configuración de una extensión de entrega. Puede establecer un formato de representación predeterminado para cada extensión de entrega. Los valores válidos son los nombres de extensión de representación incluidos en la sección correspondiente del archivo rsreportserver.config.|  
|**DefaultRenderingExtension**|Especifica si una extensión de entrega es el valor predeterminado. La extensión de entrega predeterminada es Correo electrónico del Servidor de informes. Los valores válidos son `True` o `False`. Si más de una extensión contiene un valor de `True`, se considerará que la primera es la predeterminada.|  
  
###  <a name="bkmk_rendering"></a> Configuración general de las extensiones de representación  
 Especifica las extensiones de representación predeterminadas y, posiblemente personalizadas, que se utilizan en la presentación de informes.  
  
 No modifique esta sección a menos que esté implementando una extensión de representación personalizada. Para obtener más información, vea [Implementing a Rendering Extension](../extensions/rendering-extension/implementing-a-rendering-extension.md).  
  
 Entre las extensiones de representación predeterminadas se incluyen las siguientes:  
  
-   XML  
  
-   NULL  
  
-   CSV  
  
-   PDF  
  
-   RGDI  
  
-   HTML4.0  
  
-   MHTML  
  
-   EXCEL  
  
-   RPL  
  
-   IMAGE  
  
 A partir de la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , las representaciones de MHTML y HTML 4.0 contienen de forma predeterminada la siguiente información de configuración de dispositivo para controlar el comportamiento de los tamaños de las visualizaciones de datos.  
  
```  
<DeviceInfo><DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing></DeviceInfo>  
```  
  
 Para obtener más información acerca de la configuración de DeviceInfo, vea lo siguiente:  
  
-   [Configuración de la información del dispositivo MHTML](../html-device-information-settings.md)  
  
-   [Configuración de la información de dispositivo HTML...] /.. / html-dispositivo-información-settings.md)  
  
-   [Configuración de información de dispositivos para las extensiones de representación &#40;Reporting Services&#41;](../device-information-settings-for-rendering-extensions-reporting-services.md)  
  
 Para obtener información sobre los atributos del elemento secundario **\<Extension>** , supeditado a **\<Render>** , consulte lo siguiente:  
  
-   [Personalización de los parámetros de extensión de representación en RSReportServer.Config](../customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
-   [Implementación de una extensión de representación](../extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
 No modifique esta sección a menos que esté implementando una extensión de representación personalizada. Para obtener más información, vea [Implementing a Rendering Extension](../extensions/rendering-extension/implementing-a-rendering-extension.md).  
  
###  <a name="bkmk_data"></a> Configuración general de las extensiones de datos  
 Especifica las extensiones de procesamiento de datos predeterminadas y, posiblemente personalizadas, que se utilizan para procesar consultas. Entre las extensiones de procesamiento de datos predeterminadas se incluyen las siguientes:  
  
-   SQL  
  
-   SQLAZURE  
  
-   SQLPDW  
  
-   OLEDB  
  
-   OLEDB-MD  
  
-   ORACLE  
  
-   ODBC  
  
-   XML  
  
-   SHAREPOINTLIST  
  
-   SAPBW  
  
-   ESSBASE  
  
-   TERADATA  
  
 No modifique esta sección a menos que esté agregando las extensiones de procesamiento de datos personalizadas. Para obtener más información, vea [Implementing a Data Processing Extension](../extensions/data-processing/implementing-a-data-processing-extension.md).  
  
###  <a name="bkmk_semantic"></a> Configuración general de las extensiones de consultas semánticas  
 Especifica la extensión de procesamiento de consultas semánticas que se utiliza para procesar modelos de informe. Las extensiones de procesamiento de consultas semánticas incluidas con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporcionan compatibilidad para los datos relacionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Oracle y los datos multidimensionales de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . No modifique esta sección. El procesamiento de consultas no es extensible.  
  
###  <a name="bkmk_model"></a> Configuración de la generación de modelos  
 Especifica una extensión de generación de modelos utilizada para crear los modelos de informe a partir de un origen de datos compartido que ya está publicado en un servidor de informes. Puede generar los modelos para los datos relacionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Oracle y los orígenes de datos multidimensionales de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . No modifique esta sección. La generación de modelos no es extensible.  
  
###  <a name="bkmk_security"></a> Configuración de extensión de seguridad  
 Especifica el componente de autorización usado por [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Este componente lo usa la extensión de autenticación registrada en el elemento `Authentication` del archivo RSReportServer.config. No modifique esta sección a menos que esté implementando una extensión de autenticación personalizada. Para obtener más información sobre cómo agregar las características de seguridad personalizadas, vea [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md). Para obtener más información acerca de la autorización, vea [Authorization in Reporting Services](../extensions/security-extension/authorization-in-reporting-services.md).  
  
###  <a name="bkmk_authentication"></a> Configuración de extensión de autenticación  
 Especifica las extensiones de autenticación predeterminadas y personalizadas que utiliza el servidor de informes. La extensión predeterminada está basada en la autenticación de Windows. No modifique esta sección a menos que esté implementando una extensión de autenticación personalizada. Para obtener más información sobre la autenticación en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Autenticación de Windows en Reporting Services](../extensions/security-extension/authentication-in-reporting-services.md) y [Autenticación con el servidor de informes](../security/authentication-with-the-report-server.md). Para obtener más información sobre cómo agregar las características de seguridad personalizadas, vea [Implementing a Security Extension](../extensions/security-extension/implementing-a-security-extension.md).  
  
###  <a name="bkmk_eventprocessing"></a> Procesamiento de eventos  
 Especifica los controladores de eventos predeterminados. No modifique esta sección. Esta sección no es extensible.  
  
###  <a name="bkmk_reportdefinition"></a> Personalización de definición de informe  
 Especifica el nombre y el tipo de una extensión personalizada que modifica una definición de informe.  
  
###  <a name="bkmk_rdlsandboxing"></a> RDLSandboxing  
 Especifica un modo del lenguaje RDL (Report Definition Language) que permite detectar y restringir el uso de tipos específicos de recursos de informe por parte de inquilinos individuales en un escenario donde varios inquilinos comparten una única granja de servidores web de servidores de informes. Para más información, consulte [Enable and Disable RDL Sandboxing](../enable-and-disable-rdl-sandboxing.md).  
  
##  <a name="bkmk_MapTileServer"></a> MapTileServerConfiguration (archivo RSReportServer.config)  
 `MapTileServerConfiguration` define la configuración para [!INCLUDE[msCoName](../../includes/msconame-md.md)] servicios Web de Bing Maps que proporciona un fondo de mosaico de un mapa de elemento de informe en un informe publicado en un servidor de informes. Se requieren todos los elementos secundarios.  
  
|Parámetro|Descripción|  
|-------------|-----------------|  
|**MaxConnections**|Especifica el número máximo de conexiones a los servicios web de Bing Maps.|  
|**Timeout**|Especifica el timeout en segundos que debe transcurrir para obtener una respuesta de los servicios web de Bing Maps.|  
|**AppID**|Especifica el identificador de la aplicación (AppID) que se debe usar en los servicios web de Bing Maps. `(Default)` especifica el AppID de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] predeterminado.<br /><br /> Para obtener más información sobre el uso de mosaicos de Bing Maps en un informe, vea [Condiciones adicionales de uso](https://go.microsoft.com/fwlink/?LinkId=151371) y [Declaración de privacidad](https://go.microsoft.com/fwlink/?LinkId=151372).<br /><br /> No modifique este valor a menos que deba especificar un AppID personalizado para su contrato de licencia de Bing Maps. Cuando modifique AppID, no será necesario reiniciar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para que el cambio surta efecto.|  
|**CacheLevel**|Especifica un valor en HttpRequestCacheLevel (Enumeración) de System.Net.Cache. El valor predeterminado es `Default`. Para obtener más información, vea [HttpRequestCacheLevel (Enumeración)](https://go.microsoft.com/fwlink/?LinkId=153353).|  
  
##  <a name="bkmk_nativedefaultfile"></a> Archivo de configuración predeterminada para un servidor de informes de modo nativo  
 El archivo rsreportserver.config se instala en la siguiente ubicación de forma predeterminada:  
  
 **C:\Program Files\Microsoft SQL Server\MSRS12. MSSQLSERVER\Reporting Services\ReportServer**  
  
```  
<Configuration>     <Dsn>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAoyfT3iJKS0qxG3ibhRCYhAQAAAAiAAAAUgBlAHAAbwByAHQAaQBuAGcAIABTAGUAcgB2AGUAcgAAAANmAADAAAAAEAAAADMnIAaBwxRDy2mu4yg0zKAAAAAABIAAAKAAAAAQAAAAX+0WIyZTGyyEE7R8rtmmZegAAAByz0h1aXSAggJLDnVfd1eyGlLqTln9cCff3DQ25pcNBccP2rsLkwokUrS9kcee4up6UOawgKQuQjqWbLXfpqY9Dp/ueDTcF8h+VlSWNCmcH/OlDo7Pt2S6FestlnrmFrUXImx+XPZoeDYQelDUTgy8cHUAgUlD/wW8beboXXcS04QB0uTy2mwtUl5/xAPOGXFOKkXp6w8wqnxkEdVd60WyyppOu7djRf25OBSZn3I4T5dwaORHqPGVJmVGzcagoG5u0hDqtEf2RD4FnJgcAAIRHcqxj+jqOV+ZCVvmDcdBWCsbg5OdvIBEFAAAABi/yAmdbbA2emMyOAFIQ1k0His4</Dsn>     <ConnectionType>Default</ConnectionType>     <LogonUser></LogonUser>     <LogonDomain></LogonDomain>     <LogonCred></LogonCred>     <InstanceId>MSRS12.MSSQLSERVER</InstanceId>     <InstallationID>{6af9ea4c-2593-4dd8-8e2b-6315014c1a52}</InstallationID>     <Add Key="SecureConnectionLevel" Value="0"/>     <Add Key="DisableSecureFormsAuthenticationCookie" Value="false"/>     <Add Key="CleanupCycleMinutes" Value="10"/>     <Add Key="MaxActiveReqForOneUser" Value="20"/>     <Add Key="DatabaseQueryTimeout" Value="120"/>     <Add Key="RunningRequestsScavengerCycle" Value="60"/>     <Add Key="RunningRequestsDbCycle" Value="60"/>     <Add Key="RunningRequestsAge" Value="30"/>     <Add Key="MaxScheduleWait" Value="5"/>     <Add Key="DisplayErrorLink" Value="true"/>     <Add Key="WebServiceUseFileShareStorage" Value="false"/>     <!--  <Add Key="ProcessTimeout" Value="150" /> -->     <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->     <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->     <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->     <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->     <Add Key="WatsonFlags" Value="0x0428"/>     <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException"/>     <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException"/>     <URLReservations>          <Application>               <Name>ReportServerWebService</Name>               <VirtualDirectory>ReportServer</VirtualDirectory>               <URLs>                    <URL>                         <UrlString>http://+:80</UrlString>                         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>                         <AccountName>NT Service\ReportServer</AccountName>                    </URL>               </URLs>          </Application>          <Application>               <Name>ReportManager</Name>               <VirtualDirectory>Reports</VirtualDirectory>               <URLs>                    <URL>                         <UrlString>http://+:80</UrlString>                         <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>                         <AccountName>NT Service\ReportServer</AccountName>                    </URL>               </URLs>          </Application>     </URLReservations>     <Authentication>          <AuthenticationTypes>               <RSWindowsNTLM/>          </AuthenticationTypes>          <RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>          <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>          <EnableAuthPersistence>true</EnableAuthPersistence>     </Authentication>     <Service>          <IsSchedulingService>True</IsSchedulingService>          <IsNotificationService>True</IsNotificationService>          <IsEventService>True</IsEventService>          <PollingInterval>10</PollingInterval>          <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>          <MemorySafetyMargin>80</MemorySafetyMargin>          <MemoryThreshold>90</MemoryThreshold>          <RecycleTime>720</RecycleTime>          <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>          <MaxQueueThreads>0</MaxQueueThreads>          <UrlRoot>          </UrlRoot>          <UnattendedExecutionAccount>               <UserName></UserName>               <Password></Password>               <Domain></Domain>          </UnattendedExecutionAccount>          <PolicyLevel>rssrvpolicy.config</PolicyLevel>          <IsWebServiceEnabled>True</IsWebServiceEnabled>          <IsReportManagerEnabled>True</IsReportManagerEnabled>          <FileShareStorageLocation>               <Path>               </Path>          </FileShareStorageLocation>     </Service>     <UI>          <ReportServerUrl>          </ReportServerUrl>          <PageCountMode>Estimate</PageCountMode>     </UI>     <Extensions>          <Delivery>               <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider,ReportingServicesFileShareDeliveryProvider">                    <MaxRetries>3</MaxRetries>                    <SecondsBeforeRetry>900</SecondsBeforeRetry>                    <Configuration>                         <FileShareConfiguration>                              <ExcludedRenderFormats>                                   <RenderingExtension>HTMLOWC</RenderingExtension>                                   <RenderingExtension>NULL</RenderingExtension>                                   <RenderingExtension>RGDI</RenderingExtension>                              </ExcludedRenderFormats>                         </FileShareConfiguration>                    </Configuration>               </Extension>               <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider,ReportingServicesEmailDeliveryProvider">                    <MaxRetries>3</MaxRetries>                    <SecondsBeforeRetry>900</SecondsBeforeRetry>                    <Configuration>                         <RSEmailDPConfiguration>                              <SMTPServer></SMTPServer>                              <SMTPServerPort>                              </SMTPServerPort>                              <SMTPAccountName>                              </SMTPAccountName>                              <SMTPConnectionTimeout>                              </SMTPConnectionTimeout>                              <SMTPServerPickupDirectory>                              </SMTPServerPickupDirectory>                              <SMTPUseSSL>                              </SMTPUseSSL>                              <SendUsing>2</SendUsing>                              <SMTPAuthenticate>                              </SMTPAuthenticate>                              <From></From>                              <EmbeddedRenderFormats>                                   <RenderingExtension>MHTML</RenderingExtension>                              </EmbeddedRenderFormats>                              <PrivilegedUserRenderFormats>                              </PrivilegedUserRenderFormats>                              <ExcludedRenderFormats>                                   <RenderingExtension>HTMLOWC</RenderingExtension>                                   <RenderingExtension>NULL</RenderingExtension>                                   <RenderingExtension>RGDI</RenderingExtension>                              </ExcludedRenderFormats>                              <SendEmailToUserAlias>True</SendEmailToUserAlias>                              <DefaultHostName>                              </DefaultHostName>                              <PermittedHosts>                              </PermittedHosts>                         </RSEmailDPConfiguration>                    </Configuration>               </Extension>               <Extension Name="Report Server DocumentLibrary" Type="Microsoft.ReportingServices.SharePoint.SharePointDeliveryExtension.DocumentLibraryProvider,ReportingServicesSharePointDeliveryExtension">                    <MaxRetries>3</MaxRetries>                    <SecondsBeforeRetry>900</SecondsBeforeRetry>                    <Configuration>                         <DocumentLibraryConfiguration>                              <ExcludedRenderFormats>                                   <RenderingExtension>HTMLOWC</RenderingExtension>                                   <RenderingExtension>NULL</RenderingExtension>                                   <RenderingExtension>RGDI</RenderingExtension>                              </ExcludedRenderFormats>                         </DocumentLibraryConfiguration>                    </Configuration>               </Extension>               <Extension Name="NULL" Type="Microsoft.ReportingServices.NullDeliveryProvider.NullProvider,ReportingServicesNullDeliveryProvider"/>          </Delivery>          <DeliveryUI>               <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">                    <DefaultDeliveryExtension>True</DefaultDeliveryExtension>                    <Configuration>                         <RSEmailDPConfiguration>                              <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>                         </RSEmailDPConfiguration>                    </Configuration>               </Extension>               <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>          </DeliveryUI>          <Render>               <Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering"/>               <Extension Name="NULL" Type="Microsoft.ReportingServices.Rendering.NullRenderer.NullReport,Microsoft.ReportingServices.NullRendering" Visible="false"/>               <Extension Name="CSV" Type="Microsoft.ReportingServices.Rendering.DataRenderer.CsvReport,Microsoft.ReportingServices.DataRendering"/>               <Extension Name="ATOM" Type="Microsoft.ReportingServices.Rendering.DataRenderer.AtomDataReport,Microsoft.ReportingServices.DataRendering" Visible="false"/>               <Extension Name="PDF" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.PDFRenderer,Microsoft.ReportingServices.ImageRendering"/>               <Extension Name="RGDI" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.RGDIRenderer,Microsoft.ReportingServices.ImageRendering" Visible="false"/>               <Extension Name="HTML4.0" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.Html40RenderingExtension,Microsoft.ReportingServices.HtmlRendering" Visible="false">                    <Configuration>                         <DeviceInfo>                              <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>                         </DeviceInfo>                    </Configuration>               </Extension>               <Extension Name="MHTML" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.MHtmlRenderingExtension,Microsoft.ReportingServices.HtmlRendering">                    <Configuration>                         <DeviceInfo>                              <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>                         </DeviceInfo>                    </Configuration>               </Extension>               <Extension Name="EXCEL" Type="Microsoft.ReportingServices.Rendering.ExcelRenderer.ExcelRenderer,Microsoft.ReportingServices.ExcelRendering" Visible="false"/>               <Extension Name="EXCELOPENXML" Type="Microsoft.ReportingServices.Rendering.ExcelOpenXmlRenderer.ExcelOpenXmlRenderer,Microsoft.ReportingServices.ExcelRendering"/>               <Extension Name="RPL" Type="Microsoft.ReportingServices.Rendering.RPLRendering.RPLRenderer,Microsoft.ReportingServices.RPLRendering" Visible="false" LogAllExecutionRequests="false"/>               <Extension Name="IMAGE" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering"/>               <Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>               <Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>          </Render>          <Data>               <Extension Name="SQL" Type="Microsoft.ReportingServices.DataExtensions.SqlConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.DataExtensions.SqlAzureConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.DataExtensions.SqlDwConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="OLEDB" Type="Microsoft.ReportingServices.DataExtensions.OleDbConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="OLEDB-MD" Type="Microsoft.ReportingServices.DataExtensions.AdoMdConnection,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="ORACLE" Type="Microsoft.ReportingServices.DataExtensions.OracleClientConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="ODBC" Type="Microsoft.ReportingServices.DataExtensions.OdbcConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="XML" Type="Microsoft.ReportingServices.DataExtensions.XmlDPConnection,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SHAREPOINTLIST" Type="Microsoft.ReportingServices.DataExtensions.SharePointList.SPListConnection,Microsoft.ReportingServices.DataExtensions"/>               <Extension Name="SAPBW" Type="Microsoft.ReportingServices.DataExtensions.SapBw.SapBwConnection,Microsoft.ReportingServices.DataExtensions.SapBw"/>               <Extension Name="ESSBASE" Type="Microsoft.ReportingServices.DataExtensions.Essbase.EssbaseConnection,Microsoft.ReportingServices.DataExtensions.Essbase"/>               <Extension Name="TERADATA" Type="Microsoft.ReportingServices.DataExtensions.TeradataConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>          </Data>          <SemanticQuery>               <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>False</EnableMathOpCasting>                    </Configuration>               </Extension>               <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>False</EnableMathOpCasting>                    </Configuration>               </Extension>               <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQLADW.MSSqlAdwSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>False</EnableMathOpCasting>                    </Configuration>               </Extension>               <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>True</EnableMathOpCasting>                         <DisableNO_MERGEInLeftOuters>False</DisableNO_MERGEInLeftOuters>                         <EnableUnistr>False</EnableUnistr>                         <DisableTSTruncation>False</DisableTSTruncation>                    </Configuration>               </Extension>               <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">                    <Configuration>                         <EnableMathOpCasting>True</EnableMathOpCasting>                         <ReplaceFunctionName>oREPLACE</ReplaceFunctionName>                    </Configuration>               </Extension>               <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.QueryExecution.ASSemanticQueryCommand,Microsoft.AnalysisServices.Modeling"/>          </SemanticQuery>          <ModelGeneration>               <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>               <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.Generation.ModelGeneratorExtention,Microsoft.AnalysisServices.Modeling"/>          </ModelGeneration>          <Security>               <Extension Name="Windows" Type="Microsoft.ReportingServices.Authorization.WindowsAuthorization, Microsoft.ReportingServices.Authorization"/>          </Security>          <Authentication>               <Extension Name="Windows" Type="Microsoft.ReportingServices.Authentication.WindowsAuthentication, Microsoft.ReportingServices.Authorization"/>          </Authentication>          <EventProcessing>               <Extension Name="SnapShot Extension" Type="Microsoft.ReportingServices.Library.HistorySnapShotCreatedHandler,ReportingServicesLibrary">                    <Event>                         <Type>ReportHistorySnapshotCreated</Type>                    </Event>               </Extension>               <Extension Name="Timed Subscription Extension" Type="Microsoft.ReportingServices.Library.TimedSubscriptionHandler,ReportingServicesLibrary">                    <Event>                         <Type>TimedSubscription</Type>                    </Event>               </Extension>               <Extension Name="Cache Refresh Plan Extension" Type="Microsoft.ReportingServices.Library.CacheRefreshPlanHandler,ReportingServicesLibrary">                    <Event>                         <Type>RefreshCache</Type>                    </Event>               </Extension>               <Extension Name="Cache Update Extension" Type="Microsoft.ReportingServices.Library.ReportExecutionSnapshotUpdateEventHandler,ReportingServicesLibrary">                    <Event>                         <Type>SnapshotUpdated</Type>                    </Event>               </Extension>          </EventProcessing>     </Extensions>     <MapTileServerConfiguration>          <MaxConnections>2</MaxConnections>          <Timeout>10</Timeout>          <AppID>(Default)</AppID>          <CacheLevel>Default</CacheLevel>     </MapTileServerConfiguration></Configuration>  
```  
  
##  <a name="bkmk_sharepointdefaultfile"></a> Archivo de configuración predeterminada para un servidor de informes de modo de SharePoint  
 El archivo rsreportserver.config se instala en la siguiente ubicación de forma predeterminada:  
  
 **C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\WebServices\Reporting**  
  
```  
<Configuration>  
  <Dsn />  
  <ConnectionType>Default</ConnectionType>  
  <LogonUser>  
  </LogonUser>  
  <LogonDomain>  
  </LogonDomain>  
  <LogonCred>  
  </LogonCred>  
  <InstanceId>MSRS12.@Sharepoint</InstanceId>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="CleanupCycleMinutes" Value="10" />  
  <Add Key="MaxActiveReqForOneUser" Value="20" />  
  <Add Key="AlertingCleanupCycleMinutes" Value="20" />  
  <Add Key="AlertingDataCleanupMinutes" Value="360" />  
  <Add Key="AlertingExecutionLogCleanupMinutes" Value="10080" />  
  <Add Key="AlertingMaxDataRetentionDays" Value="180" />  
  <Add Key="RunningRequestsScavengerCycle" Value="60" />  
  <Add Key="RunningRequestsDbCycle" Value="60" />  
  <Add Key="RunningRequestsAge" Value="30" />  
  <Add Key="MaxScheduleWait" Value="5" />  
  <Add Key="DisplayErrorLink" Value="true" />  
  <Add Key="WebServiceUseFileShareStorage" Value="false" />  
  <!--  <Add Key="ProcessTimeout" Value="150" /> -->  
  <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->  
  <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->  
  <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->  
  <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->  
  <Add Key="WatsonFlags" Value="0x0428" />  
  <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException" />  
  <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException" />  
  <RStrace>  
    <add name="FileName" value="ReportServerService" />  
    <add name="FileSizeLimitMb" value="32" />  
    <add name="KeepFilesForDays" value="14" />  
    <add name="Prefix" value="tid, time" />  
    <add name="TraceListeners" value="file" />  
    <add name="TraceFileMode" value="unique" />  
    <add name="Components" value="all:3" />  
  </RStrace>  
  <URLReservations>  
    <Application>  
      <Name>ReportServerWebService</Name>  
      <VirtualDirectory>ReportServer</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
    <Application>  
      <Name>ReportManager</Name>  
      <VirtualDirectory>Reports</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
  </URLReservations>  
  <Authentication>  
    <AuthenticationTypes>  
      <RSWindowsNTLM />  
    </AuthenticationTypes>  
    <EnableAuthPersistence>true</EnableAuthPersistence>  
  </Authentication>  
  <Service>  
    <IsSchedulingService>True</IsSchedulingService>  
    <IsNotificationService>True</IsNotificationService>  
    <IsEventService>True</IsEventService>  
    <IsAlertingService>True</IsAlertingService>  
    <PollingInterval>10</PollingInterval>  
    <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>  
    <MemorySafetyMargin>80</MemorySafetyMargin>  
    <MemoryThreshold>90</MemoryThreshold>  
    <RecycleTime>720</RecycleTime>  
    <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>  
    <MaxQueueThreads>0</MaxQueueThreads>  
    <UrlRoot>  
    </UrlRoot>  
    <PolicyLevel>rssrvpolicy.config</PolicyLevel>  
    <IsWebServiceEnabled>True</IsWebServiceEnabled>  
    <IsReportManagerEnabled>True</IsReportManagerEnabled>  
    <FileShareStorageLocation>  
      <Path>  
      </Path>  
    </FileShareStorageLocation>  
  </Service>  
  <UI>  
    <ReportServerUrl>  
    </ReportServerUrl>  
    <PageCountMode>Estimate</PageCountMode>  
  </UI>  
  <MapTileServerConfiguration>  
    <MaxConnections>2</MaxConnections>  
    <Timeout>10</Timeout>  
    <AppID>(Default)</AppID>  
    <CacheLevel>Default</CacheLevel>  
  </MapTileServerConfiguration>  
</Configuration>  
```  
  
## <a name="see-also"></a>Vea también  
 [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Configurar la memoria disponible para las aplicaciones del servidor de informes](../report-server/configure-available-memory-for-report-server-applications.md)   
 [Personalizar hojas de estilos para el Visor HTML y el Administrador de informes](../customize-style-sheets-for-html-viewer-and-report-manager.md)   
 [Archivos de configuración de Reporting Services](reporting-services-configuration-files.md)   
 [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
