---
title: sp_changesubscriber (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42b56712e8b441184d55bf12ce16dbcb55930374
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762780"
---
# <a name="sp_changesubscriber-transact-sql"></a>sp_changesubscriber (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cambia las opciones de un suscriptor. Se actualizan todas las tareas de distribución de los suscriptores de este publicador. Este procedimiento almacenado escribe en la tabla **MSsubscriber_info** de la base de datos de distribución. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changesubscriber [ @subscriber= ] 'subscriber'  
    [ , [ @type= ] type ]  
    [ , [ @login= ] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @commit_batch_size= ] commit_batch_size ]  
    [ , [ @status_batch_size= ] status_batch_size ]  
    [ , [ @flush_frequency= ] flush_frequency ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @security_mode= ] security_mode ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @subscriber = ] 'subscriber'`Es el nombre del suscriptor en el que se van a cambiar las opciones. *Subscriber* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @type = ] type`Es el tipo de suscriptor. el *tipo* es **tinyint**y su valor predeterminado es NULL. **0** indica un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suscriptor. **1** especifica un suscriptor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del servidor de origen de datos ODBC distinto de u otro.  
  
`[ @login = ] 'login'`Es el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador de inicio de sesión de autenticación. *login* es de tipo **sysname** y su valor predeterminado es NULL.  
  
`[ @password = ] 'password'`Es la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contraseña de autenticación. *password* es de **%** **tipo sysname y su**valor predeterminado es. **%** indica que no hay ningún cambio en la propiedad de contraseña.  
  
`[ @commit_batch_size = ] commit_batch_size`Solo se admite por compatibilidad con versiones anteriores.  
  
`[ @status_batch_size = ] status_batch_size`Solo se admite por compatibilidad con versiones anteriores.  
  
`[ @flush_frequency = ] flush_frequency`Solo se admite por compatibilidad con versiones anteriores.  
  
`[ @frequency_type = ] frequency_type`Es la frecuencia con la que se programa la tarea de distribución. *frequency_type* es de **tipo int**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|A petición|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente relativa|  
|**64**|Iniciar automáticamente|  
|**128**|Periódica|  
  
`[ @frequency_interval = ] frequency_interval`Es el intervalo de *frequency_type*. *frequency_interval* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`Es la fecha de la tarea de distribución. Este parámetro se utiliza cuando *frequency_type* se establece en **32** (relativo mensual). *frequency_relative_interval* es de **tipo int**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`Indica la frecuencia con la que debe repetirse la tarea de distribución durante el *frequency_type*definido. *frequency_recurrence_factor* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @frequency_subday = ] frequency_subday`Es la frecuencia con que se vuelve a programar durante el período definido. *frequency_subday* es de **tipo int**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`Es el intervalo de *frequence_subday*. *frequency_subday_interval* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`Es la hora del día en la que la tarea de distribución se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`Es la hora del día a la que la tarea de distribución deja de estar programada, con el formato HHMMSS. *active_end_time_of_day*es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @active_start_date = ] active_start_date`Es la fecha en la que la tarea de distribución se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @active_end_date = ] active_end_date`Es la fecha en la que la tarea de distribución deja de estar programada, con el formato AAAAMMDD. *active_end_date*es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @description = ] 'description'`Es una descripción de texto opcional. la *Descripción* es de tipo **nvarchar (255)** y su valor predeterminado es NULL.  
  
`[ @security_mode = ] security_mode`Es el modo de seguridad implementado. *security_mode* es de **tipo int**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticación|  
|**1**|Autenticación de Windows|  
  
`[ @publisher = ] 'publisher'`Especifica un publicador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no es de. *Publisher* es de **tipo sysname y su**valor predeterminado es NULL.  
  
> [!NOTE]  
>  no se debe usar el publicador al cambiar las propiedades [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de un artículo en un publicador.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changesubscriber** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_changesubscriber**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
