---
title: sp_helptracertokenhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokenhistory_TSQL
- sp_helptracertokenhistory
helpviewer_keywords:
- sp_helptracertokenhistory
ms.assetid: 96910d1c-be76-43eb-9c93-4477e6761749
author: stevestein
ms.author: sstein
ms.openlocfilehash: b8755bea5e318d1ded2631a2253134fd8721a421
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771155"
---
# <a name="sphelptracertokenhistory-transact-sql"></a>sp_helptracertokenhistory (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Devuelve información detallada de latencia acerca de los testigos de seguimiento especificados. Se devuelve una fila por cada suscriptor. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación o en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helptracertokenhistory [ @publication = ] 'publication'   
        , [ @tracer_id = ] tracer_id  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación en la que se insertó el testigo de seguimiento. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @tracer_id = ] tracer_id`Es el identificador del testigo de seguimiento en la [tabla &#40;MStracer_tokens de Transact&#41; -SQL](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) para la que se devuelve información del historial. *tracer_id* es de **tipo int**y no tiene ningún valor predeterminado.  
  
`[ @publisher = ] 'publisher'`Nombre del publicador. *Publisher* es de **tipo sysname y su**valor predeterminado es NULL.  
  
> [!NOTE]
>  Este parámetro solo debe especificarse para los publicadores que no sean de [!INCLUDE[msCoName](../../includes/msconame-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
`[ @publisher_db = ] 'publisher_db'`Nombre de la base de datos de publicación. *publisher_db* es de **tipo sysname y su**valor predeterminado es NULL. Si el procedimiento almacenado se ejecuta en el publicador, se omite este parámetro.  
  
## <a name="result-set"></a>Tipo de cursor  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**distributor_latency**|**bigint**|Número de segundos entre la confirmación del registro del token de seguimiento en el publicador y la confirmación del registro en el distribuidor.|  
|**suscriptor**|**sysname**|Nombre del suscriptor que ha recibido el token de seguimiento.|  
|**subscriber_db**|**sysname**|Nombre de la base de datos de suscripciones en la que se ha insertado el testigo de seguimiento.|  
|**subscriber_latency**|**bigint**|Número de segundos entre la confirmación del registro del token de seguimiento en el distribuidor y la confirmación del registro en el suscriptor.|  
|**overall_latency**|**bigint**|Número de segundos entre la confirmación del registro del token de seguimiento en el publicador y la confirmación del registro del token en el suscriptor.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helptracertokenhistory** se utiliza en la replicación transaccional.  
  
 Ejecute [sp_helptracertokens &#40;de Transact-&#41; SQL](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) para obtener una lista de testigos de seguimiento para la publicación.  
  
 Un valor NULL en el conjunto de resultados significa que no es posible calcular las estadísticas de latencia. Esto es debido a que no se ha recibido el token de seguimiento en el distribuidor o en uno de los suscriptores.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokenhistor_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** , del rol fijo de base de datos **db_owner** en la base de datos de publicación o de los roles fijos de base de datos **db_owner** o **replmonitor** de la base de datos de distribución pueden ejecutar **SP _ helptracertokenhistory**.  
  
## <a name="see-also"></a>Vea también  
 [Medir la latencia y validar las conexiones de la replicación transaccional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
