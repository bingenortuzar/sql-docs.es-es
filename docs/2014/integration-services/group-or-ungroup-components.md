---
title: Agrupar o desagrupar componentes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- grouping containers
- tasks [Integration Services], grouping
- containers [Integration Services], grouping
- grouping tasks
ms.assetid: 34320838-c271-4f8c-90b3-1254690890bb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f9ba8c8ce532621a44ac8a7ab58cb712a97934e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768127"
---
# <a name="group-or-ungroup-components"></a>Agrupar o desagrupar componentes
  Las pestañas **Flujo de control**, **Flujo de datos**y **Controladores de eventos** del Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] admiten la agrupación contraíble. Si un paquete tiene muchos componentes, las pestañas pueden estar abarrotadas, lo que dificulta la visión de todos los componentes a la vez y la búsqueda del elemento con el que desea trabajar. La característica de agrupación contraíble puede ahorrar espacio en la superficie de trabajo y facilitar el trabajo con paquetes grandes.  
  
 Se seleccionan los componentes que desea agrupar, los agrupa y luego expande o contrae los grupos para facilitar su trabajo. Al expandir un grupo se proporciona acceso a las propiedades de los componentes del grupo. Las restricciones de precedencia que conectan las tareas y contenedores se incluyen automáticamente en el grupo.  
  
 A continuación se presentan las consideraciones para la agrupación de componentes.  
  
-   Para agrupar componentes, el flujo de control, el flujo de datos o el controlador de eventos deben contener más de un componente.  
  
-   Los grupos también pueden anidarse, permitiendo la creación de grupos dentro de grupos. La superficie de diseño puede implementar varios grupos no anidados, pero un componente solamente puede pertenecer a un grupo, a menos que los grupos estén anidados.  
  
-   Cuando se guarda un paquete, el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] guarda la agrupación, pero la agrupación no tiene ningún efecto sobre la ejecución de paquetes. La capacidad para agrupar componentes es una característica de tiempo de diseño que no afecta al comportamiento de tiempo de ejecución del paquete.  
  
### <a name="to-group-components"></a>Para agrupar componentes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control**, **Flujo de datos**o **Controladores de eventos** .  
  
4.  En la superficie de diseño de la pestaña, seleccione los componentes que quiera agrupar, haga clic con el botón derecho en un componente que haya seleccionado y, después, haga clic en **Agrupar**.  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
### <a name="to-ungroup-components"></a>Para desagrupar componentes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control**, **Flujo de datos**o **Controladores de eventos** .  
  
4.  En la superficie de diseño de la pestaña, seleccione el grupo que contenga el componente que quiera desagrupar, haga clic con el botón derecho y, después, haga clic en **Desagrupar**.  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Agregar o eliminar tareas o contenedores en un flujo de control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
     
 [Conectar tareas y contenedores mediante una restricción de precedencia predeterminada](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)  
  
  
