---
title: syscollector_config_store (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_config_store_TSQL
- syscollector_config_store
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_config_store view
ms.assetid: f15f6b05-6808-4b76-b6a8-48dec844cf63
author: stevestein
ms.author: sstein
ms.openlocfilehash: 174fa1af651c2e713bdb91ba217e896b833467b2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060372"
---
# <a name="syscollectorconfigstore-transact-sql"></a>syscollector_config_store (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve las propiedades que se aplican a todo el recopilador de datos, a diferencia de una instancia de conjunto de recopilación. Cada fila en esta vista describe una propiedad de recopilador de datos concreta, como el nombre del almacén de datos de administración y el nombre de instancia donde se encuentra el almacén de datos de administración.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|parameter_name|**nvarchar(128)**|El nombre de la propiedad. No admite valores NULL.|  
|parameter_value|**sql_variant**|Valor real de la propiedad. Acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso SELECT en la vista o la pertenencia a los roles fijos de base de datos dc_operator, dc_proxy o dc_admin.  
  
## <a name="remarks"></a>Comentarios  
 La lista de propiedades disponibles se corrige y sus valores solo se pueden cambiar usando el procedimiento almacenado adecuado. En la tabla siguiente se describen las propiedades que se exponen a través de esta vista.  
  
|Nombre de propiedad|Descripción|  
|-------------------|-----------------|  
|CacheDirectory|Nombre del directorio en el sistema de archivos donde los paquetes de tipos de recopilador almacenan la información temporal.<br /><br /> NULL = se usa el directorio temporal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|CacheWindow|Indica la directiva de retención de datos del directorio de memoria caché para las cargas de datos que no han podido realizarse.<br /><br /> -1 = retener los datos de todas las cargas con errores.<br /><br /> 0 = no retener ningún dato de las cargas con errores.<br /><br /> *n* = retener los datos de *n* cargas previas con errores, donde *n* > = 1.<br /><br /> Utilice el procedimiento almacenado sp_syscollector_set_cache_window para cambiar este valor.|  
|CollectorEnabled|Indica el estado del recopilador de datos.<br /><br /> 0 = deshabilitado<br /><br /> 1 = habilitado<br /><br /> Utilice el procedimiento almacenado sp_syscollector_enable_collector o sp_syscollector_disable_collector para cambiar este valor.|  
|MDWDatabase|Nombre del almacén de administración de datos. Use el procedimiento almacenado sp_syscollector_set_warehouse_database_name para cambiar este valor.|  
|MDWInstance|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el almacén de administración de datos. Use el procedimiento almacenado sp_syscollector_set_warehouse_instance_name para cambiar este valor.|  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se consulta la vista syscollector_config_store.  
  
```sql  
SELECT parameter_name, parameter_value  
FROM msdb.dbo.syscollector_config_store;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Vistas del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [sp_syscollector_set_warehouse_database_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)   
 [sp_syscollector_set_warehouse_instance_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
