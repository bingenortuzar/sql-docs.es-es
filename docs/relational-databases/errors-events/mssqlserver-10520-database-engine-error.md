---
title: MSSQLSERVER_10520 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4b39522a5aa1e3208dfe1f7440abe20f4f0e00fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068160"
---
# <a name="mssqlserver10520"></a>MSSQLSERVER_10520
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10520|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_PARAM_NOT_ALLOWED|  
|Texto del mensaje|No se puede crear la guía de plan '%.*ls' porque @type se especificó como '%ls' y se especificó un valor no NULL para el parámetro '%ls'. Este tipo requiere un valor NULL para el parámetro. Especifique NULL para el parámetro o cambie el tipo por otro que admita un valor no NULL para el parámetro.|  
  
## <a name="explanation"></a>Explicación  
El tipo especificado en @type requiere un valor NULL para el parámetro especificado; sin embargo, se proporcionó un valor distinto de NULL.  
  
## <a name="user-action"></a>Acción del usuario  
Especifique NULL para el parámetro o cambie el tipo por otro que admita un valor no NULL para el parámetro.  
  
## <a name="see-also"></a>Consulte también  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
  
