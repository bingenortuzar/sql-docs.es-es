---
title: FirstChild (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c1bd2f37304131b881d49aaa874eaed13530fc0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032073"
---
# <a name="firstchild-mdx"></a>FirstChild (MDX)


  Devuelve el primer elemento secundario de un miembro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.FirstChild   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
### <a name="example"></a>Ejemplo  
 La consulta siguiente devuelve el primer elemento secundario del año fiscal 2003 de la jerarquía Fiscal, que es el primer semestre del año fiscal 2003.  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstChild ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [LastChild &#40;MDX&#41;](../mdx/lastchild-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
