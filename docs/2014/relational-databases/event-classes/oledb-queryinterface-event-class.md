---
title: OLEDB QueryInterface, clase de eventos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- OLEDB QueryInterface event class
ms.assetid: f54c9ef9-3add-497c-a09b-42c4ce3c623d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b420e0b4b9c9531209f3d3227f534116e26dd206
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63032427"
---
# <a name="oledb-queryinterface-event-class"></a>OLEDB QueryInterface, clase de eventos
  La clase de evento **OLEDB QueryInterface** se produce cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emite una llamada **QueryInterface** de OLE DB para consultas distribuidas y procedimientos almacenados remotos. Incluya esta clase de evento en los seguimientos que supervisan problemas asociados a consultas distribuidas y procedimientos almacenados remotos.  
  
 Al incluir la clase de evento **OLEDB QueryInterface** , habrá una gran sobrecarga. Si estos eventos se producen frecuentemente, el seguimiento puede reducir mucho el rendimiento. Para minimizar la sobrecarga, limite el uso de esta clase de evento a los seguimientos que supervisen problemas específicos durante periodos breves.  
  
## <a name="oledb-queryinterface-event-class-data-columns"></a>Columnas de datos de la clase de evento OLEDB QueryInterface  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Sí|  
|DatabaseID|`int`|Identificador de la base de datos especificada mediante la instrucción USE *database* o la base de datos predeterminada si no se emite la instrucción USE *database* para una determinada instancia. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos **ServerName** en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|Duration|`bigint`|Tiempo necesario para completar el evento QueryInterface de OLE DB.|13|No|  
|EndTime|`datetime`|Hora a la que finalizó el evento.|15|Sí|  
|Error|`int`|Número de error de un evento dado. Con frecuencia, es el número de error almacenado en la vista de catálogo **sys.messages** .|31|Sí|  
|EventClass|`int`|Tipo de evento = 120.|27|Sin |  
|EventSequence|`int`|Secuencia de la clase de evento OLE DB en el lote.|51|No|  
|EventSubClass|`int`|0=Inicio<br /><br /> 1=Completado|21|No|  
|GroupID|`int`|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sí|  
|LinkedServerName|`nvarchar`|Nombre del servidor vinculado.|45|Sí|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|MethodName|`nvarchar`|Nombre del método de llamada.|47|Sin |  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Sí|  
|ProviderName|`nvarchar`|Nombre del proveedor OLE DB.|46|Sí|  
|IdSolicitud|`int`|Identificador de la solicitud que contiene la instrucción.|49|Sí|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, `SessionLoginName` muestra inicioDeSesión1 y `LoginName` muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TextData|`nvarchar`|Parámetros enviados y recibidos en la llamada OLE DB.|1|Sin |  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Objetos de automatización OLE en Transact-SQL](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
