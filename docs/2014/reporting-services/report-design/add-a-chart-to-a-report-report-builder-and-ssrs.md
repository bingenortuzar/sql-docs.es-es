---
title: Agregar un gráfico a un informe (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a6b595dc-f775-4a53-8554-74a0bf9335ec
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 257df5742c2f8dec7d48c6d3afb4d6c6373d058c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106891"
---
# <a name="add-a-chart-to-a-report-report-builder-and-ssrs"></a>Agregar un gráfico a un informe (Generador de informes y SSRS)
  Si desea resumir datos y presentarlos con un formato visual, use una región de datos Gráfico. Es importante elegir el tipo de gráfico adecuado para el tipo de datos que se va a presentar. Esto determinará en qué medida se podrán interpretar correctamente los datos cuando se trasladen al gráfico. Para más información, vea [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
 La manera más simple de agregar una región de datos de Gráfico a su informe es ejecutar el Asistente para nuevo gráfico. El asistente proporciona gráficos de columna, línea, circular, barra y área. Para éstos y otros tipos de gráfico, puede agregar también un gráfico manualmente.  
  
 Después de agregar una región de datos Gráfico a la superficie de diseño, puede arrastrar los campos de conjunto de datos de informe para los datos numéricos y no numéricos hasta el panel de Datos del gráfico en el gráfico. Haga clic en el gráfico para mostrar el panel Datos del gráfico con estas tres áreas: grupos de series, grupos de categorías y valores.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-chart-to-a-report-by-using-the-chart-wizard"></a>Para agregar un gráfico a un informe utilizando el Asistente para gráficos  
  
1.  > [!NOTE]  
    >  El Asistente para gráficos solamente está disponible en el Generador de informes.  
  
     En la pestaña **Insertar** , haga clic en **Gráfico**y, a continuación, haga clic en **Asistente para gráficos**.  
  
2.  Siga los pasos en el Asistente para **Nuevo** gráfico.  
  
3.  En la pestaña **Inicio** , haga clic en **Ejecutar** para ver el informe representado.  
  
4.  En la pestaña **Ejecutar** , haga clic en **Diseño** para seguir trabajando en el informe.  
  
### <a name="to-add-a-chart-to-a-report"></a>Para agregar un gráfico a un informe  
  
1.  Cree un informe y defina un conjunto de datos. Para obtener más información, consulte [agregar datos a un informe &#40;generador de informes y SSRS&#41;](../report-data/report-datasets-ssrs.md).  
  
2.  En la pestaña **Insertar** , haga clic en **Gráfico**y, a continuación, haga clic en **Insertar gráfico**.  
  
3.  Haga clic en la superficie de diseño en la que desea que se encuentre la esquina superior izquierda del gráfico y arrastre hasta donde desee que se encuentre la esquina inferior derecha del gráfico.  
  
     Aparece el cuadro de diálogo **Seleccionar tipo de gráfico** .  
  
4.  Seleccione el tipo de gráfico que desea agregar. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Haga clic en el gráfico para mostrar el panel **Datos del gráfico** .  
  
6.  Agregue uno o más campos al área **Valores** . Esta información se representará en el eje de valores.  
  
7.  Agregue un campo de agrupación al área **Grupos de categorías** . Al agregar este campo al área **Grupos de categorías** , se crea un campo de agrupación automáticamente. Cada grupo representa un punto de datos de la serie.  
  
8.  Para resumir los datos por categoría, haga clic con el botón derecho en el campo de datos y, después, haga clic en **Propiedades de la serie**. En el cuadro **Categoría** , seleccione el campo de categoría en la lista desplegable. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
9. En la pestaña **Inicio** , haga clic en **Ejecutar** para ver el informe representado.  
  
10. En la pestaña **Ejecutar** , haga clic en **Diseño** para seguir trabajando en el informe.  
  
 En los gráficos con ejes, como los gráficos de barras y de columnas, es posible que el eje de categorías no muestre todas las etiquetas de categoría. Para más información sobre cómo cambiar las etiquetas de los ejes, vea [Especificar un intervalo de eje &#40;Generador de informes y SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tipos de gráficos &#40;Generador de informes y SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Puntos de datos vacíos y nulos en los gráficos &#40;Generador de informes y SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [Tutorial: Incorporación de un gráfico de barras a un informe (Generador de informes)](https://go.microsoft.com/fwlink/?LinkId=198052)   
 [Tutorial: Agregar un gráfico de barras a un informe (Diseñador de informes)](https://go.microsoft.com/fwlink/?LinkId=198042)   
 [Tutorial: Incorporación de un gráfico circular a un informe (Generador de informes)](https://go.microsoft.com/fwlink/?LinkId=198051)   
 [Tutorial: Agregar un gráfico circular a un informe (Diseñador de informes)](https://go.microsoft.com/fwlink/?LinkId=198041)  
  
  
