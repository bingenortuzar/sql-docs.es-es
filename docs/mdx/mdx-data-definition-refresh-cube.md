---
title: REFRESH CUBE (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 957609573c206b7c3492789c369d0fb2be2398a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038164"
---
# <a name="mdx-data-definition---refresh-cube"></a>Definición de datos de MDX: REFRESH CUBE


  Actualiza la caché de cliente para un cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REFRESH CUBECube_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Expresión de cadena válida que proporciona un nombre de cubo.  
  
## <a name="remarks"></a>Comentarios  
 Las aplicaciones cliente conectadas a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], esta instrucción hace que la memoria caché en la aplicación cliente se sincronice con el servidor. Mientras que esto normalmente se detectará y actualizará automáticamente, el período de tiempo antes de que esto suceda depende de la configuración de la cadena de conexión del cliente. La instrucción REFRESH CUBE actualiza inmediatamente los datos.  
  
 En las aplicaciones cliente conectadas a un cubo local, la instrucción REFRESH CUBE hace que el archivo de cubo local se vuelva a generar.  
  
> [!IMPORTANT]  
>  Los conjuntos con nombre que se almacenan en el servidor no se actualizan.  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
