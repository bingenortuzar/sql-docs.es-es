---
title: Comando exclusivo de SET | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d1a37043d332b54d0d5c5ebb7b2ba9f3acce000
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071760"
---
# <a name="set-exclusive-command"></a>Comando exclusivo de Set
Especifica si se abren los archivos de tabla para su uso exclusivo o compartido en una red.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Accesibilidad de los límites de una tabla abierta en una red para el usuario que lo abrió. La tabla no es accesible para otros usuarios de la red. SET ON exclusivo también impide que todos los demás usuarios que tengan acceso de solo lectura.  
  
 OFF  
 (Valor predeterminado para el controlador; los valores predeterminados de Visual FoxPro son ON para la sesión de datos globales y OFF para una sesión de datos privados). Permite filtrar una tabla que se abre en una red para compartir y modificar cualquier usuario en la red.  
  
## <a name="remarks"></a>Comentarios  
 Cambiar la configuración de conjunto exclusivo no cambia el estado de las tablas abiertos previamente. Por ejemplo, si se abre una tabla con establecer exclusivo establecida en ON y exclusivos establecer posteriormente se cambia a OFF, la tabla conserva su estado de uso exclusivo.  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo de configuración de Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
