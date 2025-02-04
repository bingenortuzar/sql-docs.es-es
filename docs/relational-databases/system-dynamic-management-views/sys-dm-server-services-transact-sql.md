---
title: sys.dm_server_services (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_services
- sys.dm_server_services
- sys.dm_server_services_TSQL
- dm_server_services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_services dynamic management view
ms.assetid: 3f0defd0-478d-4e7f-96be-8795c9de4e3f
author: stevestein
ms.author: sstein
ms.openlocfilehash: b1c44b269f68b39d633a18f366615fd41b582938
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892948"
---
# <a name="sysdm_server_services-transact-sql"></a>sys.dm_server_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre los servicios SQL Server, Texto completo y Agente SQL Server en la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use esta vista de administración dinámica para notificar información de estado sobre estos servicios.  
  
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar(256)**|Nombre del servicio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]de, de texto completo o de Agente SQL Server. No puede ser null.|  
|startup_type|**int**|Indica el modo de inicio del servicio. A continuación se muestran los valores posibles y sus descripciones correspondientes.<br /><br /> 0: Otros<br />1: Otros<br />2: Automático<br />3: Manual<br />4: Disabled<br /><br /> Acepta valores NULL.|  
|startup_type_desc|**nvarchar(256)**|Describe el modo de inicio del servicio. A continuación se muestran los valores posibles y sus descripciones correspondientes.<br /><br /> Distinta Otro (inicio de arranque)<br />Distinta Otro (inicio del sistema)<br />Automático: Inicio automático<br />Manual: Inicio de la demanda<br />Deshabilitado: Disabled<br /><br /> No puede ser null.|  
|status|**int**|Indica el estado actual del servicio. A continuación se muestran los valores posibles y sus descripciones correspondientes.<br /><br /> 1: Stopped<br />2: Otro (Inicio pendiente)<br />3: Otro (detención pendiente)<br />4: En ejecución<br />5: Otro (continuación pendiente)<br />6: Otro (pausa pendiente)<br />7: En pausa<br /><br /> Acepta valores NULL.|  
|status_desc|**nvarchar(256)**|Describe el estado actual del servicio. A continuación se muestran los valores posibles y sus descripciones correspondientes.<br /><br /> Ha El servicio está detenido.<br />Otro (operación de inicio pendiente): El servicio está en proceso de inicio.<br />Otro (operación de detención pendiente): El servicio está en proceso de detención.<br />Estén El servicio se está ejecutando.<br />Otro (continuar con las operaciones pendientes): El servicio está en un estado pendiente.<br />Otro (pausa pendiente): El servicio está en proceso de pausa.<br />En pausa El servicio está en pausa.<br /><br /> No puede ser null.|  
|process_id|**int**|Identificador de proceso del servicio. No puede ser null.|  
|last_startup_time|**datetimeoffset(7)**|Fecha y hora en que el servicio se inició por última vez. Acepta valores NULL.|  
|service_account|**nvarchar(256)**|Cuenta autorizada para controlar el servicio. Esta cuenta puede iniciar o detener el servicio, o puede modificar las propiedades del servicio. No puede ser null.|  
|filename|**nvarchar(256)**|Ruta de acceso y nombre del archivo ejecutable del servicio. No puede ser null.|  
|is_clustered|**nvarchar(1)**|Indica si el servicio está instalado como un recurso de un servidor en clúster. No puede ser null.|  
|cluster_nodename|**nvarchar(256)**|Nombre del nodo de clúster en el que está instalado el servicio. Acepta valores NULL.|
|instant_file_initialization_enabled|**nvarchar(1)**|Especifica si la inicialización instantánea de archivos está [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] habilitada para el servicio.<br /><br />Y = la inicialización instantánea de archivos está habilitada para el servicio.<br /><br />N = la inicialización instantánea de archivos está deshabilitada para el servicio.<br /><br /> Acepta valores NULL.<br /><br /> **Nota:** No se aplica a otros servicios como el Agente SQL Server.<br /><br /> **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](A partir [!INCLUDE[sssql11](../../includes/sssql11-md.md)] de SP4 y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).|  

## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere el permiso `VIEW SERVER STATE` en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_server_registry &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  
