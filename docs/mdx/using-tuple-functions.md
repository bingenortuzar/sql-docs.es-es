---
title: Usar funciones de tupla | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9a329c8786ce580469e4601709509ca8a2de73f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037978"
---
# <a name="using-tuple-functions"></a>Usar funciones de tupla


  Una función de tupla recupera una tupla de un conjunto o mediante la resolución de una representación de cadena de una tupla.  
  
 Las funciones de tupla, al igual que las funciones de miembro y de conjunto, son esenciales para negociar las estructuras multidimensionales de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Hay tres funciones de tupla en MDX, [actual &#40;MDX&#41;](../mdx/current-mdx.md), [elemento &#40;tupla&#41; &#40;MDX&#41; ](../mdx/item-tuple-mdx.md) y [StrToTuple &#40;MDX&#41;](../mdx/strtotuple-mdx.md). En la consulta de ejemplo siguiente se muestra el modo de usar cada una de estas funciones:  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of Years and Countries`  
  
 `SET MyTuples AS  [Date].[Calendar Year].[Calendar Year].MEMBERS * [Customer].[Country].[Country].MEMBERS`  
  
 `//Returns a string representation of that set using the Current and Generate functions`  
  
 `MEMBER MEASURES.CURRENTDEMO AS GENERATE(MyTuples, TUPLETOSTR(MyTuples.CURRENT), ", ")`  
  
 `//Retrieves the fourth tuple from that set and displays it as a string`  
  
 `MEMBER MEASURES.ITEMDEMO AS TUPLETOSTR(MyTuples.ITEM(3))`  
  
 `//Creates a tuple consisting of the measure Internet Sales Amount and the country Australia from a string`  
  
 `MEMBER MEASURES.STRTOTUPLEDEMO AS STRTOTUPLE("([Measures].[Internet Sales Amount]" + ", [Customer].[Country].&[Australia])")`  
  
 `SELECT{MEASURES.CURRENTDEMO,MEASURES.ITEMDEMO,MEASURES.STRTOTUPLEDEMO} ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;sintaxis de MDX&#41;](../mdx/functions-mdx-syntax.md)   
 [Uso de funciones de miembro](../mdx/using-member-functions.md)   
 [Uso de funciones de conjuntos](../mdx/using-set-functions.md)  
  
  
