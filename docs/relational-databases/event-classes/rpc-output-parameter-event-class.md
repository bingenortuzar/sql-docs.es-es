---
title: RPC Output Parameter (clase de eventos) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- RPC Output Parameter event class
ms.assetid: 8c830d11-7e88-4c3e-98e9-ba72c8c99b02
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b74cbe8ec74d0ea097693b38b05c87006baf07d7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908332"
---
# <a name="rpc-output-parameter-event-class"></a>RPC Output Parameter [clase de eventos]
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La clase de eventos RPC Output Parameter realiza el seguimiento de los valores de los parámetros de salida de las llamadas a procedimiento remoto (RPC) después de su ejecución.  
  
 Utilice esta clase para examinar los valores de salida devueltos por procedimientos almacenados. Por ejemplo, si una aplicación no produce los valores de salida esperados después de ejecutar una llamada a procedimiento remoto, puede usar esta clase de evento para ayudar a aislar el problema entre el código del cliente y el código del servidor.  
  
## <a name="rpc-output-parameter-event-class-data-columns"></a>Columnas de datos de la clase de evento RPC Output Parameter  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|ClientProcessID|**int**|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Sí|  
|DatabaseID|**int**|Identificador de la base de datos especificada mediante la instrucción USE *database* o la base de datos predeterminada si no se emite la instrucción USE *database* para una determinada instancia. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DatabaseName|**nvarchar**|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|EventClass|**int**|Tipo de evento = 100.|27|No|  
|EventSequence|**int**|Secuencia de un evento determinado de la solicitud.|51|No|  
|GroupID|**int**|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
|HostName|**nvarchar**|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IsSystem|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|LoginName|**nvarchar**|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|LoginSid|**imagen**|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NTDomainName|**nvarchar**|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|**nvarchar**|Nombre del usuario de Windows.|6|Sí|  
|ObjectName|**nvarchar**|Nombre del parámetro al que se hace referencia.|34|Sí|  
|IdSolicitud|**int**|Id. de la solicitud que contiene la instrucción.|49|Sí|  
|ServerName|**nvarchar**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|SessionLoginName|**nvarchar**|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|**int**|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|**datetime**|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TextData|**ntext**|Valores del parámetro de salida de RPC.|1|Sí|  
|TransactionID|**bigint**|Id. de la transacción asignado por el sistema.|4|Sí|  
|XactSequence|**bigint**|Token que describe la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
