---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69acb74bd1c50900ae4852c41b3304da7ca7c00c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869468"
---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1807|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|CANNOT_EX_LOCK|  
|Texto del mensaje|No se puede obtener un bloqueo exclusivo en la base de datos '%.*ls'. Intente la operación en otro momento.|  
  
## <a name="explanation"></a>Explicación  
 Una operación que necesita acceso exclusivo a la base de datos no pudo obtenerlo.  
  
## <a name="user-action"></a>Acción del usuario  
 Desconecte todas las conexiones a esa base de datos o vuelva a intentar ejecutar la consulta en otro momento.  
  
  
