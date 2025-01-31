---
title: Clase de eventos Umbral de la CPU superado | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- CPU Threshold Exceeded Event Class
ms.assetid: eb106f7d-baa3-4a2b-96b2-f9fe0844057d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d74d1907b0f96275658c716a7a08061f0eec8995
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999563"
---
# <a name="cpu-threshold-exceeded-event-class"></a>Clase de eventos Umbral de la CPU superado
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Esta clase de eventos indica que el regulador de recursos ha detectado una consulta que supera el umbral de la CPU especificado para REQUEST_MAX_CPU_TIME_SEC.  
  
> [!NOTE]  
>  El intervalo para la detección de este evento es de cinco segundos. Está garantizado que se generará un evento si una consulta supera el límite especificado por lo menos en cinco segundos. Sin embargo, si una consulta supera el umbral especificado en menos de cinco segundos, es posible que se omita su detección dependiendo del tiempo de ejecución de la consulta y del momento en el que se llevó a cabo el último barrido para la detección.  
  
## <a name="cpu-threshold-exceeded-data-columns"></a>Columnas de datos del Umbral de la CPU superado  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|CPU|**int**|Uso de la CPU en milisegundos.|18|Sí|  
|EventClass|**int**|214|27|No|  
|EventSubClass|**int**|Infracción del límite de la CPU.|21|Sí|  
|GroupID|**int**|Id. del grupo donde se produjo la infracción.|66|Sí|  
|OwnerID|**int**|SPID del proceso que produjo la infracción.|58|Sí|  
|SPID|**int**|Id. del proceso de servidor que dispara este evento.<br /><br /> Nota: Este puede ser diferente al SPID del usuario actual si un subproceso del sistema valida el uso de la CPU como una tarea en segundo plano.|12|Sí|  
|StartTime|**datetime**|El momento en el que se desencadenó este evento.|14|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
