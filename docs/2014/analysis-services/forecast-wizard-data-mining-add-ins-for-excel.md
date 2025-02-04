---
title: Pronóstico (complementos de minería de datos para Excel de datos) del Asistente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- forecasting [data mining]
- time series [data mining]
ms.assetid: c5b33f75-42d4-4598-89e7-94815c142ce6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f0717d8a81cc89897de005144dd631d23da42137
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081033"
---
# <a name="forecast-wizard-data-mining-add-ins-for-excel"></a>Asistente para pronóstico (Complementos de minería de datos para Excel)
  ![Asistente para asociación en la cinta de opciones minería de datos](media/dmc-forecast.gif "asociar el Asistente en la cinta de opciones minería de datos")  
  
 El Asistente para pronóstico le permite predecir valores en una serie temporal. El Asistente para pronóstico usa el algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)], que es un algoritmo de regresión que se usa para predecir columnas continuas, como ventas de productos.  
  
 Cada modelo de pronóstico debe contener una serie de casos, que es la columna que distingue entre los puntos de una secuencia. Por ejemplo, si va a usar datos históricos para pronosticar las ventas durante un período de varios meses, debería usar una columna que contenga una serie de fechas como la serie de casos.  
  
 Puede crear predicciones a partir de un modelo de predicción sin proporcionar nuevos datos de entrada.  
  
 El [previsión &#40;herramientas de análisis de tabla para Excel&#41; ](forecast-table-analysis-tools-for-excel.md) herramienta, en el **analizar** cinta de opciones, también le permite crear modelos de predicción, pero es menos personalizable y solo se pueden usar datos en tablas de Excel.  
  
## <a name="using-the-forecast-wizard"></a>Usar el Asistente para pronóstico  
  
1.  En el **minería de datos** la cinta de opciones, haga clic en **previsión**.  
  
2.  En el **seleccionar datos de origen**, elija la tabla de Excel, intervalo o un origen de datos externo que se usará como entradas.  
  
     Si utiliza un origen de datos externo, puede definir consultas o vistas personalizadas y guardarlas como un origen de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  En el **Forecasting** página, para **marca de tiempo**, seleccione una columna que contiene el valor numérico único (Esto incluye los valores de fecha y hora) que puede usarse como la serie de casos. El origen de datos se debe ordenar de forma ascendente según esta columna.  
  
     Si los datos no tienen este tipo de columna, puede usar la opción \<sin marca de tiempo >. El asistente agregará una columna de orden única para los datos de entrada; por consiguiente, debe asegurarse de que los datos están ordenados de la manera que desea antes de ejecutar el asistente y elegir esta opción.  
  
4.  Si lo desea, puede hacer clic en **parámetros** y personalizar el comportamiento del modelo de minería de datos.  
  
     Los modelos de predicción admiten varios algoritmos:  
  
    -   ARIMA  
  
    -   ARTXP (un tipo de modelo de regresión)  
  
    -   ARTXP y ARIMA combinados  
  
     Para obtener información acerca de las diferencias, vea [Microsoft Time Series Algorithm Technical Reference](data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
     También puede agregar sugerencias de periodicidad, especificar opciones de suavizado y personalizar las opciones de regresión para el modelo.  
  
5.  En el **finalizar** página, proporcione un nombre descriptivo para el conjunto de datos y el modelo y establecer las siguientes opciones que controlan cómo trabajar con el modelo terminado:  
  
    -   **Examinar modelo**. Cuando se selecciona esta opción, tan pronto como el asistente finaliza el procesamiento del modelo, se abre un **examinar** ventana que le ayudarán a explorar los resultados. El contenido del visor depende del tipo de modelo que creó. Para obtener más información, consulte [examinar un modelo de previsión](browsing-a-forecasting-model.md).  
  
    -   **Habilitar obtención de detalles**. Seleccione esta opción para ver los datos subyacentes desde el modelo terminado. Esta opción solo está disponible si se crea un modelo de árbol de decisión.  
  
    -   **Usar modelo temporal**. Si selecciona esta opción, el modelo no se guardará en el servidor. Se eliminan los modelos temporales al cerrar Excel.  
  
### <a name="requirements"></a>Requisitos  
 Los datos deben incluir al menos una columna que se pueda utilizar como serie temporal. Los valores de esta columna deben ser únicos y continuos, es decir, no debe haber interrupciones. Antes de ejecutar el asistente, ordene los datos según la columna de serie temporal en orden ascendente.  
  
 Si los datos no incluyen una columna de hora o de fecha, puede asignar una serie numérica arbitraria o permitir al asistente crearla. Si permite al asistente crear la columna de orden de la serie, asegúrese de que las otras columnas están ordenadas en el orden que desea antes de iniciar el asistente.  
  
## <a name="see-also"></a>Vea también  
 [Creación de un modelo de minería de datos](creating-a-data-mining-model.md)   
 [Previsión &#40;herramientas de análisis de tabla para Excel&#41;](forecast-table-analysis-tools-for-excel.md)   
 [Examinar un modelo de pronóstico](browsing-a-forecasting-model.md)  
  
  
