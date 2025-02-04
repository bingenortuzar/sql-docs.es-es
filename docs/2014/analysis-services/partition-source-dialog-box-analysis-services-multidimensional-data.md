---
title: Cuadro de diálogo de origen (Analysis Services - datos multidimensionales) de partición | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionsourcedialog.f1
ms.assetid: c414dabe-9bad-49b7-9a3c-dfca87fef92b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2102d28a61a99ed9ed6786dd8f2dee196066045c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072147"
---
# <a name="partition-source-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Origen de la partición (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Origen de la partición** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para especificar el origen de los datos de la tabla de hechos para una partición. Para mostrar el cuadro de diálogo **Origen de la partición** :  
  
-   Haga clic en el botón **…** de una celda de la cuadrícula **Particiones** de un grupo de medida seleccionado en el panel **Grupos de medida** en la pestaña **Particiones** del Diseñador de cubos.  
  
-   Haga clic en el botón **…** del valor de propiedad **Origen** de un objeto de **Partición** en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Opciones  
  
|Opción|Definición|  
|------------|----------------|  
|**Tipo de enlace**|Seleccione el tipo de enlace que desea utilizar como origen de la partición especificada. Las siguientes opciones están disponibles:<br /><br /> **Enlace de tablas**: Seleccione esta opción para mostrar el panel **Detalle del enlace de tablas** e indique que la partición está enlazada al contenido de una tabla en un origen de datos o vista del origen de datos. Para más información sobre el panel **Detalle del enlace de tablas**, vea [Detalle del enlace de tablas &#40;cuadro de diálogo Origen de la partición&#41; &#40;Analysis Services - Datos multidimensionales&#41;](table-binding-partition-source-dialog-analysis-services-multidimensional-data.md).<br /><br /> **Detalles**: Seleccione esta opción para mostrar el panel **Detalle del enlace de consultas** e indique que la partición está enlazada al contenido de una consulta ejecutada en un origen de datos. Para más información sobre el panel **Detalle del enlace de consultas**, vea [Detalle del enlace de consultas &#40;cuadro de diálogo Origen de la partición&#41; &#40;Analysis Services - Datos multidimensionales&#41;](query-binding-partition-source-dialog-analysis-services-multidimensional-data.md).|  
|**Detail**|Muestra el cuadro de diálogo **Detalle del enlace de tablas** o el cuadro de diálogo **Detalle del enlace de consultas** , según el valor de la opción **Tipo de enlace** .|  
  
## <a name="see-also"></a>Vea también  
 [Las particiones &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](partitions-cube-designer-analysis-services-multidimensional-data.md)   
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
