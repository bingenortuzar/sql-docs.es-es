---
title: sys.registered_search_property_lists (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- registered_search_property_lists_TSQL
- sys.registered_search_property_lists
- registered_search_property_lists
- sys.registered_search_property_lists_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- sys.registered_search_property_lists catalog view
- search property lists [SQL Server], viewing
ms.assetid: 630d4caa-9bea-4cd3-a5b1-01098b0855fc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 87af4645a052001ddfc2d0540b6b40e75e3dbb20
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067850"
---
# <a name="sysregisteredsearchpropertylists-transact-sql"></a>sys.registered_search_property_lists (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para cada lista de propiedades de búsqueda de la base de datos actual.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|Identificador de la lista de propiedades.|  
|**name**|**sysname**|Nombre de la lista de propiedades.|  
|**create_date**|**datetime**|Feche en que se creó la lista de propiedades.|  
|**modify_date**|**datetime**|Fecha en que se modificó la lista propiedades por última vez mediante una instrucción ALTER.|  
|**principal_id**|**int**|Propietario de la lista de propiedades.|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información, vea [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="permissions"></a>Permisos  
 La visibilidad de los metadatos en las listas de propiedades se limita a aquellas de las que se es propietario o en las que se tenga concedido algún permiso REFERENCE.  
  
> [!NOTE]  
>  El propietario de lista de propiedades de búsqueda puede conceder permisos REFERENCE o CONTROL en la lista. Los usuarios con permiso CONTROL también pueden conceder el permiso REFERENCE a otros usuarios.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestran el identificador y nombre de las listas de propiedades de búsquedas en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT property_list_id, name FROM sys.registered_search_property_lists;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
  
