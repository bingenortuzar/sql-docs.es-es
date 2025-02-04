---
title: Agregar un front-end web adicional de Reporting Services a una granja de servidores | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d7a11bda-ae26-49ac-b071-37d83cae5afe
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a7996ea2541963d0c7a2060d819667e25d102305
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108958"
---
# <a name="add-an-additional-reporting-services-web-front-end-to-a-farm"></a>Agregar un front-end web adicional de Reporting Services a una granja de servidores
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] El modo de SharePoint incluye los componentes necesarios para los servidores de aplicaciones y los servidores front-end web (WFE). Este tema se centra en instalar los componentes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] necesarios para un servidor de WFE, incluidas las páginas de aplicación utilizadas por las características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] como, por ejemplo, suscripciones, alertas de datos y [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. La instalación primaria de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] necesaria para WFE es la del complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para Productos de SharePoint 2010.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Debe ser administrador local para ejecutar el programa de instalación de SQL Server.  
  
-   El equipo debe estar unido a un dominio.  
  
-   Debe saber el nombre del servidor de bases de datos existente que hospeda la configuración de SharePoint y las bases de datos de contenido.  
  
-   El servidor de bases de datos debe estar configurado para permitir las conexiones de base de datos remota.  Si no lo está, no podrá combinar el nuevo servidor con la granja de servidores porque el nuevo servidor no podrá establecer una conexión a las bases de datos de configuración de SharePoint.  
  
-   El nuevo servidor deberá tener instalada la misma versión de SharePoint que están ejecutando los servidores actuales de la granja. Por ejemplo, si la granja de servidores ya tiene instalado SharePoint 2010 Service Pack 1 (SP1), deberá instalar también SP1 en el nuevo servidor para poder combinar la granja de servidores.  
  
-   Revise los siguientes temas adicionales para conocer los requisitos del sistema y de las versiones:  
  
     [Instrucciones para usar las características de SQL Server BI en una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
## <a name="steps"></a>Pasos  
 En los pasos de este tema se supone que el administrador de una granja de servidores de SharePoint va a instalar y configurar el servidor. En el diagrama se muestra un entorno típico de tres niveles. Los elementos numerados en el diagrama se describen en la siguiente lista:  
  
-   (1) Varios servidores front-end web (WFE). Los servidores WFE requieren el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint 2010. Los pasos siguientes agregan un segundo servidor de aplicaciones en este nivel.  
  
-   (2) Dos servidores de aplicaciones que ejecutan [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y los sitios web, por ejemplo, Administración central.  
  
-   (3) Dos servidores de base de datos de SQL Server.  
  
-   (4) Representa una solución de equilibrio de carga de red (NLB) de software o hardware  
  
 ![Agregar SSRS a un nuevo WFE de SharePoint](../../../2014/sql-server/install/media/rs-sharepointscale-wfe.gif "Agregar SSRS a un nuevo WFE de SharePoint")  
  
 En los siguientes pasos se supone que un administrador va a instalar y configurar el servidor.  
  
|Paso|Descripción y vínculo|  
|----------|--------------------------|  
|Ejecutar la herramienta de preparación de Productos de SharePoint 2010|Debe tener el disco de instalación para SharePoint 2010. La herramienta de preparación es **PrerequisiteInstaller.exe** en los discos de instalación.|  
|Instalar un producto de SharePoint 2010.|1) seleccione el **granja de servidores** tipo de instalación.<br /><br /> (2) seleccione **completar** para el tipo de servidor.<br /><br /> 3) Una vez completada la instalación, no ejecute el Asistente para configuración de Productos de SharePoint si la granja de servidores de SharePoint existente tiene instalado SharePoint 2010 SP1. Debe instalar SharePoint SP1 antes de ejecutar el Asistente para configuración de Productos de SharePoint.|  
|Instalar SharePoint Server 2010 SP1.|Si la granja de SharePoint existente tiene instalado SharePoint 2010 SP1, descargue e instale SharePoint 2010 SP1 desde:[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697).<br /><br /> Para obtener más información acerca de SharePoint 2010 SP1, vea [Problemas conocidos al instalar Office 2010 SP1 y SharePoint 2010 SP1](https://support.microsoft.com/kb/2532126):|  
|Ejecutar el Asistente para configuración de Productos de SharePoint para agregar el servidor a la granja.|(1) en el **productos de Microsoft SharePoint 2010** grupo de programas, haga clic en **Asistente para configuración de productos de Microsoft SharePoint 2010**.<br /><br /> 2) en el **conectarse a una granja de servidores** página, seleccione **conectar a una granja existente** y haga clic en **siguiente**.<br /><br /> 3) en el **especificar base de datos de configuración** página, escriba el nombre del servidor de base de datos usada para la granja de servidores existente y el nombre de la base de datos de configuración. Haga clic en **Siguiente**.<br />**&#42;&#42;Importante &#42; &#42;**  si ve un mensaje de error similar al siguiente y se ha comprobado que tiene permisos, a continuación, compruebe qué protocolos están habilitados para la configuración de red de SQL Server en **Sql Server Administrador de configuración**. "No se pudo conectar al servidor de base de datos. Asegúrese de la base de datos existe, es un servidor Sql Server y que tiene los permisos adecuados para tener acceso al servidor."<br />**&#42;&#42;Importante &#42; &#42;**  si ve la página **de los productos y estado de la revisión**, deberá revisar la información de la página y actualizar el servidor con los archivos necesarios para que pueda continuar y unir el servidor de la granja de servidores.<br /><br /> (4) en el **especifique la configuración de seguridad de granja** página, escriba la frase de contraseña de la granja de servidores y haga clic en **siguiente**. Haga clic en **Siguiente** en la página de confirmación para ejecutar el asistente.<br /><br /> 5) haga clic en **siguiente** para ejecutar el **Asistente para configuración de granja de servidores**.|  
|Comprobar que el servidor se ha agregado a la granja de servidores de SharePoint.|1) En Administración central de SharePoint, haga clic en **Administrar servidores en esta granja de servidores** en el grupo **Configuración del sistema** .<br /><br /> 2) Compruebe que el nuevo servidor se agrega y que el estado es correcto.<br /><br /> (3) para quitar este servidor desde el rol de WFE, haga clic en **administrar servicios en el servidor** y detener el servicio **aplicación Web de Microsoft SharePoint Foundation**.|  
|Instalar el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento para productos de SharePoint 2010.|Hay varios métodos para instalar el complemento. En los siguientes pasos se usa el asistente para instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para obtener más información acerca de cómo instalar el complemento, vea [instalar o desinstalar el complemento Reporting Services para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md). Ejecute [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalación:<br /><br /> 1) En la página **Rol de instalación** , seleccione **Instalación de características de SQL Server**.<br /><br /> 2) en el **selección de características** página, seleccione **complemento de Reporting Services para productos de SharePoint**<br /><br /> (3) haga clic en **siguiente** en las páginas siguientes para completar las opciones de configuración.<br /><br /> Para obtener más información sobre la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Instalar el modo de SharePoint de Reporting Services para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).|  
|Comprobar que el nuevo servidor está operativo.|1) En Administración central de SharePoint, haga clic en **Administrar servidores en esta granja de servidores** en el grupo **Configuración del sistema** .<br /><br /> 2) Compruebe que el nuevo servidor está en la lista.|  
|Actualizar la solución de NLB.|Si procede, actualice el entorno NLB de hardware o software para incluir el nuevo servidor.|  
  
## <a name="see-also"></a>Vea también  
 [Agregar un sitio Web o servidor de aplicaciones para la granja de servidores (SharePoint Server 2010)](https://technet.microsoft.com/library/bb218968.aspx?missingurl=%2fen-us%2flibrary%2fe1aeaddf-6ee4-43a9-82b7-db20b68c71db\(Office.14\))   
 [Configurar los servicios (SharePoint Server 2010)](https://technet.microsoft.com/library/ee794878.aspx)  
  
  
