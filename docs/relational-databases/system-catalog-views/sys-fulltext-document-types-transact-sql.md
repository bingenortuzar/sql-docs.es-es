---
title: sys.fulltext_document_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_document_types_TSQL
- fulltext_document_types
- fulltext_document_types_TSQL
- sys.fulltext_document_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_document_types catalog view
ms.assetid: 156fcfa4-7304-4a5c-b96f-1c3e061e5df0
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e60f977c220d14680499ca12a4884e912587b7b6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133849"
---
# <a name="sysfulltextdocumenttypes-transact-sql"></a>sys.fulltext_document_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada tipo de documento disponible para operaciones de indización de texto completo. Cada fila representa la interfaz IFilter registrada en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**document_type**|**sysname**|Extensión de archivo del tipo de documento admitido.<br /><br /> Este valor se puede usar para identificar el filtro que se usará durante la indización de texto completo de las columnas de tipo **varbinary (max)** o **imagen**.|  
|**class_id**|**uniqueidentifier**|GUID de la clase de IFilter que admite la extensión de archivo.|  
|**path**|**nvarchar(260)**|Ruta de acceso al archivo DLL de IFilter. La ruta de acceso solo es visible para los miembros del rol fijo de servidor **serveradmin** .|  
|**version**|**sysname**|Versión del archivo DLL de IFilter.|  
|**manufacturer**|**sysname**|Nombre del fabricante de IFilter.<br /><br /> Nota: Solo los documentos con el fabricante como [!INCLUDE[msCoName](../../includes/msconame-md.md)] se admiten en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
