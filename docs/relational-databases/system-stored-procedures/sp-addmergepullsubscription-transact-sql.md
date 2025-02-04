---
title: sp_addmergepullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1b0a20e2bc7a167698353db31e7c0411fb1a6961
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769141"
---
# <a name="spaddmergepullsubscription-transact-sql"></a>sp_addmergepullsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Agrega una suscripción de extracción a una publicación de combinación. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addmergepullsubscription [ @publication= ] 'publication'   
    [ , [ @publisher= ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @subscriber_type= ] 'subscriber_type' ]   
    [ , [ @subscription_priority= ] subscription_priority ]   
    [ , [ @sync_type= ] 'sync_type' ]   
    [ , [ @description= ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher = ] 'publisher'`Es el nombre del publicador. *Publisher* es de **tipo sysname**y su valor predeterminado es el nombre del servidor local. El publicador debe ser un servidor válido.  
  
`[ @publisher_db = ] 'publisher_db'`Es el nombre de la base de datos del publicador. *publisher_db* es de **tipo sysname y su**valor predeterminado es NULL.  
  
`[ @subscriber_type = ] 'subscriber_type'`Es el tipo de suscriptor. *subscriber_type* es de tipo **nvarchar (15)** y puede ser **global**, **local** o **Anonymous**. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, se hace referencia a las suscripciones locales como suscripciones de cliente y suscripciones globales como suscripciones de servidor.  
  
`[ @subscription_priority = ] subscription_priority`Es la prioridad de la suscripción. *subscription_priority*es **real**y su valor predeterminado es NULL. En el caso de las suscripciones locales y anónimas, la prioridad es **0,0**. La prioridad la utiliza el solucionador predeterminado para elegir un ganador cuando se detectan conflictos. Para los suscriptores globales, la prioridad de la suscripción debe ser menor que 100, que es la prioridad del publicador.  
  
`[ @sync_type = ] 'sync_type'`Es el tipo de sincronización de la suscripción. *sync_type*es de tipo **nvarchar (15)** y su valor predeterminado es **Automatic**. Puede ser **automático** o **ninguno**. Si es **automático**, el esquema y los datos iniciales de las tablas publicadas se transfieren primero al suscriptor. Si no hay **ninguno**, se supone que el suscriptor ya tiene el esquema y los datos iniciales de las tablas publicadas. Las tablas y los datos del sistema se transfieren siempre.  
  
> [!NOTE]  
>  No se recomienda especificar un valor de **None**.  
  
`[ @description = ] 'description'`Es una breve descripción de esta suscripción de extracción. la *Descripción*es de tipo **nvarchar (255)** y su valor predeterminado es NULL. El monitor de replicación muestra este valor en la columna **nombre descriptivo** , que se puede utilizar para ordenar las suscripciones de una publicación supervisada.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addmergepullsubscription** se utiliza para la replicación de mezcla.  
  
 Si utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el agente para sincronizar la suscripción, el procedimiento almacenado [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) se debe ejecutar en el suscriptor para crear un agente y un trabajo para sincronizar con la publicación.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_addmergepullsubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [Transact &#40;-SQL de sp_changemergepullsubscription&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [Transact &#40;-SQL de sp_helpmergepullsubscription&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
