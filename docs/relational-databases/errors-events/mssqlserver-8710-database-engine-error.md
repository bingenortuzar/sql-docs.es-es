---
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8b88b9212cec193e86de72b70c126df3e3d0d92e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120490"
---
# <a name="mssqlserver8710"></a>MSSQLSERVER_8710
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|MSSQLSERVER|  
|Identificador del evento|8710|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|QUERY2_CUBE_ILLEGAL_AGG_FUNC|  
|Texto del mensaje|Las funciones de agregado que se utilizan con consultas CUBE, ROLLUP o GROUPING SET se deben proporcionar para la combinación de subagregados. Para solucionar este problema, quite la función de agregado o escriba la consulta utilizando UNION ALL en cláusulas GROUP BY.|  
  
## <a name="explanation"></a>Explicación  
Se ha usado una función de agregado con CUBE, ROLLUP o GROUPING SETS que no proporciona un método para combinar subagregados.  
  
## <a name="user-action"></a>Acción del usuario  
Para solucionar este problema, quite la función de agregado o escriba la consulta utilizando UNION ALL en cláusulas GROUP BY.  
  
