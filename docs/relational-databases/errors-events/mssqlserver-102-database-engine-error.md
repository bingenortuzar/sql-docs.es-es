---
title: MSSQLSERVER_102 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 48df93c2976ee7b75bf064ca0443420f0a2ce70d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068251"
---
# <a name="mssqlserver102"></a>MSSQLSERVER_102
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|102|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|P_SYNTAXERR2|  
|Texto del mensaje|Sintaxis incorrecta cerca de '%.*ls'.|  
  
## <a name="explanation"></a>Explicación  
Indica un error de sintaxis. La información adicional no está disponible porque el error impide que [!INCLUDE[ssDE](../../includes/ssde-md.md)] procese la instrucción.  
  
Puede deberse a un intento de crear una clave simétrica mediante el cifrado RC4 desusado o RC4_128, cuando no está en el modo de compatibilidad 90 o 100.  
  
## <a name="user-action"></a>Acción del usuario  
Busque la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] para los errores de sintaxis.  
  
Si creó una clave simétrica mediante RC4 o RC4_128, seleccione un cifrado más reciente como, por ejemplo, uno de los algoritmos de AES. (Se recomienda). Si debe usar RC4, emplee ALTER DATABASE SET COMPATIBILITY_LEVEL para establecer el nivel de compatibilidad de la base de datos en 90 o 100. (No se recomienda).  
  
