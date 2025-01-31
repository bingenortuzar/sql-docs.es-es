---
title: Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model content, viewing
ms.assetid: 4a5f7c51-c704-4214-b05d-21cf735e6d96
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb080721ccb3e5b5aef190eda3d1088df09762c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086067"
---
# <a name="browse-a-model-using-the-microsoft-generic-content-tree-viewer"></a>Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft
  El Visor de contenido genérico del modelo de minería de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] proporciona información detallada sobre los patrones encontrados por el algoritmo de minería de datos, y también ofrece acceso a diversas estadísticas generadas durante el proceso de análisis. La cantidad y el tipo de información dependen del algoritmo utilizado, pero pueden incluir las categorías siguientes:  
  
-   Segmentos de datos y sus características.  
  
-   Estadísticas descriptivas sobre cada grupo o sobre el conjunto completo de datos.  
  
-   Número de bifurcaciones o nodos secundarios de un árbol.  
  
-   Diversos cálculos, como la varianza y la media, para un clúster o un conjunto completo de datos.  
  
 Ver esta información puede servir de ayuda para entender mejor los resultados del análisis. También se pueden identificar distintas maneras de ajustar y volver a entrenar el modelo. O bien, se puede decidir volver a entrenar el modelo usando un algoritmo diferente.  
  
## <a name="viewing-mining-model-content"></a>Ver contenido del modelo de minería de datos  
 El Visor de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] muestra las columnas, las reglas, las propiedades, los atributos, los nodos y otro tipo de contenido del *conjunto de filas de esquema de contenido* del modelo de minería de datos. El conjunto de filas de esquema de contenido es un marco genérico para presentar información detallada sobre el contenido de un modelo de minería de datos.  
  
 Esta información detallada está contenida en una tabla HTML que representa los patrones, los clústeres, o los árboles del modelo como nodos. Puede hacer clic en cada nodo y expandirlo para ver más información, tal como las fórmulas o el recuento de valores distintos para un atributo numérico. También puede explorar las relaciones de elementos primarios y secundarios entre los nodos.  
  
 Para obtener más información sobre el significado general de los términos que se usan en el contenido del modelo de minería de datos, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-model-content-analysis-services-data-mining.md). El tema también contiene vínculos a información acerca del contenido del modelo de minería de datos para tipos específicos de modelos. Cada tipo de modelo de minería de datos contiene información muy específica del algoritmo y de los patrones localizados en los datos, de modo que se recomienda consultar el tema de referencia técnica de cada tipo de modelo para comprender cada tipo de modelo.  
  
## <a name="querying-mining-model-content"></a>Consultar el contenido del modelo de minería de datos  
 La información proporcionada por el Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] también se encuentra disponible si se consulta el modelo de minería de datos. Puede crear consultas en el contenido del modelo de minería de datos usando instrucciones de Extensiones de minería de datos (DMX). Por ejemplo, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], se puede realizar una consulta de contenido ejecutando la siguiente instrucción de DMX:  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 Para obtener más información, vea [Consultas de minería de datos](data-mining-queries.md).  
  
## <a name="see-also"></a>Vea también  
 [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)   
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
  
