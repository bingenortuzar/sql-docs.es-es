---
title: 'Configuración del sitio de SharePoint para el elemento web Visor de informes: SSRS | Microsoft Docs'
ms.date: 11/15/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: jt000
ms.author: jasontre
ms.openlocfilehash: 738908549caa157557a16b1ae05575231a15c734
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580587"
---
# <a name="sharepoint-site-settings-for-the-report-viewer-web-part---reporting-services"></a>Configuración del sitio de SharePoint para el elemento web Visor de informes: Reporting Services | Microsoft Docs

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2016-2019](../../includes/ssrs-appliesto-sharepoint-2016-2019.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

El elemento web Visor de informes tiene un par de opciones que se pueden configurar. Un administrador del sitio puede habilitar y deshabilitar estas opciones en la página de configuración del sitio de SharePoint. Tenga en cuenta que cada sitio tiene su propia configuración. Además, esta configuración no se restablecerá después de reinstalar el elemento web Visor de informes.

## <a name="accessing-the-site-settings-page"></a>Acceso a la página de configuración del sitio

Para acceder a la configuración del sitio:

1. Desde el sitio de SharePoint, seleccione el icono de **engranaje** de la parte superior izquierda y, a continuación, **Configuración del sitio**.

    ![Configuración del sitio desde el icono de engranaje.](media/sharepoint-site-settings.png)

2. Haga clic en **Configuración del elemento web del Visor de informes** en el grupo de configuración del sitio de **Reporting Services**.

    > [!NOTE]
    > Para acceder a la configuración del sitio, también puede navegar directamente a `<site>/_layouts/15/ReportViewerWebPart/ReportViewerWebPartSettings.aspx`

## <a name="report-viewer-web-part-settings"></a>Configuración del elemento web Visor de informes

|Configuración|Comentarios|  
|-------------|--------------|  
|Recopilar los datos de uso|Habilita el envío de información de errores y uso a Microsoft para ayudar a mejorar nuestros productos. Para obtener información acerca de la directiva de recopilación de datos de informes de error, consulte la [Declaración de privacidad de Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkID=868444).|  
|Habilitar los metadatos de accesibilidad para los informes|Define la información del dispositivo [ `AccessibleTablix`](../html-device-information-settings.md) para los informes representados.| 
