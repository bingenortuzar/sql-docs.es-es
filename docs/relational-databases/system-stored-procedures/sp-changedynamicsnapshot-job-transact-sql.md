---
title: sp_changedynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedynamicsnapshot_job
- sp_changedynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_changedynamicsnapshot_job
ms.assetid: ea0dacd2-a5fd-42f4-88dd-7d289b0ae017
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4db6a29d92fe093e9704f88fcc528c9fa687ccff
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768948"
---
# <a name="spchangedynamicsnapshotjob-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Modifica el trabajo de agente que genera la instantánea para una suscripción a una publicación con un filtro de fila con parámetros. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changedynamicsnapshot_job [ @publication = ] 'publication'  
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`Es el nombre del trabajo de instantánea que se va a cambiar. *dynamic_snapshot_jobname*es de **tipo sysname y su**valor predeterminado es N '% '. Si se especifica *dynamic_snapshot_jobid* , debe usar el valor predeterminado para *dynamic_snapshot_jobname*.  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`Es el identificador del trabajo de instantánea que se va a cambiar. *dynamic_snapshot_jobid* es de tipo **uniqueidentifier**y su valor predeterminado es NULL. Si se especifica *dynamic_snapshot_jobname*, debe usar el valor predeterminado para *dynamic_snapshot_jobid*.  
  
`[ @frequency_type = ] frequency_type`Es la frecuencia con la que se programa el agente. *frequency_type* es de **tipo int**y puede tener uno de los valores siguientes.  
  
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
|NULL (predeterminado)||  
  
`[ @frequency_interval = ] frequency_interval`Los días en los que se ejecuta el agente. *frequency_interval* es de **tipo int**y puede tener uno de los valores siguientes.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Domingo|  
|**2**|Lunes|  
|**3**|Martes|  
|**4**|Miércoles|  
|**5**|Jueves|  
|**6**|Viernes|  
|**7**|Sábado|  
|**8**|Day|  
|**9**|Días de la semana|  
|**10**|Días del fin de semana|  
|NULL (predeterminado)||  
  
`[ @frequency_subday = ] frequency_subday`Es la frecuencia con que se vuelve a programar durante el período definido. *frequency_subday* es de **tipo int**y puede tener uno de los valores siguientes.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (predeterminado)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`Es el intervalo de *frequency_subday*. *frequency_subday_interval* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`Es la fecha en la que se ejecuta el Agente de mezcla. Este parámetro se utiliza cuando *frequency_type* se establece en **32** (relativo mensual). *frequency_relative_interval* es de **tipo int**y puede tener uno de los valores siguientes.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
|NULL (predeterminado)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @active_start_date = ] active_start_date`Es la fecha en la que se programa el Agente de mezcla por primera vez, con el formato AAAAMMDD. *active_start_date* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @active_end_date = ] active_end_date`Es la fecha en la que el Agente de mezcla deja de estar programado, con el formato AAAAMMDD. *active_end_date* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`Es la hora del día a la que se programa el Agente de mezcla por primera vez, con el formato HHMMSS. *active_start_time_of_day* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`Es la hora del día en que el Agente de mezcla deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @job_login = ] 'job_login'`Es la [!INCLUDE[msCoName](../../includes/msconame-md.md)] cuenta de Windows con la que se ejecuta la agente de instantáneas cuando se genera la instantánea para una suscripción mediante un filtro de fila con parámetros. *job_login* es de tipo **nvarchar (257)** y su valor predeterminado es NULL.  
  
`[ @job_password = ] 'job_password'`Es la contraseña de la cuenta de Windows con la que se ejecuta el Agente de instantáneas al generar la instantánea para una suscripción mediante un filtro de fila con parámetros. *job_password* es de tipo **nvarchar (257)** y su valor predeterminado es NULL.  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changedynamicsnapshot_job** se utiliza en la replicación de mezcla para publicaciones con filtros de fila con parámetros.  
  
 Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_changedynamicsnapshot_job**.  
  
## <a name="see-also"></a>Vea también  
 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  (Ver y modificar la configuración de seguridad de la replicación)  
 [Instantáneas para publicaciones de combinación con filtros con parámetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
  
