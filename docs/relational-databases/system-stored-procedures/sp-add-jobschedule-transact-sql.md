---
title: sp_add_jobschedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobschedule
- sp_add_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobschedule
ms.assetid: ffce19d9-d1d6-45b4-89fd-ad0f60822ba0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 06dbee74cfb3e2d5e697ea9594d46c98557de8ef
ms.sourcegitcommit: df1f71231f8edbdfe76e8851acf653c25449075e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2019
ms.locfileid: "70810494"
---
# <a name="sp_add_jobschedule-transact-sql"></a>sp_add_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Crea una programación para un trabajo del Agente SQL.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  > [!IMPORTANT]  
  > En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_jobschedule [ @job_id = ] job_id, | [ @job_name = ] 'job_name', [ @name = ] 'name'  
     [ , [ @enabled = ] enabled_flag ]  
     [ , [ @freq_type = ] frequency_type ]  
     [ , [ @freq_interval = ] frequency_interval ]  
     [ , [ @freq_subday_type = ] frequency_subday_type ]  
     [ , [ @freq_subday_interval = ] frequency_subday_interval ]  
     [ , [ @freq_relative_interval = ] frequency_relative_interval ]  
     [ , [ @freq_recurrence_factor = ] frequency_recurrence_factor ]  
     [ , [ @active_start_date = ] active_start_date ]  
     [ , [ @active_end_date = ] active_end_date ]  
     [ , [ @active_start_time = ] active_start_time ]  
     [ , [ @active_end_time = ] active_end_time ]  
     [ , [ @schedule_id = ] schedule_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] job_id`Número de identificación del trabajo al que se agrega la programación. *job_id* es de tipo **uniqueidentifier**y no tiene ningún valor predeterminado.  
  
`[ @job_name = ] 'job_name'`Nombre del trabajo al que se agrega la programación. *job_name* es de tipo **nvarchar (128)** y no tiene ningún valor predeterminado.  
  
> [!NOTE]  
>  Se debe especificar *job_id* o *job_name* , pero no se pueden especificar ambos.  
  
`[ @name = ] 'name'`Nombre de la programación. *Name* es de tipo **nvarchar (128)** y no tiene ningún valor predeterminado.  
  
`[ @enabled = ] enabled_flag`Indica el estado actual de la programación. *enabled_flag* es de **tinyint**y su valor predeterminado es **1** (habilitado). Si es **0**, la programación no está habilitada. Si la programación está deshabilitada, el trabajo no se ejecutará.  
  
`[ @freq_type = ] frequency_type`Valor que indica cuándo se va a ejecutar el trabajo. *frequency_type* es de **tipo int**, su valor predeterminado es **0**y puede tener uno de los valores siguientes:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente, con respecto a *frequency_interval.*|  
|**64**|Se ejecuta cuando se inicia el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**128**|Se ejecuta cuando el equipo está inactivo.|  
  
`[ @freq_interval = ] frequency_interval`Día en el que se ejecuta el trabajo. *frequency_interval* es de **tipo int**, su valor predeterminado es 0 y depende del valor de *frequency_type* , tal y como se indica en la tabla siguiente:  
  
|Valor|Efecto|  
|-----------|------------|  
|**1** (una vez)|*frequency_interval* no se utiliza.|  
|**4** (diariamente)|Cada *frequency_interval* días.|  
|**8** (semanalmente)|*frequency_interval* es uno o más de los siguientes (combinados con un operador lógico or):<br /><br /> 1 = Domingo<br /><br /> 2 = Lunes<br /><br /> 4 = martes<br /><br /> 8 = miércoles<br /><br /> 16 = jueves<br /><br /> 32 = viernes<br /><br /> 64 = sábado|  
|**16** (mensualmente)|En el día *frequency_interval* del mes.|  
|**32** (relativo mensual)|*frequency_interval* es uno de los siguientes:<br /><br /> 1 = Domingo<br /><br /> 2 = Lunes<br /><br /> 3 = Martes<br /><br /> 4 = Miércoles<br /><br /> 5 = Jueves<br /><br /> 6 = Viernes<br /><br /> 7 = Sábado<br /><br /> 8 = Día<br /><br /> 9 = Día de la semana<br /><br /> 10 = Día del fin de semana|  
|**64** (cuando se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicia el servicio del agente)|*frequency_interval* no se utiliza.|  
|**128**|*frequency_interval* no se utiliza.|  
  
`[ @freq_subday_type = ] frequency_subday_type`Especifica las unidades para *frequency_subday_interval*. *frequency_subday_type* es de **tipo int**, no tiene ningún valor predeterminado y puede tener uno de los valores siguientes:  
  
|Valor|Descripción (unidad)|  
|-----------|--------------------------|  
|**0x1**|A la hora especificada|  
|**0x4**|Minutos|  
|**0x8**|Horas|  
  
`[ @freq_subday_interval = ] frequency_subday_interval`Número de períodos de *frequency_subday_type* entre cada ejecución del trabajo. *frequency_subday_interval* es de **tipo int**y su valor predeterminado es 0.  
  
`[ @freq_relative_interval = ] frequency_relative_interval`Define más el *frequency_interval* cuando *frequency_type* se establece en **32** (relativo mensual).  
  
 *frequency_relative_interval* es de **tipo int**, no tiene ningún valor predeterminado y puede tener uno de los valores siguientes:  
  
|Valor|Descripción (unidad)|  
|-----------|--------------------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
  
 *frequency_relative_interval* indica la aparición del intervalo. Por ejemplo, si *frequency_relative_interval* se establece en **2**, *frequency_type* se establece en **32**y *frequency_interval* se establece en **3**, el trabajo programado se produciría el segundo martes de cada mes.  
  
`[ @freq_recurrence_factor = ] frequency_recurrence_factor`Número de semanas o meses entre la ejecución programada del trabajo. *frequency_recurrence_factor* solo se utiliza si *frequency_type* se establece en **8**, **16**o **32**. *frequency_recurrence_factor* es de **tipo int**y su valor predeterminado es 0.  
  
`[ @active_start_date = ] active_start_date`Fecha en la que puede comenzar la ejecución del trabajo. *active_start_date* es de **tipo int**y no tiene ningún valor predeterminado. La fecha tiene el formato AAAAMMDD. Si *active_start_date* está establecido, la fecha debe ser mayor o igual que 19900101.  
  
 Una vez creada la programación, revise la fecha de inicio y confirme que es correcta. Para obtener más información, vea la sección sobre la programación de la fecha de inicio en [crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
`[ @active_end_date = ] active_end_date`Fecha en la que se puede detener la ejecución del trabajo. *active_end_date* es de **tipo int**y no tiene ningún valor predeterminado. La fecha tiene el formato AAAAMMDD.  
  
`[ @active_start_time = ] active_start_time`Hora de un día entre *active_start_date* y *active_end_date* para iniciar la ejecución del trabajo. *active_start_time* es de **tipo int**y no tiene ningún valor predeterminado. La hora tiene el formato HHMMSS en un reloj de 24 horas.  
  
`[ @active_end_time = active_end_time_`Hora de cualquier día entre *active_start_date* y *active_end_date* para finalizar la ejecución del trabajo. *active_end_time* es de **tipo int**y no tiene ningún valor predeterminado. La hora tiene el formato HHMMSS en un reloj de 24 horas.  
  
`[ @schedule_id = schedule_idOUTPUT`Número de identificación de la programación asignado a la programación si se ha creado correctamente. *schedule_id* es una variable de salida de tipo **int**y no tiene ningún valor predeterminado.  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT`Identificador único de la programación. *schedule_uid* es una variable de tipo **uniqueidentifier**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Ahora, las programaciones de trabajos se pueden administrar independientemente de los trabajos. Para agregar una programación a un trabajo, use **sp_add_schedule** para crear la programación y **sp_attach_schedule** para adjuntar la programación a un trabajo.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
 
 ## <a name="example"></a>Ejemplo
 En el ejemplo siguiente se asigna una programación de trabajo `SaturdayReports` a la que se ejecutará cada sábado a las 2:00 a.m.
```sql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>Vea también  
 [Crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [Programar un trabajo](../../ssms/agent/schedule-a-job.md)   
 [Crear una programación](../../ssms/agent/create-a-schedule.md)   
 [Procedimientos &#40;almacenados de Agente SQL Server TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
