---
title: sys.filetables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- filetables
- filetables_TSQL
- sys.filetables
- sys.filetables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetables catalog view
ms.assetid: a740be59-cd52-4707-9ad2-5203669a63ac
author: stevestein
ms.author: sstein
ms.openlocfilehash: 791bba2f5ec1830e343acff24fd55628a3f13d2e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134003"
---
# <a name="sysfiletables-transact-sql"></a>sys.filetables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada objeto FileTable de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para más información sobre FileTables, vea [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).    
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**||Número de identificación del objeto. Es único en una base de datos.<br /><br /> Para obtener más información, [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_enabled**|**bit**|1 = FileTable está en el estado "habilitado".|  
|**directory_name**|**varchar(255)**|Nombre del directorio raíz de un objeto FileTable.|  
|**filename_collation_id**||Es el identificador de intercalación definido para el FileTable|  
|**filename_collation_name**||Es el nombre de intercalación definido para el FileTable.|  
  
## <a name="see-also"></a>Vea también  
 [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)   
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
  
  
