---
title: ShortestLineTo (tipo de datos Geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ShortestLineTo_TSQL
- ShortestLineTo
dev_langs:
- TSQL
helpviewer_keywords:
- ShortestLineTo method (geography)
ms.assetid: 9d7c9885-5d1b-49ae-af31-5ef9fb8acaba
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7844f1d38f5d2e6f36f971eb83d8961596483142
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042611"
---
# <a name="shortestlineto-geography-data-type"></a>ShortestLineTo (tipo de datos Geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve una instancia de **LineString** con dos puntos que representan la distancia más corta entre las dos instancias de **geography**. La longitud de la instancia de **LineString** devuelta es la distancia entre las dos instancias de **geography**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.ShortestLineTo ( geography_other )  
```  
  
## <a name="arguments"></a>Argumentos  
 *otra_geografía*  
 Especifica la segunda instancia de **geography** a la que la instancia de **geography** que realiza la llamada está intentando determinar la distancia más corta.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Notas  
 El método devuelve una instancia de **LineString** con los extremos en los bordes de las dos instancias de **geography** que no se cruzan y que se comparan. La longitud de la instancia de **LineString** devuelta es igual a la distancia más corta entre las dos instancias de **geography**. Se devuelve una instancia vacía de **LineString** cuando las dos instancias de **geography** se cruzan.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-calling-shortestlineto-on-non-intersecting-instances"></a>A. Llamar a ShortestLineTo() en las instancias que no se cruzan  
 En este ejemplo se busca la distancia más corta entre una instancia de `CircularString` y una instancia de `LineString`, y se devuelven las instancias de `LineString` que conectan los dos extremos:  
  
 ```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography = 'LINESTRING(-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
 ```  
  
### <a name="b-calling-shortestlineto-on-intersecting-instances"></a>B. Llamar a ShortestLineTo() en las instancias que se cruzan  
 En este ejemplo se devuelve una instancia de `LineString` vacía porque la instancia de `LineString` se cruza con la instancia de `CircularString`:  
  
 ```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography = 'LINESTRING(-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.348 47.649, -122.681 47.655)';  
 SELECT @g1.ShortestLineTo(@g2).ToString();
``` 
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
