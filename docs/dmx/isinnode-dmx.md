---
title: IsInNode (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6e4c7df84bc7bf3a4804db76d952b1219100ef5a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008361"
---
# <a name="isinnode-dmx"></a>IsInNode (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica si el nodo especificado contiene el caso actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsInNode(<NodeID>)  
```  
  
## <a name="return-type"></a>Tipo devuelto  
 Un tipo booleano.  
  
## <a name="remarks"></a>Comentarios  
 **IsInNode** solo se usa en [SELECT FROM &#60;modelo&#62;. CASOS &#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md) y [SELECT FROM &#60;modelo&#62;. SAMPLE_CASES &#40;DMX&#41; ](../dmx/select-from-model-sample-cases-dmx.md) las consultas.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todos los casos que se han utilizado para crear el modelo que está asociado al nodo especificado en la función IsInNode.  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
