---
title: sp_help_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobstep_TSQL
- sp_help_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobstep
ms.assetid: 4a13b804-45f2-4f82-987f-42d9a57dd6db
author: stevestein
ms.author: sstein
ms.openlocfilehash: c65498b25bfbe0a5eee38a43ea212e29edc26295
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090051"
---
# <a name="sphelpjobstep-transact-sql"></a>sp_help_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información para los pasos de un trabajo que el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza para realizar actividades automatizadas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_jobstep { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]   
     [ , [ @step_name = ] 'step_name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_id = ] 'job_id'` El número de identificación del trabajo que se va a devolver información del trabajo. *job_id* es **uniqueidentifier**, su valor predeterminado es null.  
  
`[ @job_name = ] 'job_name'` El nombre del trabajo. *job_name* es **sysname**, su valor predeterminado es NULL.  
  
> [!NOTE]  
>  Cualquier *job_id* o *job_name* debe especificarse, pero no se pueden especificar ambos.  
  
`[ @step_id = ] step_id` El número de identificación del paso del trabajo. Si no se especifica, se incluirán todos los pasos del trabajo. *step_id* es **int**, su valor predeterminado es null.  
  
`[ @step_name = ] 'step_name'` El nombre del paso del trabajo. *Step_name* es **sysname**, su valor predeterminado es null.  
  
`[ @suffix = ] suffix` Una marca que indica si una descripción de texto se anexa a la **marcas** columna en la salida. *sufijo*es **bit**, con el valor predeterminado de **0**. Si *sufijo* es **1**, se agrega una descripción.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**step_id**|**int**|Identificador único del paso.|  
|**step_name**|**sysname**|Nombre del paso del trabajo.|  
|**subsystem**|**nvarchar(40)**|Subsistema en el que se ejecuta el comando del paso.|  
|**command**|**nvarchar(max)**|Comando que se ejecuta en el paso.|  
|**flags**|**int**|Máscara de bits que controla el comportamiento del paso.|  
|**cmdexec_success_code**|**int**|Para un **CmdExec** paso, se trata de procesar el código de salida de un comando correcto.|  
|**on_success_action**|**tinyint**|Acción que se realiza si el paso termina correctamente:<br /><br /> **1** = salir del trabajo que se ha ejecutado correctamente.<br /><br /> **2** = salir del trabajo informa de un error.<br /><br /> **3** = ir al paso siguiente.<br /><br /> **4** = ir al paso.|  
|**on_success_step_id**|**int**|Si **on_success_action** es 4, esto indica que se ejecute el siguiente paso.|  
|**on_fail_action**|**tinyint**|Qué hacer si el paso da error. Los valores son los mismos que **on_success_action**.|  
|**on_fail_step_id**|**int**|Si **on_fail_action** es 4, esto indica que se ejecute el siguiente paso.|  
|**servidor**|**sysname**|Reservado.|  
|**database_name**|**sysname**|Para pasos [!INCLUDE[tsql](../../includes/tsql-md.md)], la base de datos en que se ejecuta el comando.|  
|**database_user_name**|**sysname**|Para pasos [!INCLUDE[tsql](../../includes/tsql-md.md)], el contexto de usuario de la base de datos en que se ejecuta el comando.|  
|**retry_attempts**|**int**|Número máximo de veces que se vuelve a intentar el comando (si no termina correctamente).|  
|**retry_interval**|**int**|Intervalo (en minutos) entre cada nuevo intento.|  
|**os_run_priority**|**int**|Reservado.|  
|**output_file_name**|**nvarchar(200)**|En el comando que se debe escribir la salida de archivo ([!INCLUDE[tsql](../../includes/tsql-md.md)], **CmdExec**, y **PowerShell** solo para los pasos).|  
|**last_run_outcome**|**int**|Resultado del paso la última vez que se ejecutó:<br /><br /> **0** = error<br /><br /> **1** = se ha realizado correctamente<br /><br /> **2** = reintento<br /><br /> **3** = cancelado<br /><br /> **5** = desconocido|  
|**last_run_duration**|**int**|Duración (hhmmss) del paso la última vez que se ejecutó.|  
|**last_run_retries**|**int**|Número de veces que se ha intentado el comando desde que se ejecutó el paso por última vez.|  
|**last_run_date**|**int**|Fecha en que se inició la ejecución del paso por última vez.|  
|**last_run_time**|**int**|Hora en que se inició la ejecución del paso por última vez.|  
|**proxy_id**|**int**|Proxy del paso de trabajo.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_jobstep** está en el **msdb** base de datos.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Los miembros de **SQLAgentUserRole** solo pueden ver los pasos de trabajo para trabajos que les pertenecen.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-return-information-for-all-steps-in-a-specific-job"></a>A. Devolver información de todos los pasos de un trabajo específico  
 En el ejemplo siguiente se devuelven todos los pasos del trabajo denominado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-information-about-a-specific-job-step"></a>b. Devolver información acerca de un paso de trabajo específico  
 En el ejemplo siguiente se devuelve información acerca del primer paso del trabajo denominado `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
