---
title: Scripting y PowerShell con Reporting Services | Microsoft Docs
ms.date: 09/14/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- Reporting Services, scripting
- scripting [Reporting Services]
ms.assetid: 1ac2646d-ed5a-4436-b18f-2150c33f3d87
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d1a0c969bf5e1964446ac9ffd3d9abe12bb90b89
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893403"
---
# <a name="scripting-and-powershell-with-reporting-services"></a>Secuencias de comandos y PowerShell con Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite una amplia gama de escenarios de desarrollo y administración a través de script, incluida la utilidad de línea de comandos rs.exe, cmdlets de PowerShell para servidores de informes de modo de SharePoint y aprovechando el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modelo de objetos de PowerShell para los modos nativo y SharePoint.  
  
-   Los administradores pueden escribir el script en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para automatizar la manera de implementar y administrar una instalación del servidor de informes. Los administradores también pueden generar y ejecutar scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] que crean, configurar y actualizan una base de datos del servidor de informes. Los administradores también pueden usar las características de script de reproducción y registro en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para automatizar las tareas de mantenimiento rutinarias.  
  
-   Los programadores pueden crear aplicaciones personalizadas que incluyen el script. Puede ejecutar un script que realiza llamadas al servicio web del servidor de informes. Casi cualquier operación que puede escribir en código administrado también se puede escribir en script.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] secuencia de comandos de .NET como lenguaje de secuencia de comandos que puede procesar la utilidad RS.exe, un host de secuencias de comandos que se ejecuta en el servidor de informes.  
  
## <a name="reporting-services-sharepoint-mode-powershell-cmdlets-and-samples"></a>Ejemplos y cmdlets de PowerShell del modo SharePoint de Reporting Services  
 ![Contenido relacionado con PowerShell](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] El modo SharePoint incluye [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] cmdlets para la administración del servidor de informes.  
  
-   [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md) Incluye los ejemplos siguientes:  
  
    -   Crear una aplicación de servicio y un proxy  
  
    -   Revisar y actualizar una extensión de entrega  
  
    -   Obtener y establecer propiedades de la base de datos de la aplicación Reporting Services; por ejemplo, el tiempo de espera de la base de datos  
  
    -   Extensiones de datos de lista  
  
## <a name="reporting-services-object-model-and-powershell-samples"></a>Ejemplos de Powershell y modelo de objetos de Reporting Services  
 ![Contenido relacionado con PowerShell](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")  
  
 PowerShell realiza la llamada al núcleo del modelo de objetos y para la mayor parte válida para los modos SharePoint y nativo; por ejemplo, el trabajo de migración, el trabajo de suscripción y más ejemplos relacionados para las suscripciones funcionan en SQL15.  
  
-   [Use PowerShell para cambiar y enumerar los propietarios de una suscripción de Reporting Services y ejecutar una suscripción](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
-   [Usar PowerShell para crear una máquina virtual de Azure con un servidor de informes en modo nativo](https://msdn.microsoft.com/library/azure/dn449661.aspx).  
  
-   Vea la sección "Obtener acceso a las clases WMI mediante PowerShell" en [Obtener acceso al proveedor WMI de Reporting Services](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  

## <a name="rsexe-scripting-samples"></a>Ejemplos de secuencias de comandos de RS.exe  
  
-   [Script rs.exe para copiar contenido entre servidores de informes de servicios de informes de ejemplo](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
-   Consulte [Muestras de producto de SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889)para obtener más ejemplos de secuencias de comandos, aplicaciones y extensiones.  
  
## <a name="see-also"></a>Consulte también  
 [Utilidad RS.exe &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)   
 [Script para tareas administrativas y de implementación](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
 [Script con la utilidad rs.exe y el servicio Web](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
  
  
