---
title: sysopentapes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysopentapes
- sysopentapes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], sysopentapes system table
- sysopentapes system table
ms.assetid: c066ca9b-9cfd-46b1-90a3-5c8dc9e7b6ae
author: stevestein
ms.author: sstein
ms.openlocfilehash: 813592ffa5b67a4926dff611c2ba0e0faf36d273
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029800"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada dispositivo de cinta abierto. Esta vista se almacena en el **maestro** base de datos.  
  
> [!IMPORTANT]  
>  Esta tabla del sistema se incluye como una vista para la compatibilidad con versiones anteriores. En su lugar, use el [sys.dm_io_backup_tapes &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) vista de administración dinámica.  
  
> [!NOTE]  
>  No puede quitar el **sysopentapes** vista.  

  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**ocurra**|**nvarchar(64)**|Nombre de archivo físico del dispositivo de cinta abierto. Para obtener más información sobre la apertura y liberación de los dispositivos de cinta, consulte [copia de seguridad &#40;Transact-SQL&#41; ](../../t-sql/statements/backup-transact-sql.md) y [restaurar &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).|  
  
## <a name="permissions"></a>Permisos  
 El usuario necesita tener el permiso VIEW SERVER STATE en el servidor.  
  
  
