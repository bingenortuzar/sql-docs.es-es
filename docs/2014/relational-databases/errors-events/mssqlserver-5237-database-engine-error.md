---
title: MSSQLSERVER_5237 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5237 (Database Engine error)
ms.assetid: 9ff28935-d1eb-47ee-99b3-1a65cb948ce7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eabe36c423b1df3702b594137aca371a6075e327
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867632"
---
# <a name="mssqlserver5237"></a>MSSQLSERVER_5237
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|5237|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC4_INDEXED_VIEW_CHECK_QUERY_FAILED_NO_ERRORCODE|  
|Texto del mensaje|Error de comprobación del conjunto de filas cruzadas de DBCC para el objeto 'NAME' (Id. de objeto O_ID) debido a un error de consulta interno.|  
  
## <a name="explanation"></a>Explicación  
 Un error interno ha provocado que DBCC no pueda ejecutar la consulta para comprobar las vistas indizadas.  
  
## <a name="user-action"></a>Acción del usuario  
 Vuelva a ejecutar el comando DBCC.  
  
  
