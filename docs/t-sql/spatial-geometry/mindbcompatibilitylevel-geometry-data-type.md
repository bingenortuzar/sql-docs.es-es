---
title: MinDbCompatibilityLevel (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geometry)
ms.assetid: c848b974-8ccb-4c5c-a7eb-b019a9538d99
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ddebe254c44d1577b2da5200cec02011c5bca89f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101202"
---
# <a name="mindbcompatibilitylevel-geometry-data-type"></a>MinDbCompatibilityLevel (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve el nivel de compatibilidad de base de datos mínimo que reconoce la instancia de tipo de datos **geometry**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de valor devuelto de CLR: **int**  
  
## <a name="remarks"></a>Notas  
 Use `MinDbCompatibilityLevel()` para probar un objeto espacial a efectos de compatibilidad antes de cambiar el nivel de compatibilidad de una base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>A. Probar el tipo CircularString a efectos de compatibilidad con el nivel de compatibilidad 110  
 En el ejemplo siguiente se prueba una instancia de `CircularString` a efectos de compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(3 4, 8 9, 5 6)'; 
 IF @g.MinDbCompatibilityLevel() <= 110 
 BEGIN 
 SELECT @g.ToString(); 
 END
 ```  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. Probar el tipo LineString a efectos de compatibilidad con el nivel de compatibilidad 100  
 En el ejemplo siguiente se prueba una instancia de `LineString` a efectos de compatibilidad con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 9, 5 6)'; 
 IF @g.MinDbCompatibilityLevel() <= 100 
 BEGIN 
 SELECT @g.ToString(); 
 END
``` 
  
## <a name="see-also"></a>Consulte también  
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

