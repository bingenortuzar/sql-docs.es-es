---
title: Integration Services Server (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 02966721d1fdfd1c1d3051510e0dd68ed26dcbc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771741"
---
# <a name="integration-services-ssis-server"></a>Servidor de Integration Services (SSIS)
  Después de diseñar y probar paquetes en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], puede implementar los proyectos que contienen los paquetes en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 El servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos de `SSISDB`. La base de datos almacena los objetos siguientes: paquetes, proyectos, parámetros, permisos, propiedades del servidor e historial operativo.  
  
 La base de datos de `SSISDB` expone la información de objetos en vistas públicas que puede consultar. La base de datos también proporciona procedimientos almacenados a los que puede llamar para administrar los objetos.  
  
 Para poder implementar los proyectos en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], debe crear el catálogo de `SSISDB`.  
  
 Para obtener información general de la funcionalidad del catálogo de SSISDB, consulte [SSIS Catalog (Catálogo de SSIS)](ssis-catalog.md).  
  
## <a name="high-availability"></a>Alta disponibilidad  
 Como otras bases de datos de usuario, la base de datos de `SSISDB` admite la creación de reflejo de la base de datos y la replicación. Para obtener más información sobre la creación de reflejo y la replicación, consulte [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 También puede proporcionar alta disponibilidad de SSISDB y de su contenido mediante SSIS y los grupos de disponibilidad AlwaysOn. Para obtener más información, vea esta entrada de blog de Matt Masson, [SSIS con AlwaysOn](https://go.microsoft.com/fwlink/?LinkId=255873), en blogs.msdn.com.  
  
##  <a name="ssms"></a> Servidor de Integration Services en SQL Server Management Studio  
 Al conectarse a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos de `SSISDB`, ve los objetos siguientes en el Explorador de objetos:  
  
-   **Base de datos SSISDB**  
  
     El `SSISDB` base de datos aparece bajo el **bases de datos** nodo en el Explorador de objetos. Puede consultar las vistas y llamar a los procedimientos almacenados que administran el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y los objetos que están almacenados en el servidor.  
  
-   **Catálogos de Integration Services**  
  
     En el nodo **Catálogos de Integration Services** hay carpetas para los proyectos y los entornos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Crear el catálogo de SSIS](../create-the-ssis-catalog.md)  
  
-   [Ver la lista de paquetes en el servidor de Integration Services](view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Implementar proyectos en el servidor de Integration Services](../deploy-projects-to-integration-services-server.md)  
  
-   [Ejecutar un paquete en el servidor SSIS con SQL Server Management Studio](../run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog, [SSIS con AlwaysOn](https://go.microsoft.com/fwlink/?LinkId=255873), en blogs.msdn.com.  
  
  
