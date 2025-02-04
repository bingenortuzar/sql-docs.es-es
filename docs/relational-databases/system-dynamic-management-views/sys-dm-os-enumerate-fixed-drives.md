---
title: Sys. DM _ _os_enumerate_fixed_drives (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_enumerate_fixed_drives
- sys.dm_os_enumerate_fixed_drives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_enumerate_fixed_drives dynamic management view
ms.assetid: 2e27489e-cf69-4a89-9036-77723ac3de66
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fa5834c14bfb1fafe3123c28a60359d64d059dfc
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/27/2019
ms.locfileid: "71342520"
---
# <a name="sysdm_os_enumerate_fixed_drives-transact-sql"></a>Sys. DM _ _os_enumerate_fixed_drives (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Introducido en SQL Server 2019.

Enumera los volúmenes montados en Letras de unidad como `C:\`.

|Nombre de columna|Tipo de datos|Descripción|
|-----------------|---------------|-----------------|  
|`fixed_drive_path`|`nvarchar(512)`|Ruta de acceso al volumen, como `C:\`.|  
|`drive_type`|`int`|Código para el tipo de unidad. Consulte [@no__t función-1](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew).|
|`drive_type_desc`|`nvarchar(512)`|Descripción del tipo de unidad. Consulte [@no__t función-1](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew).|
|`free_space_in_bytes`|`bigint`|Espacio libre en disco en bytes.|

## <a name="permissions"></a>Permisos

El usuario debe tener el permiso `VIEW SERVER STATE` en el servidor.

## <a name="see-also"></a>Vea también  

 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones &#40;y vistas de administración dinámica relacionadas con e/s TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
