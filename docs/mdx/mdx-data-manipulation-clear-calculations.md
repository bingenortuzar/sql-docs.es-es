---
title: CLEAR CALCULATIONS (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1b0766cb002960a96d702184ac9719abe7610afd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938020"
---
# <a name="mdx-data-manipulation---clear-calculations"></a>Manipulación de datos de MDX: CLEAR CALCULATIONS


  Quita todos los cálculos del cubo y devuelve el cubo al paso de cálculo 0.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CLEAR CALCULATIONS [FROMCube_Expression]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Expression*  
 Una expresión de cubo de MDX (Expresiones multidimensionales) válida.  
  
## <a name="remarks"></a>Comentarios  
 El **FROM** cláusula puede omitirse cuando el contexto del cubo es conocido, como en un script MDX.  
  
> [!NOTE]  
>  Esta instrucción solo puede ser ejecutada por un administrador de base de datos o de servidor o un miembro de un rol con acceso a los datos de origen del cubo (es decir, ReadSourceData=true)  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de manipulación de datos MDX &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
