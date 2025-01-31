---
title: sp_helpdistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistpublisher_TSQL
- sp_helpdistpublisher
helpviewer_keywords:
- sp_helpdistpublisher
ms.assetid: f207c22d-8fb2-4756-8a9d-6c51d6cd3470
author: stevestein
ms.author: sstein
ms.openlocfilehash: a47a81b2b19ceccf76a031e298ab60cf4a6f8c9a
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770950"
---
# <a name="sphelpdistpublisher-transact-sql"></a>sp_helpdistpublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Devuelve las propiedades de los publicadores que utilizan un distribuidor. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`Es el publicador cuyas propiedades se devuelven. *Publisher* es de **%** **tipo sysname y su**valor predeterminado es.  
  
`[ @check_user = ] check_user` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre del publicador.|  
|**distribution_db**|**sysname**|Base de datos de distribución del publicador especificado.|  
|**security_mode**|**int**|Modo de seguridad empleado por los agentes de replicación para conectar al publicador para suscripciones de actualización en cola, o con un publicador que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **0**  =  autenticación[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **1** = autenticación de Windows|  
|**login**|**sysname**|Nombre de inicio de sesión empleado por los agentes de replicación para conectar al publicador para suscripciones de actualización en cola, o con un publicador que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**nvarchar(524)**|Contraseña devuelta (en forma de cifrado sencillo). La contraseña es NULL para los usuarios que no sean **sysadmin**.|  
|**active**|**bit**|Indica si un publicador remoto utiliza el servidor local como distribuidor:<br /><br /> **0** = No<br /><br /> **1** = Sí|  
|**working_directory**|**nvarchar(255)**|Nombre del directorio de trabajo.|  
|**trusted**|**bit**|Si se necesita la contraseña cuando un publicador se conecta con el distribuidor. En [!INCLUDE[msCoName](../../includes/msconame-md.md)] y[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] versiones posteriores, siempre debe devolver **0**, lo que significa que se necesita la contraseña.|  
|**thirdparty_flag**|**bit**|Indica si la publicación está habilitada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o por una aplicación de terceros:<br /><br /> **0, Oracle o** = el publicador de puerta de enlace de Oracle.[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **1** = el publicador se ha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrado con mediante una aplicación de otro fabricante.|  
|**publisher_type**|**sysname**|Tipo de publicador; puede ser uno de los siguientes:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **PUERTA DE ENLACE DE ORACLE**|  
|**publisher_data_source**|**nvarchar(4000)**|Nombre del origen de datos OLE DB en el publicador.|  
|**storage_connection_string**|**nvarchar(4000)**|Clave de acceso de almacenamiento para el directorio de trabajo cuando el distribuidor o el publicador en Azure SQL Database.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpdistpublisher** se utiliza en todos los tipos de replicación.  
  
 **sp_helpdistpublisher** no mostrará el inicio de sesión o la contraseña del publicador en el conjunto de resultados para inicios de sesión que no sean de**sysadmin** .  
  
## <a name="permissions"></a>Permisos  
 Los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **Sp_helpdistpublisher** para cualquier publicador que use el servidor local como distribuidor. Los miembros del rol fijo de base de datos **db_owner** o del rol **replmonitor** en una base de datos de distribución pueden ejecutar **sp_helpdistpublisher** para cualquier publicador que use esa base de datos de distribución. Los usuarios de la lista de acceso a la publicación para una publicación en el publicador especificado pueden ejecutar **sp_helpdistpublisher**. Si no se especifica Publisher, se devuelve información para todos los publicadores para los que el usuario tiene derechos de acceso.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
