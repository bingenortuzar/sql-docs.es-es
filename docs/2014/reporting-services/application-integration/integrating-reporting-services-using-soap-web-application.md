---
title: Usar la API de SOAP en una aplicación web | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], Web applications
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- report servers [Reporting Services], SOAP
- Web applications [Reporting Services]
ms.assetid: e8ca4455-0dc3-4741-8872-3636114938ad
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5a90135c634e45f3fb4e3ff9c780347caaea24f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126274"
---
# <a name="using-the-soap-api-in-a-web-application"></a>Usar la API SOAP en una aplicación web
  Puede tener acceso a la funcionalidad completa del servidor de informes a través de la API SOAP de Reporting Services. Dado que es un servicio web, se puede tener acceso con facilidad a esta API para proporcionar características de informes de empresa para aplicaciones empresariales personalizadas. Para tener acceso al servicio web del servidor de informes desde una aplicación web, se usa casi el mismo proceso que en el acceso a la API SOAP desde una aplicación para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Con [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], puede generar una clase de proxy que exponga las propiedades y los métodos del servicio web del servidor de informes y le permita usar una infraestructura y herramientas conocidas para compilar las aplicaciones empresariales en la tecnología [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 El acceso a la funcionalidad de administración de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se realiza con tanta facilidad desde una aplicación web como desde una aplicación para Windows. Desde una aplicación web, puede agregar y quitar los elementos de la base de datos del servidor de informes, establecer la seguridad de los elementos, modificar los elementos de la base de datos del servidor de informes, administrar la programación y la entrega, etcétera.  
  
## <a name="enabling-impersonation"></a>Habilitar la suplantación  
 El primer paso para configurar una aplicación web es habilitar la suplantación desde el cliente de servicios web. Con la suplantación, las aplicaciones de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] pueden ejecutarse con la identidad del cliente en cuyo el nombre operan. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] se basa en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) para autenticar al usuario y pasar un token autenticado a la aplicación de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] o, si no se puede autenticar al usuario, pasar un token sin autenticar. En cualquier caso, la aplicación de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] suplanta al token que se reciba, si está habilitada la suplantación. Puede habilitar la suplantación en el cliente modificando el archivo Web.config de la aplicación cliente como sigue:  
  
```  
<!-- Web.config file. -->  
<identity impersonate="true"/>  
```  
  
> [!NOTE]  
>  De manera predeterminada, la suplantación está deshabilitada.  
  
 Para más información sobre la suplantación de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)], vea la documentación del SDK de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
## <a name="managing-the-report-server-using-soap-api"></a>Administrar el servidor de informes mediante la API SOAP  
 También puede utilizar la aplicación web para administrar un servidor de informes y su contenido. El Administrador de informes, que se incluye con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], es un ejemplo de aplicación web que se genera completamente utilizando [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] y la API SOAP de Reporting Services. Puede agregar la funcionalidad de administración de informes del Administrador de informes a sus aplicaciones web personalizadas. Por ejemplo, es posible que desee devolver una lista de los informes disponibles en la base de datos del servidor de informes y mostrarlos en un [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] `Listbox` control para los usuarios elijan. El código siguiente se conecta a la base de datos del servidor de informes y devuelve una lista de los elementos de la base de datos del servidor de informes. A continuación, los informes disponibles se agregan a un control Listbox, que muestra la ruta de acceso de cada informe.  
  
```vb  
Private Sub Page_Load(sender As Object, e As System.EventArgs)  
   ' Create a Web service proxy object and set credentials  
   Dim rs As New ReportingService2005()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return a list of catalog items in the report server database  
   Dim items As CatalogItem() = rs.ListChildren("/", True)  
  
   ' For each report, display the path of the report in a Listbox  
   Dim ci As CatalogItem  
   For Each ci In  items  
      If ci.Type = ItemTypeEnum.Report Then  
         catalogListBox.Items.Add(ci.Path)  
      End If  
   Next ci  
End Sub ' Page_Load   
```  
  
```csharp  
private void Page_Load(object sender, System.EventArgs e)  
{  
   // Create a Web service proxy object and set credentials  
   ReportingService2005 rs = new ReportingService2005();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return a list of catalog items in the report server database  
   CatalogItem[] items = rs.ListChildren("/", true);  
  
   // For each report, display the path of the report in a Listbox  
   foreach(CatalogItem ci in items)  
   {  
      if (ci.Type == ItemTypeEnum.Report)  
         catalogListBox.Items.Add(ci.Path);  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio web y .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Integración de Reporting Services en las aplicaciones](../application-integration/integrating-reporting-services-into-applications.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Usar la API de SOAP en una aplicación Windows](integrating-reporting-services-using-soap-windows-application.md)  
  
  
