---
title: MSSQLSERVER_17084 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17084 (Database Engine error)
ms.assetid: e579d104-3307-4edd-8587-b14ecbc02ed9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6e18eff965ac406ffd764bbe01bd9bb1aff41437
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076715"
---
# <a name="mssqlserver17084"></a>MSSQLSERVER_17084
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|17084|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|P3_ATOMIC_WITH_MISSING_OPTION|  
|Texto del mensaje|La cláusula WITH de la instrucción BEGIN ATOMIC debe especificar un valor para la opción '%ls'.|  
  
## <a name="explanation"></a>Explicación  
La cláusula WITH de la instrucción BEGIN ATOMIC no especificó un valor para una opción.  
  
## <a name="user-action"></a>Acción del usuario  
Los bloques **ATOMIC** requieren valores para las opciones **WITH** **TRANSACTION ISOLATION LEVEL** y **LANGUAGE**. Por ejemplo:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N'us_english')  
```  
  
Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
