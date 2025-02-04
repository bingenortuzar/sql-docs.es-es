---
title: El rol de SOAP en Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- SOAP [Reporting Services], role in Reporting Services
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: f229c3ef-f2ca-448f-98f1-b8df350b9992
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4e0b418e44436912b5ed1368ad7a316951872266
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62519210"
---
# <a name="the-role-of-soap-in-reporting-services"></a>El rol de SOAP en Reporting Services
  El servicio web del servidor de informes utiliza la mensajería del Protocolo simple de acceso a objetos (SOAP, Simple Object Access Protocol) para enviar comandos basados en texto a través de una red. Estos comandos adoptan la forma de texto XML que se envía a través de World Wide Web utilizando HTTP. Al usar SOAP como protocolo de comunicaciones, el servicio web del servidor de informes permite a las aplicaciones y componentes intercambiar datos con el servidor de informes utilizando una infraestructura abierta y ampliamente aceptada. El estándar SOAP se define en www.w3.org/TR/SOAP.  
  
 Cualquier aplicación cliente puede actuar como cliente SOAP siempre que conozca dicho protocolo y pueda enviar solicitudes SOAP. El Administrador de informes es un cliente SOAP de este tipo. Proporciona una interfaz para la base de datos del servidor de informes en la que se almacenan todos los informes y el contenido relacionado con los informes. Los usuarios finales pueden utilizar la aplicación para explorar y administrar los informes y carpetas en el espacio de nombres del servidor de informes. El Administrador de informes se integra en la infraestructura del servicio web del servidor de informes.  
  
 Un servidor de informes actúa como servidor SOAP, un servicio que conoce SOAP y puede aceptar las solicitudes de los clientes SOAP y crear las respuestas adecuadas. El servidor administra las solicitudes y envía las respuestas codificadas al cliente.  
  
 Los mensajes SOAP en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] adoptan muchas formas diferentes, según el tipo de solicitud que realice el cliente. En el ejemplo siguiente se representa una solicitud de cliente SOAP simple para quitar un elemento de la base de datos del servidor de informes.  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItem xmlns="https://www.microsoft.com/sql/ReportingServer">  
            <item>/Samples/Report1</item>  
        </DeleteItem>  
    </soap:Body>  
</soap:Envelope>  
```  
  
 El propio SOAP requiere que los mensajes se coloquen en un elemento `Envelope`, con la mayoría del mensaje dentro de un elemento `Body`. En este ejemplo, el cuerpo contiene una llamada al método <xref:ReportService2010.ReportingService2010.DeleteItem%2A>, que acepta un parámetro de cadena que representa la ruta de acceso al elemento que se va a eliminar. Puede crear una clase de proxy de cliente de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que encapsule todas las operaciones SOAP en métodos. El método de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] siguiente representa el ejemplo de SOAP proporcionado anteriormente.  
  
```  
public void DeleteItem(string item);  
```  
  
 La respuesta del servidor podría ser similar a la siguiente:  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItemResponse xmlns="https://www.microsoft.com/sql/ReportingServer" />  
    </soap:Body>  
</soap:Envelope>  
```  
  
 El método <xref:ReportService2010.ReportingService2010.DeleteItem%2A> no devuelve ningún valor, de modo que se devuelve una respuesta vacía.  
  
## <a name="see-also"></a>Vea también  
 [Acceso a la API de SOAP](accessing-the-soap-api.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Servidor de informes de Reporting Services](../reporting-services-report-server.md)   
 [Servicio web del servidor de informes](report-server-web-service.md)  
  
  
