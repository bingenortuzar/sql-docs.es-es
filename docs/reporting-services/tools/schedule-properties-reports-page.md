---
title: Propiedades de la programación (página Informes) | Microsoft Docs
ms.date: 06/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.scheduleproperties.reports.f1
ms.assetid: 7db728bd-4b08-43ef-a49a-e8dcdd37cf89
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0e8441dec655398ec530bc95049a339edd9e01ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571404"
---
# <a name="schedule-properties-reports-page"></a>Propiedades de la programación (página Informes)
  Use la [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] página de propiedades de programación en [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] para ver una lista de todos los informes que usan la programación compartida específica. Las programaciones pueden utilizarse para actualizar instantáneas de informe, generar un historial de informes, desencadenar una suscripción o hacer expirar una copia del informe almacenada en caché. Para averiguar cómo se usa la programación, vea la información de propiedad y suscripciones del informe.  
  
 Aunque esta página muestra cada informe que usa la programación compartida, no indica cuántas veces se usa la programación compartida dentro de ese informe único. Por ejemplo, supongamos que 20 diferentes suscriptores al informe Company Sales usan la misma programación compartida para desencadenar el procesamiento de suscripciones. En este caso, el informe Company Sales solamente aparecerá una vez en esta lista, aunque el informe tenga 20 referencias a la programación compartida.  
  
 Para abrir la página de propiedades de programación:
 1. Inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2. Conéctese a un servidor de informes.
 3. Abra la carpeta **Programaciones compartidas** .
 4. Haga clic con el botón derecho en una programación compartida y seleccione **Propiedades**.
 5. Haga clic en **Informes**.  
  
  También puede administrar programaciones compartidas desde la **Configuración del sitio** del portal web de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] .
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Ediciones y características admitidas de SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).  
  
## <a name="options"></a>Opciones  
 **Carpeta**  
 Especifica la ruta de acceso del informe.  
  
 **Informe**  
 Especifica el nombre del informe que utiliza la programación.  
  
## <a name="see-also"></a>Consulte también  
 [Crear, modificar y eliminar programaciones](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [Programaciones](../../reporting-services/subscriptions/schedules.md)   
 [Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Configurar las propiedades generales de un informe (Administrador de informes)](https://msdn.microsoft.com/10b941b2-28e6-4408-9ee4-acebc63c8496)  
  
  

