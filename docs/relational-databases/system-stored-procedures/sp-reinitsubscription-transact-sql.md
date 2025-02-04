---
title: sp_reinitsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitsubscription
- sp_reinitsubscription_TSQL
helpviewer_keywords:
- sp_reinitsubscription
ms.assetid: d56ae218-6128-4ff9-b06c-749914505c7b
author: stevestein
ms.author: sstein
ms.openlocfilehash: eaeeaa5009cb119b40dcde9b8f9baa170d8f7bef
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762530"
---
# <a name="sp_reinitsubscription-transact-sql"></a>sp_reinitsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Marca las suscripciones para reinicialización. Este procedimiento almacenado se ejecuta en el publicador para suscripciones de inserción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_reinitsubscription [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
        , [ @subscriber = ] 'subscriber'  
    [ , [ @destination_db = ] 'destination_db']  
    [ , [ @for_schema_change = ] 'for_schema_change']  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @ignore_distributor_failure = ] ignore_distributor_failure ]   
    [ , [ @invalidate_snapshot = ] invalidate_snapshot ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname y su**valor predeterminado es ALL.  
  
`[ @article = ] 'article'`Es el nombre del artículo. *article* es de **tipo sysname y su**valor predeterminado es ALL. Para una publicación de actualización inmediata, *article* debe ser **All**; de lo contrario, el procedimiento almacenado omite la publicación y notifica un error.  
  
`[ @subscriber = ] 'subscriber'`Es el nombre del suscriptor. *Subscriber* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @destination_db = ] 'destination_db'`Es el nombre de la base de datos de destino. *destination_db* es de **tipo sysname y su**valor predeterminado es ALL.  
  
`[ @for_schema_change = ] 'for_schema_change'`Indica si la reinicialización se produce como resultado de un cambio de esquema en la base de datos de publicación. *for_schema_change* es de **bit**y su valor predeterminado es 0. Si es **0**, las suscripciones activas para publicaciones que permiten la actualización inmediata se reactivan siempre y cuando se reinicialice toda la publicación y no solo algunos de sus artículos. Esto significa que la reinicialización se produce como resultado de un cambio de esquema. Si es **1**, las suscripciones activas no se reactivan hasta que se ejecuta el agente de instantáneas.  
  
`[ @publisher = ] 'publisher'`Especifica un publicador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no es de. *Publisher* es de **tipo sysname y su**valor predeterminado es NULL.  
  
> [!NOTE]  
>  no se debe usar el publicador para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los publicadores.  
  
`[ @ignore_distributor_failure = ] ignore_distributor_failure`Permite la reinicialización incluso si el distribuidor no existe o está sin conexión. *ignore_distributor_failure* es de **bit**y su valor predeterminado es 0. Si es **0**, se produce un error en la reinicialización si el distribuidor no existe o está sin conexión.  
  
`[ @invalidate_snapshot = ] invalidate_snapshot`Invalida la instantánea de publicación existente. *invalidate_snapshot* es de **bit**y su valor predeterminado es 0. Si es **1**, se genera una nueva instantánea para la publicación.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_reinitsubscription** se utiliza en la replicación transaccional.  
  
 **sp_reinitsubscription** no se admite para la replicación transaccional punto a punto.  
  
 Para aquellas suscripciones en las que se aplica automáticamente la instantánea inicial y en las que la publicación no admite suscripciones actualizables, es necesario ejecutar el Agente de instantáneas después de ejecutar el procedimiento almacenado a fin de que el esquema y los archivos del programa de copia masiva estén preparados; a continuación, los Agentes de distribución estarán preparados para volver a sincronizar las suscripciones.  
  
 Para aquellas suscripciones en las que la instantánea inicial se aplica automáticamente y en las que la publicación admite suscripciones actualizables, el Agente de distribución vuelve a sincronizar la suscripción utilizando el esquema y los archivos del programa de copia masiva más recientes creados previamente por el Agente de instantáneas. La Agente de distribución vuelve a sincronizar la suscripción inmediatamente después de que el usuario ejecute **sp_reinitsubscription**, si el agente de distribución no está ocupado; de lo contrario, la sincronización puede producirse después del intervalo de mensajes (especificado por Agente de distribución parámetro del símbolo del sistema: **MessageInterval**).  
  
 **sp_reinitsubscription** no tiene ningún efecto en las suscripciones en las que la instantánea inicial se aplica manualmente.  
  
 Para volver a sincronizar las suscripciones anónimas en una publicación, pase **All** o NULL como *suscriptor*.  
  
 La replicación transaccional admite la reinicialización de suscripciones en el nivel del artículo. La instantánea del artículo se volverá a aplicar en el suscriptor durante la siguiente sincronización una vez que se haya marcado el artículo para reinicializarlo. Sin embargo, si hay artículos dependientes a los que también está suscrito el mismo suscriptor, se puede generar un error al volver a aplicar la instantánea en el artículo, a menos que los artículos dependientes de la publicación se reinicialicen también automáticamente en determinadas circunstancias:  
  
-   Si el comando de creación previa del artículo es 'drop', los artículos de vistas y procedimientos almacenados enlazados a un esquema del objeto base de ese artículo también se marcan para reinicializarlos.  
  
-   Si la opción de esquema del artículo incluye scripting de integridad referencial declarada en las claves principales, los artículos que tienen tablas base con relaciones de clave externa con tablas base del artículo reinicializado también se marcan para reinicializarlos.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_reinittranpushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitsubscription-tr_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** , los miembros del rol fijo de base de datos **db_owner** o el creador de la suscripción pueden ejecutar **sp_reinitsubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Reinicializar una suscripción](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Reinicializar suscripciones](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
