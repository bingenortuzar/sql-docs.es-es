---
title: sp_repldone (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 35cd38269fabba59d257e41141141764b6d4919d
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771112"
---
# <a name="sprepldone-transact-sql"></a>sp_repldone (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Actualiza el registro que identifica la última transacción distribuida del servidor. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!CAUTION]  
>  Si ejecuta **sp_repldone** manualmente, puede invalidar el orden y la coherencia de las transacciones entregadas. **sp_repldone** solo se debe usar para solucionar problemas de replicación según lo indicado por un profesional de soporte técnico de replicación experimentado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_repldone [ @xactid= ] xactid   
        , [ @xact_seqno= ] xact_seqno   
    [ , [ @numtrans= ] numtrans ]   
    [ , [ @time= ] time   
    [ , [ @reset= ] reset ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @xactid = ] xactid`Es el número de secuencia de registro (LSN) del primer registro de la última transacción distribuida del servidor. *xactid* es **binario (10)** y no tiene ningún valor predeterminado.  
  
`[ @xact_seqno = ] xact_seqno`Es el LSN del último registro de la última transacción distribuida del servidor. *xact_seqno* es **binario (10)** y no tiene ningún valor predeterminado.  
  
`[ @numtrans = ] numtrans`Es el número de transacciones distribuidas. *numtrans* es de **tipo int**y no tiene ningún valor predeterminado.  
  
`[ @time = ] time`Es el número de milisegundos, si se proporciona, necesarios para distribuir el último lote de transacciones. *Time* es de **tipo int**y no tiene ningún valor predeterminado.  
  
`[ @reset = ] reset`Es el estado de restablecimiento. *RESET* es de **tipo int**y no tiene ningún valor predeterminado. Si es **1**, todas las transacciones replicadas del registro se marcan como distribuidas. Si es **0**, el registro de transacciones se restablece a la primera transacción replicada y no hay transacciones replicadas marcadas como distribuidas. *RESET* solo es válido cuando *xactid* y *xact_seqno* son NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_repldone** se usa en la replicación transaccional.  
  
 el proceso de registro del log usa **sp_repldone** para realizar el seguimiento de las transacciones que se han distribuido.  
  
 Con **sp_repldone**, puede indicar manualmente al servidor que se ha replicado una transacción (enviada al distribuidor). También le permite cambiar la transacción que está marcada como la siguiente en espera de la replicación. Puede desplazarse hacia delante y hacia atrás en la lista de transacciones replicadas. (Todas las transacciones menores o iguales que esa transacción se marcan como distribuidas.)  
  
 Los parámetros necesarios *xactid* y *xact_seqno* se pueden obtener mediante **sp_repltrans** o **sp_replcmds**.  
  
## <a name="permissions"></a>Permisos  
 Los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_repldone**.  
  
## <a name="examples"></a>Ejemplos  
 Cuando *xactid* es null, *xact_seqno* es NULL y *RESET* es **1**, todas las transacciones replicadas del registro se marcan como distribuidas. Esto resulta útil cuando, por ejemplo, hay transacciones replicadas en el registro de transacciones que ya no son válidas y desea truncar el registro:  
  
```  
EXEC sp_repldone @xactid = NULL, @xact_segno = NULL, @numtrans = 0,     @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  Este procedimiento se puede utilizar en situaciones de emergencia para permitir que se trunque el registro de transacciones cuando existen transacciones pendientes de replicación.  
  
## <a name="see-also"></a>Vea también  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
