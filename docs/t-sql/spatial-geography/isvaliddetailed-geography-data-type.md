---
title: IsValidDetailed (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsValidDetailed_TSQL
- IsValidDetailed
dev_langs:
- TSQL
helpviewer_keywords:
- IsValidDetailed geography
ms.assetid: f5f0b753-c825-43ce-987d-98655d8d8702
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c769b2e5fa5de94770d556264b82c81e28d43363
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930216"
---
# <a name="isvaliddetailed-geography-data-type"></a>IsValidDetailed (tipo de datos Geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve un mensaje que puede ayudar a identificar problemas con un objeto espacial no válido. Cuando el objeto no es válido, solo se devuelve el primer error. Cuando el objeto es válido, se devuelve el valor 24400.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.IsValidDetailed()  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(max)**  
  
 Tipo de valor devuelto de CLR: **string**  
  
## <a name="remarks"></a>Notas  
 La tabla siguiente contiene los posibles valores devueltos:  
  
|Valor devuelto|Descripción|  
|------------------|-----------------|  
|24400|Válido|  
|24401|No es válido por un motivo desconocido.|  
|24402|No es válido porque el punto {0} es un punto aislado, que no es válido en este tipo de objeto.|  
|24403|No es válido porque algún par de bordes del polígono se solapan.|  
|24404|No es válido porque el anillo del polígono {0} se corta a sí mismo o a algún otro anillo.|  
|24405|No es válido porque algún anillo del polígono se corta a sí mismo o a algún otro anillo.|  
|24406|No es válido porque la curva {0} degenera en un punto.|  
|24407|No es válido porque el anillo del polígono {0} se contrae en una línea en el punto {1}.|  
|24408|No es válido porque el anillo del polígono {0} no se cierra.|  
|24409|No es válido porque alguna parte del anillo del polígono {0} está en el interior de un polígono.|  
|24410|No es válido porque el anillo {0} es el primero de un polígono que no es el anillo exterior.|  
|24411|No es válido porque el anillo {0} cae fuera del anillo exterior {1} de su polígono.|  
|24412|No es válido porque el interior de un polígono con los anillos {0} y {1} no está conectado.|  
|24413|No es válido debido a dos bordes que se solapan en la curva {0}.|  
|24414|No es válido porque un borde de la curva {0} se superpone con un borde de la curva {1}.|  
|24415|No es válido porque el polígono tiene una estructura de anillo no válida.|  
|24416|No es válido porque en la curva {0}, el borde que comienza en el punto {1} es una línea o un arco degenerado con extremos opuestos.|  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo de un objeto espacial no válido se muestra cómo se comportan los métodos **IsValidDetailed()** .  
  
```sql  
DECLARE @p GEOGRAPHY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24409: Not valid because some portion of polygon ring (1) lies in the interior of a polygon.  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
