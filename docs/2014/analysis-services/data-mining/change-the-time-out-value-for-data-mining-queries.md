---
title: Cambie el valor de tiempo de espera de consultas de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time-out
ms.assetid: f1add4bc-e882-440a-a98b-333cfa274c3e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 640d07115e2a071bb5d57e87955c11670f4c38b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085888"
---
# <a name="change-the-time-out-value-for-data-mining-queries"></a>Cambiar el valor del tiempo de espera para las consultas de minería de datos
  Al generar un gráfico de elevación o ejecutar una consulta de predicción, en ocasiones se necesita mucho tiempo para generar todos los datos requeridos para la predicción. Para evitar que se exceda el tiempo de espera de la consulta, puede cambiar el valor que controla cuánto tiempo debe esperar el servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para completar una consulta.  
  
 El valor predeterminado es 15; sin embargo, si sus modelos son complejos o el origen de datos es grande, puede no ser suficiente. Si es necesario, puede aumentar significativamente el valor para dejar tiempo suficiente para los procesos. Por ejemplo, si establece **Tiempo de espera de la consulta** en 600, la consulta podría seguir ejecutándose hasta un tiempo máximo de 10 minutos.  
  
 Para más información sobre las consultas de predicción, vea [Tareas y procedimientos de Consulta de minería de datos](data-mining-query-tasks-and-how-tos.md).  
  
### <a name="configure-the-time-out-value-for-data-mining-queries"></a>Configurar el valor del tiempo de espera para las consultas de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el menú **Herramientas** , seleccione **Opciones**.  
  
2.  En el panel **Opciones** , expanda **Diseñadores de Business Intelligence**.  
  
3.  Haga clic en el cuadro de texto **Tiempo de espera de la consulta** y escriba un valor para el número de segundos.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de Consulta de minería de datos](data-mining-query-tasks-and-how-tos.md)   
 [Consultas de minería de datos](data-mining-queries.md)  
  
  
