---
title: MSSQLSERVER_41333 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f137d859fa6f6233e14bc34c6bf50797a4360a98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123289"
---
# <a name="mssqlserver41333"></a>MSSQLSERVER_41333
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|41333|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|CROSS_CONTAINER_ISOLATION_FAILURE|  
|Texto del mensaje|Las siguientes transacciones deben acceder a tablas optimizadas para memoria y a procedimientos almacenados compilados de forma nativa en el aislamiento de instantáneas: transacciones RepeatableRead, transacciones Serializable y transacciones que accedan a las tablas que no estén optimizadas para memoria en aislamiento RepeatableRead o Serializable.|  
  
## <a name="explanation"></a>Explicación  
Hay restricciones respecto al usuario de los niveles de aislamiento mayores entre las transacciones basadas en disco y las transacciones XTP.  
  
## <a name="user-action"></a>Acción del usuario  
No intente operaciones de aislamiento alto nivel de las tablas optimizadas en memoria (y procedimientos compilados de forma nativa) y las tablas basadas en disco.  
  
Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
