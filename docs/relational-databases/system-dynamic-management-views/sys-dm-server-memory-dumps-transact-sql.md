---
title: Sys.dm_server_memory_dumps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_server_memory_dumps_TSQL
- dm_server_memory_dumps_TSQL
- dm_server_memory_dumps
- sys.dm_server_memory_dumps
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_memory_dumps dynamic management view
ms.assetid: 41782719-f54d-4e11-941a-c050c7576e23
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7f31bc59e918a2a2ca4f0cf9e3833571028e85a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090797"
---
# <a name="sysdmservermemorydumps-transact-sql"></a>sys.dm_server_memory_dumps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada archivo de volcado de memoria generado por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Use esta vista de administración dinámica para solucionar problemas potenciales.  
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**filename**|**nvarchar(256)**|Ruta de acceso y nombre del archivo de volcado de memoria. No puede ser null.|  
|**creation_time**|**datetimeoffset(7)**|Fecha y hora en que se creó el archivo. No puede ser null.|  
|**size_in_bytes**|**bigint**|Tamaño (en bytes) del archivo. Acepta valores NULL.|  
  
## <a name="general-remarks"></a>Notas generales  
 El tipo de volcado de memoria puede ser un minivolcado de memoria, un volcado de memoria de todos los subprocesos o un volcado de memoria completo. Los archivos tienen una extensión .mdmp.  
  
## <a name="security"></a>Seguridad  
 Los archivos de volcado de memoria pueden contener información confidencial. Para proteger la información confidencial, puede utilizar una lista de control de acceso (ACL) con objeto de restringir el acceso a los archivos o copiarlos en una carpeta con acceso restringido. Por ejemplo, antes de enviar que a Microsoft los archivos de depuración de servicios de soporte técnico, recomendamos que quite cualquier información importante o confidencial.  
  
### <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW SERVER STATE.  
  
  
