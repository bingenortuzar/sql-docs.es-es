---
title: MSSQLSERVER_1458 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 546d3e40d8b925d88344f6074d577b1b14c31092
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033428"
---
# <a name="mssqlserver1458"></a>MSSQLSERVER_1458
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1458|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBM_FAILREDO_ON_PRIMARY|  
|Texto del mensaje|La copia principal de la base de datos '%.*ls' encontró el error %d, el estado %d y la gravedad %d. Se suspendió la creación de reflejos de la base de datos. Intente resolver la condición de error y reanude la creación de reflejo.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje indica que la base de datos principal encontró un error que ocasionó la suspensión de la creación de reflejo de la base de datos.  
  
## <a name="user-action"></a>Acción del usuario  
En la mayoría de los casos, este error se corrige automáticamente. Si el problema continúa, el reinicio de la instancia de la base de datos o del servidor normalmente corrige el problema. Para obtener más información, busque el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de cada asociado para el error asociado que precedía a este mensaje.  
  
## <a name="see-also"></a>Consulte también  
[Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](~/database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
