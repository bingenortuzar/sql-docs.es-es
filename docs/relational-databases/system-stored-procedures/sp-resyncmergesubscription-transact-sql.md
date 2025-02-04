---
title: sp_resyncmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resyncmergesubscription_TSQL
- sp_resyncmergesubscription
helpviewer_keywords:
- sp_resyncmergesubscription
ms.assetid: e04d464a-60ab-4b39-a710-c066025708e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: e77488a379543dd6f2749a07048fa67a92d530ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041030"
---
# <a name="spresyncmergesubscription-transact-sql"></a>sp_resyncmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Vuelve a sincronizar una suscripción de combinación en el estado de validación conocido que especifique. Esto le permite exigir convergencia o sincronizar la base de datos de suscripciones en un punto específico del tiempo, como la última vez que hubo una validación correcta o en una fecha específica. La instantánea no se vuelve a aplicar cuando se sincroniza de nuevo una suscripción utilizando este método. Este procedimiento almacenado no se utiliza para suscripciones de replicación de instantáneas ni replicación transaccional. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_resyncmergesubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
        , [ @publication = ] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @resync_type = ] resync_type ]  
    [ , [ @resync_date_str = ] resync_date_string ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` Es el nombre del publicador. *publicador* es **sysname**, su valor predeterminado es null. El valor NULL es válido si se ejecuta el procedimiento almacenado en el publicador. Si el procedimiento almacenado se ejecuta en el suscriptor, se debe especificar un publicador.  
  
`[ @publisher_db = ] 'publisher_db'` Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, su valor predeterminado es null. El valor NULL es válido si se ejecuta el procedimiento almacenado en el publicador de la base de datos de publicación. Si el procedimiento almacenado se ejecuta en el suscriptor, se debe especificar un publicador.  
  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación*es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @subscriber = ] 'subscriber'` Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es null. El valor NULL es válido si el procedimiento almacenado se ejecuta en el suscriptor. Si el procedimiento almacenado se ejecuta en el publicador, se debe especificar un suscriptor.  
  
`[ @subscriber_db = ] 'subscriber_db'` Es el nombre de la base de datos de suscripción. *subscription_db* es **sysname**, su valor predeterminado es null. El valor NULL es válido si el procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripciones. Si el procedimiento almacenado se ejecuta en el publicador, se debe especificar un suscriptor.  
  
`[ @resync_type = ] resync_type` Define cuándo debe comenzar la resincronización. *resync_type* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|La sincronización comienza después de la instantánea inicial. Esta es la opción que consume más recursos, puesto que se vuelven a aplicar al suscriptor todos los cambios a partir de la instantánea inicial.|  
|**1**|La sincronización comienza después de la última validación correcta. Todas las generaciones nuevas o incompletas originadas a partir de la última validación correcta se aplicarán de nuevo al suscriptor.|  
|**2**|La sincronización comienza desde la fecha dada en *resync_date_str*. Todas las generaciones nuevas o incompletas originadas después de la fecha se vuelven a aplicar al suscriptor.|  
  
`[ @resync_date_str = ] resync_date_string` Define la fecha de cuándo debe comenzar la resincronización. *resync_date_string* es **nvarchar (30)** , su valor predeterminado es null. Este parámetro se usa cuando el *resync_type* es un valor de **2**. La fecha proporcionada se convierte en su equivalente **datetime** valor.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_resyncmergesubscription** se utiliza en la replicación de mezcla.  
  
 Un valor de **0** para el *resync_type* parámetro, que vuelve a aplicar todos los cambios desde la instantánea inicial, puede ser que consumen muchos recursos, pero posiblemente muchos menos que una reinicialización completa. Por ejemplo, si la instantánea inicial tuvo lugar hace un mes, este valor dará lugar a que se apliquen de nuevo los datos del pasado mes. Si la instantánea inicial contenía 1 GB de datos, pero la cantidad de cambios del mes pasado ocupaba 2 MB de datos cambiados, sería mucho más eficaz volver a aplicar los datos que aplicar de nuevo la instantánea de 1 GB completa.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_resyncmergesubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
