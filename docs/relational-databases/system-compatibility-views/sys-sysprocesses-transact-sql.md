---
title: Sys.sysprocesses (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysprocesses_TSQL
- sys.sysprocesses_TSQL
- sys.sysprocesses
- sysprocesses
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysprocesses compatibility view
- sysprocesses system table
ms.assetid: 60a36d36-54b3-4bd6-9cac-702205a21b16
author: rothja
ms.author: jroth
ms.openlocfilehash: 60f4cf3945ed026a311e8e8dc0ab37f95ec8aabb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986496"
---
# <a name="syssysprocesses-transact-sql"></a>sys.sysprocesses (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información sobre los procesos que se ejecutan en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estos procesos pueden ser procesos del cliente o procesos del sistema. Para obtener acceso a sysprocesses, debe estar en el contexto de la base de datos maestra o utilizar el nombre de tres partes master.dbo.sysprocesses.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|spid|**smallint**|Identificador de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|kpid|**smallint**|Identificador de subproceso de Windows.|  
|blocked|**smallint**|Id. de la sesión que bloquea la solicitud. Si esta columna es NULL, la solicitud no está bloqueada o la información de la sesión de bloqueo no está disponible (o no puede ser identificada).<br /><br /> -2 = El recurso de bloqueo es propiedad de una transacción distribuida huérfana.<br /><br /> -3 = El recurso de bloqueo es propiedad de una transacción de recuperación diferida.<br /><br /> -4 = No se pudo determinar el Id. de sesión del propietario del bloqueo temporal a causa de transiciones internas de estado del bloqueo temporal.|  
|waittype|**binary(2)**|Reservado.|  
|waittime|**bigint**|Tiempo de espera actual (en milisegundos).<br /><br /> 0 = El proceso no está en espera.|  
|lastwaittype|**nchar(32)**|Cadena que indica el nombre del último tipo de espera, o del actual.|  
|waitresource|**nchar(256)**|Representación textual de un recurso de bloqueo.|  
|dbid|**smallint**|Identificador de la base de datos que el proceso utiliza actualmente.|  
|uid|**smallint**|Identificador del usuario que ha ejecutado el comando. Produce un desbordamiento o devuelve NULL si el número de usuarios y roles es superior a 32.767.|  
|cpu|**int**|Tiempo de CPU acumulado para el proceso. La entrada se actualiza para todos los procesos, independientemente de si la opción SET STATISTICS TIME está establecida en ON o en OFF.|  
|physical_io|**bigint**|Número de lecturas y escrituras en disco acumuladas para el proceso.|  
|memusage|**int**|Número de páginas de la memoria caché de procedimientos que están asignadas actualmente al proceso. Un número negativo indica que el proceso está liberando memoria asignada por otro proceso.|  
|login_time|**datetime**|Hora a la que un proceso de cliente inició una sesión en el servidor.|  
|last_batch|**datetime**|Hora a la que un proceso de cliente ejecutó por última vez una llamada a un procedimiento almacenado remoto o una instrucción EXECUTE.|  
|ecid|**smallint**|Identificador de contexto de ejecución usado para identificar de forma única los subprocesos que operan en nombre de un único proceso.|  
|open_tran|**smallint**|Número de transacciones abiertas para el proceso.|  
|status|**nchar(30)**|Estado del identificador de proceso. Los valores posibles son:<br /><br /> **latente**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está restableciendo la sesión.<br /><br /> **ejecutando** = la sesión se está ejecutando uno o varios lotes. Si Conjuntos de resultados activos múltiples (MARS) está habilitado, una sesión puede ejecutar varios lotes. Para obtener más información, vea [Usar conjuntos de resultados activos múltiples &#40;MARS&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).<br /><br /> **en segundo plano** = la sesión está ejecutando una tarea en segundo plano, como la detección de interbloqueo.<br /><br /> **reversión** = la sesión está realizando una reversión de transacción.<br /><br /> **pendiente** = la sesión está esperando un subproceso de trabajo esté disponible.<br /><br /> **puede ejecutar** = la tarea en la sesión está en la cola de ejecutables de un programador mientras espera obtener un cuanto de tiempo.<br /><br /> **spinloop** = la tarea en la sesión está esperando un subproceso se libere.<br /><br /> **suspende** = la sesión está esperando un evento, como E/S, en completarse.|  
|sid|**binary(86)**|Identificador único global (GUID) del usuario.|  
|hostname|**nchar(128)**|Nombre de la estación de trabajo.|  
|program_name|**nchar(128)**|Nombre del programa de aplicación.|  
|hostprocess|**nchar(10)**|Número de identificación de proceso de la estación de trabajo.|  
|cmd|**nchar(16)**|Comando que se está ejecutando actualmente.|  
|nt_domain|**nchar(128)**|Dominio de Windows para el cliente, si se utiliza la autenticación de Windows o una conexión de confianza.|  
|nt_username|**nchar(128)**|Nombre de usuario de Windows del proceso, si se utiliza la autenticación de Windows una conexión de confianza.|  
|net_address|**nchar(12)**|Identificador único asignado al adaptador de red de la estación de trabajo de cada usuario. Cuando un usuario inicia una sesión, este identificador se inserta en la columna net_address.|  
|net_library|**nchar(12)**|Columna en la que se almacena la biblioteca de red del cliente. Cada proceso de cliente proviene de una conexión de red. Conexiones de red tienen una biblioteca de red asociada a ellos que les permite tomar la conexión.|  
|loginame|**nchar(128)**|Nombre de inicio de sesión.|  
|context_info|**binary(128)**|Datos almacenados en un lote con la instrucción SET CONTEXT_INFO.|  
|sql_handle|**binary(20)**|Representa el objeto o archivo por lotes en ejecución.<br /><br /> **Tenga en cuenta** este valor se deriva de la dirección de memoria o por lotes del objeto. No se calcula mediante el algoritmo hash de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|stmt_start|**int**|Desplazamiento inicial de la instrucción SQL actual para el identificador sql_handle especificado.|  
|stmt_end|**int**|Desplazamiento final de la instrucción SQL actual para el identificador sql_handle especificado.<br /><br /> -1 = La instrucción actual se ejecuta al final de los resultados devueltos por la función fn_get_sql para el identificador sql_handle especificado.|  
|request_id|**int**|Id. de solicitud. Se utiliza para identificar solicitudes que se ejecutan en una sesión específica.|
|page_resource |**binary (8)** |**Se aplica a**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br /><br /> Una representación hexadecimal de 8 bytes del recurso de página si la `waitresource` columna contiene una página. |  
  
## <a name="remarks"></a>Comentarios  
 Si un usuario tiene el permiso VIEW SERVER STATE en el servidor, verá todas las sesiones en ejecución de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; de lo contrario, el usuario solo verá la sesión actual.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica y funciones relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
