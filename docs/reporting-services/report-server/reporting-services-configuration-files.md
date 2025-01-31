---
title: Archivos de configuración de Reporting Services | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b0bd7ad95fcda039c6fd5a9299f4339d35b8a619
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2019
ms.locfileid: "67564131"
---
# <a name="reporting-services-configuration-files"></a>Archivos de configuración de Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] almacena información de componentes en el Registro y en los archivos de configuración que se copian en el sistema de archivos durante la instalación. Los archivos de configuración contienen una combinación de valores solo para uso interno y valores definidos por el usuario. Estos últimos se especifican durante la instalación, mediante herramientas de configuración, con las utilidades de la línea de comandos y mediante la edición manual de los archivos de configuración.  
  
 Solo es necesario modificar los archivos de configuración cuando se agrega o configura la configuración avanzada. Los parámetros de configuración se especifican como atributos o elementos XML. Si comprende XML y los archivos de configuración, puede utilizar un editor de texto o de código para modificar las opciones de configuración definibles por el usuario. Para más información sobre cómo modificar un archivo de configuración o sobre cómo lee el servidor de informes los valores de configuración nuevos y actualizados, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
> [!NOTE]  
> En versiones anteriores, el Administrador de informes tenía su propio archivo de configuración denominado RSWebApplication.config. Ahora ese archivo está obsoleto. Si actualizó desde una instalación anterior, no se eliminará el archivo pero el servidor de informes no leerá ningún valor del mismo. Si el archivo está en su equipo, debe eliminarlo. En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, todas las opciones de configuración del Administrador de informes y del portal web se almacenan y se leen del archivo RSReportServer.config. Para examinar una lista de las configuraciones eliminadas o movidas, vea [Cambios substanciales de SQL Server Reporting Services en SQL Server 2016](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
 En este artículo:  
  
-   [Resumen de archivos de configuración (modo nativo)](#bkmk_config_file_Summary_native_mode)  
  
-   [Resumen de archivos de configuración (modo de SharePoint)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> Resumen de archivos de configuración (modo nativo)  
 La tabla siguiente proporciona una descripción de donde está almacenada la configuración. La mayoría de los parámetros de configuración están almacenados en archivos de configuración que se incluyen con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. De forma predeterminada, el directorio de instalación es el siguiente:  
  
```
Install Paths  
C:\Program Files\Microsoft SQL Server\MSRSxx.MSSQLSERVER  (where xx is the MS SQL version number)
  or  
C:\Program Files\Microsoft SQL Server Reporting Services\SSRS  
  depending on the SSRS version
```  
  
|Se almacena en:|Descripción|Ubicación|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Almacena las opciones de configuración para las áreas de característica del servicio del servidor de informes: el Administrador de informes o el portal web, el servicio web del servidor de informes y el procesamiento en segundo plano. Para obtener más información sobre cada configuración, vea [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Directorio de instalación> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Almacena las directivas de seguridad de acceso del código para las extensiones del servidor. Para obtener más información acerca de este archivo, vea [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Directorio de instalación> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|Almacena las directivas de seguridad de acceso del código para el portal web. Para obtener más información acerca de este archivo, vea [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Directorio de instalación> \Reporting Services \ReportManager|  
|Web.config para el servicio web del servidor de informes.|Incluye solo los valores que se requieren para ASP.NET.|\<Directorio de instalación> \Reporting Services \ReportServer|  
|Web.config del Administrador de informes.|Incluye solo los valores que son necesarios para ASP.NET si es aplicable para la versión SSRS.|\<Directorio de instalación> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|Almacena los parámetros de configuración que especifican los niveles de seguimiento y las opciones de registro para el servicio del servidor de informes. Para obtener más información sobre los elementos de este archivo, vea [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md).|\<Directorio de instalación> \Reporting Services \ReportServer \Bin|  
|Parámetros del Registro|Almacena el estado de la configuración y otras configuraciones utilizadas para desinstalar Reporting Services. Si está solucionando problemas de instalación o de configuración, puede ver estos valores para obtener información sobre cómo se configura el servidor de informes.<br /><br /> No modifique directamente estos valores, ya que podría invalidar su instalación.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<idDeInstancia\> \Setup<br /><br /> **- Y -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|Almacena los parámetros de configuración para el Diseñador de informes. Para obtener más información, consulte [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<unidad>:\Archivos de programa \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
|RSPreviewPolicy.config|Almacena las directivas de seguridad de acceso del código para las extensiones de servidor utilizadas durante la vista previa del informe. Para obtener más información acerca de este archivo, vea [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|C:\Archivos de programa\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> Resumen de archivos de configuración (modo de SharePoint)  
 En la tabla siguiente se proporciona una descripción de los archivos de configuración usados para un servidor de informes en modo de SharePoint. La mayoría de las configuraciones se almacenan en bases de datos de la aplicación de servicio de SharePoint. Para obtener más información, vea [Aplicaciones de servicio y servicio de SharePoint de Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
  
 De forma predeterminada, el directorio de instalación para el modo de SharePoint es el siguiente:  
  
```
Install path
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|Se almacena en:|Descripción|Ubicación|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Almacena las opciones de configuración para las áreas de característica del servicio del servidor de informes: el Administrador de informes o el portal web, el servicio web del servidor de informes y el procesamiento en segundo plano. Para obtener más información sobre cada configuración, vea [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Directorio de instalación> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Almacena las directivas de seguridad de acceso del código para las extensiones del servidor. Para obtener más información acerca de este archivo, vea [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Directorio de instalación> \Reporting Services \ReportServer|  
|Web.config para el servicio web del servidor de informes.|Incluye solo los valores que son necesarios para ASP.NET si es aplicable para la versión SSRS.|\<Directorio de instalación> \Reporting Services \ReportServer|  
|Parámetros del Registro|Almacena el estado de la configuración y otras configuraciones utilizadas para desinstalar Reporting Services. También almacena información sobre cada aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> No modifique directamente estos valores, ya que podría invalidar su instalación.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<idDeInstancia\> \Setup<br /><br /> Identificador de instancia de ejemplo: MSSQL13.MSSQLSERVER<br /><br /> **- Y -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|Almacena los parámetros de configuración para el Diseñador de informes. Para obtener más información, consulte [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<unidad>:\Archivos de programa \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
  
## <a name="see-also"></a>Vea también  
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Extensiones de Reporting Services](../../reporting-services/extensions/reporting-services-extensions.md)   
 [rsconfig (utilidad) &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
 [Inicio y detención del servicio del servidor de informes](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
