---
title: CALCULAte (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a873c2a6a60e3e6283c3c24fa4b9d28757e57ffb
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893354"
---
# <a name="mdx-scripting---calculate"></a>Scripting de MDX: CALCULATE


  Llena cada celda de un cubo con un valor agregado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>Argumentos  
 None  
  
## <a name="remarks"></a>Comentarios  
 La instrucción CALCULATE se incluye automáticamente como la primera instrucción de un script MDX de un cubo al crearlo mediante [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. La instrucción CALCULATE indica que se agregue cada celda del cubo comenzando por las celdas de menor granularidad. Después de agregar una celda, si se llenan celdas de menor granularidad mediante expresiones, eso repercute en el valor agregado de las celdas de mayor granularidad. Casi siempre se prefiere realizar esta agregación, pero se puede eliminar o hacer que otras instrucciones se ejecuten antes que esta instrucción.  
  
 La instrucción CALCULATE no se puede incluir en un subcubo anidado del script MDX. Un subcubo anidado se define mediante la instrucción SCOPE. Para obtener más información acerca de la instrucción SCOPE, vea [ &#40;Scope&#41;Statement MDX](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Los miembros calculados no se agregan.  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones &#40;de scripting de MDX MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [Aspectos básicos de scripting MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services)   
 [Definir asignaciones y otros comandos de script](https://docs.microsoft.com/analysis-services/multidimensional-models/define-assignments-and-other-script-commands)  
  
  
