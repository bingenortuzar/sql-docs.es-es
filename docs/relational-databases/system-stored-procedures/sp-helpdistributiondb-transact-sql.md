---
title: sp_helpdistributiondb (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 90dee1076743ae54201248c808b04c6197d42198
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770928"
---
# <a name="sphelpdistributiondb-transact-sql"></a>sp_helpdistributiondb (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Devuelve las propiedades de la base datos de distribución especificada. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @database = ] 'database_name'`Es el nombre de la base de datos cuyas propiedades se devuelven. *database_name* es de **tipo sysname y su**valor **%** predeterminado es para todas las bases de datos asociadas al distribuidor y en el que el usuario tiene permisos.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre de la base de datos de distribución.|  
|**min_distretention**|**int**|Período mínimo de retención, en horas, antes de que se eliminen las transacciones.|  
|**max_distretention**|**int**|Período máximo de retención, en horas, antes de que se eliminen las transacciones.|  
|**retención del historial**|**int**|Número de horas que se conserva el historial.|  
|**history_cleanup_agent**|**sysname**|Nombre del Agente de limpieza del historial.|  
|**distribution_cleanup_agent**|**sysname**|Nombre del Agente de limpieza de distribución.|  
|**status**|**int**|Exclusivamente para uso interno.|  
|**data_folder**|**nvarchar(255)**|Nombre del directorio que se utiliza para almacenar los archivos de base de datos.|  
|**data_file**|**nvarchar(255)**|Nombre del archivo de la base de datos.|  
|**data_file_size**|**int**|Tamaño inicial del archivo de datos en megabytes.|  
|**log_folder**|**nvarchar(255)**|Nombre del directorio del archivo de registro de la base de datos.|  
|**log_file**|**nvarchar(255)**|Nombre del archivo de registro.|  
|**log_file_size**|**int**|Tamaño inicial del archivo de registro en megabytes.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpdistributiondb** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Los miembros del rol fijo de base de datos **db_owner** o del rol **replmonitor** en una base de datos de distribución y los usuarios de la lista de acceso a la publicación de una publicación que usa la base de datos de distribución pueden ejecutar **sp_helpdistributiondb** para devolver información relacionada con archivos. Los miembros del rol **Public** pueden ejecutar **sp_helpdistributiondb** para devolver información relacionada con archivos de las bases de datos de distribución a las que tienen acceso.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
