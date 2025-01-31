---
title: Utilizar CacheSize | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2e3a67e9ad0f1f26f804ecb38e960041863fad9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923573"
---
# <a name="using-cachesize"></a>Utilizar CacheSize
Use la **CacheSize** propiedad para controlar el número de registros que para recuperar de una vez en la memoria local desde el proveedor. Por ejemplo, si la **CacheSize** es 10, después de abrir primero la **Recordset** objeto, el proveedor recupera los 10 primeros registros en la memoria local. Conforme se desplaza por la **Recordset** objeto, el proveedor devuelve los datos desde el búfer de memoria local. Tan pronto como se mueve más allá del último registro en la memoria caché, el proveedor recupera los 10 siguientes registros del origen de datos en la memoria caché.  
  
> [!NOTE]
>  **CacheSize** se basa en el **número máximo de filas abierto** propiedad específica del proveedor (en el **propiedades** colección de la **Recordset** objeto). No puede establecer **CacheSize** en un valor mayor que **número máximo de filas abierto.** Para modificar el número de filas que se puede abrir el proveedor, establezca **número máximo de filas abierto**.  
  
 El valor de **CacheSize** se puede ajustar durante la vigencia de la **Recordset** objeto, pero al cambiar este valor solo afecta al número de registros en la memoria caché después de recuperaciones posteriores desde el origen de datos. Cambiar el valor de propiedad por sí solo no cambiará el contenido actual de la memoria caché.  
  
 Si hay menos registros que se recuperan de **CacheSize** especifica, el proveedor devuelve los registros restantes y se produce ningún error.  
  
 Un **CacheSize** valor de cero no se permite y devuelve un error.  
  
 Los registros recuperados de la memoria caché no reflejan los cambios simultáneos realizados por otros usuarios a los datos de origen. Para forzar una actualización de todos los datos almacenados en caché, use el [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
 Si **CacheSize** se establece en un valor mayor que 1, los métodos de navegación ([mover](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext y MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) puede producir la navegación a un eliminada registro, si se produce una eliminación después de haber recuperaron los registros. Después de la operación de captura inicial, las eliminaciones posteriores no se reflejarán en la caché de datos hasta que intente obtener acceso a un valor de datos de una fila eliminada. Sin embargo, establecer **CacheSize** a 1 se elimina este problema porque no se pueden recuperar las filas eliminadas.
