---
title: Palabra clave reservada de siguiente de dos puntos Remove | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- reserved keywords
ms.assetid: 4f23f7e4-7b4d-4e19-86c9-7527bb8b107d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce2cfce6e35a95b7a07c17c4d3a2fd8a1b1c2610
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093181"
---
# <a name="remove-colon-following-reserved-keyword"></a>Quitar los dos puntos que siguen a las palabras claves reservadas
  El Asesor de actualizaciones detectó un script que contiene dos puntos (:) después de una palabra clave reservada. En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta sintaxis no se tenía en cuenta y las instrucciones se ejecutaban correctamente. Ahora, esta sintaxis hace que la instrucción no se pueda ejecutar si el modo de compatibilidad de la base de datos está establecido en 100 o más.  
  
 Las bases de datos de usuario mantienen su modo de compatibilidad.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Antes de cambiar el modo de compatibilidad de la base de datos a 100 o más, modifique sus scripts quitando los dos puntos que siguen a las palabras clave reservadas. Para obtener más información, vea "sp_dbcmptlevel" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
