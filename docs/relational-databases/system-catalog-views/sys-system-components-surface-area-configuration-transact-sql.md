---
title: Sys.system_components_surface_area_configuration (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.system_components_surface_area_configuration_TSQL
- system_components_surface_area_configuration
- system_components_surface_area_configuration_TSQL
- sys.system_components_surface_area_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_components_surface_area_configuration catalog view
ms.assetid: d9920008-3387-4f9e-8f21-47473f2ba04f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 665e73b3cd072bfffc214c518d75d96af3591f94
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108869"
---
# <a name="syssystemcomponentssurfaceareaconfiguration-transact-sql"></a>sys.system_components_surface_area_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada objeto de sistema ejecutable que un componente de configuración del área expuesta puede habilitar o deshabilitar. Para obtener más información, vea [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**component_name**|**sysname**|Nombre del componente. Tendrá la intercalación de palabras clave, Latin1_General_CI_AS_KS_WS. No puede ser NULL.|  
|**database_name**|**sysname**|Base de datos que contiene el objeto. Tendrá la intercalación de palabras clave, Latin1_General_CI_AS_KS_WS. Debe ser una de las siguientes:<br /><br /> **maestra**<br /><br /> **msdb**<br /><br /> **MSSQLSYSTEMRESOURCE**|  
|**schema_name**|**sysname**|Esquema que contiene el objeto. Tendrá la intercalación de palabras clave, Latin1_General_CI_AS_KS_WS. No puede ser NULL.|  
|**object_name**|**sysname**|Nombre del objeto. Tendrá la intercalación de palabras clave, Latin1_General_CI_AS_KS_WS. No puede ser NULL.|  
|**state**|**tinyint**|0 = Deshabilitado<br /><br /> 1 = Habilitado|  
|**type**|**char(2)**|Tipo de objeto. Puede ser uno de los valores siguientes:<br /><br /> P = SQL_STORED_PROCEDURE<br /><br /> PC = CLR_STORED_PROCEDURE<br /><br /> FN = SQL_SCALAR_FUNCTION<br /><br /> FS = CLR_SCALAR_FUNCTION<br /><br /> FT = CLR_TABLE_VALUED_FUNCTION<br /><br /> IF = SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> TF = SQL_TABLE_VALUED_FUNCTION<br /><br /> X = EXTENDED_STORED_PROCEDURE|  
|**type_desc**|**nvarchar(60)**|Nombre descriptivo del tipo de objeto.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
