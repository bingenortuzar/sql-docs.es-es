---
title: Sys.plan_guides (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.planguides_TSQL
- plan_guides
- sys.planguides
- plan_guides_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.plan_guides catalog view
ms.assetid: 3dde0397-ef6f-4b3f-8250-3f25584eb62b
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 19b78ff53b5640d74b49d2e5956c39aa1df2e230
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068069"
---
# <a name="sysplanguides-transact-sql"></a>sys.plan_guides (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contiene una fila por cada guía de plan de la base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**plan_guide_id**|**int**|Identificador único de la guía de plan en la base de datos.|  
|**name**|**sysname**|Nombre de la guía de plan.|  
|**create_date**|**datetime**|Fecha y hora de creación de la guía de plan.|  
|**modify_date**|**Fecha y hora**|Fecha de la última modificación de la guía de plan.|  
|**is_disabled**|**bit**|1 = La guía de plan está deshabilitada.<br /><br /> 0 = La guía de plan está habilitada.|  
|**query_text**|**nvarchar(max)**|Es el texto de la consulta en que se crea la guía de plan.|  
|**scope_type**|**tinyint**|Identifica el ámbito de la guía de plan.<br /><br /> 1 = OBJECT<br /><br /> 2 = SQL<br /><br /> 3 = TEMPLATE|  
|**scope_type_desc**|**nvarchar(60)**|Descripción del ámbito de la guía de plan.<br /><br /> OBJECT<br /><br /> SQL<br /><br /> TEMPLATE|  
|**scope_object_id**|**Int**|Id. del objeto que define el ámbito de la guía de plan si el ámbito es OBJECT.<br /><br /> Es NULL si el ámbito de la guía de plan no es OBJECT.|  
|**scope_batch**|**nvarchar(max)**|Texto del lote si **scope_type** es SQL.<br /><br /> Es NULL si el tipo de lote no es SQL.<br /><br /> Si es NULL y **scope_type** es SQL, el valor de **query_text** se aplica.|  
|**parameters**|**nvarchar(max)**|Es la cadena que define la lista de parámetros asociados a la guía de plan.<br /><br /> NULL = No se asocia ninguna lista de parámetros a la guía de plan.|  
|**sugerencias**|**nvarchar(max)**|Son las sugerencias de la cláusula OPTION asociadas a la guía de plan.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
