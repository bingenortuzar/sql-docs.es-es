---
title: Clase de eventos Broker:Forwarded Message Dropped | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Forwarded Message Dropped event class
ms.assetid: ec242d0b-77b0-45f5-8b12-186a14b173a8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf6e9bb278417d69be0ec0a99cb1c47d88ffddff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62664031"
---
# <a name="brokerforwarded-message-dropped-event-class"></a>Broker:Forwarded Message Dropped, clase de eventos
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un evento Broker:Forwarded Message Dropped cuando Service Broker quita un mensaje que estaba destinado a reenviarse.  
  
## <a name="brokerforwarded-message-dropped-event-class-data-columns"></a>Columnas de datos de la clase de eventos Broker:Forwarded Message Dropped  
  
|Columna de datos|Tipo|Descripción|Número de columna|Filtrable|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|BigintData1|`bigint`|Número de secuencia de mensajes.|52|Sin|  
|ClientProcessID|`int`|Id. que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Sí|  
|DatabaseID|`int`|Identificador de la base de datos especificada mediante la instrucción USE *database* o identificador de la base de datos predeterminada si no se ha emitido la instrucción USE *database*para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos Server Name en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en que se ejecuta la instrucción del usuario.|35|Sí|  
|DBUserName|`nvarchar`|Identificador de la instancia del agente de donde procede este mensaje.|40|No|  
|Error|`int`|Número de identificación del mensaje en sys.messages para el texto del evento.|31|Sin|  
|EventClass|`int`|Tipo de clase de eventos capturado. Es siempre 191 para Broker:Forwarded Message Dropped.|27|Sin|  
|EventSequence|`int`|Número de secuencia de este evento.|51|Sin|  
|FileName|`nvarchar`|Nombre del servicio al que se destina el mensaje.|36|Sin|  
|GUID|`uniqueidentifier`|Id. de conversación del diálogo. Este identificador se transmite como parte del mensaje y lo comparten ambas partes de la conversación.|54|Sin|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IndexID|`int`|Número de saltos que quedan para el mensaje reenviado.|24|Sin|  
|IntegerData|`int`|Número de fragmento del mensaje reenviado.|25|No|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|`nvarchar`|Nombre del usuario al que pertenece la conexión que generó este evento.|6|Sí|  
|ObjectId|`int`|Tiempo de vida del mensaje reenviado.|22|No|  
|ObjectName|`nvarchar`|Identificador del mensaje reenviado.|34|No|  
|OwnerName|`nvarchar`|Identificador de la instancia del agente del destino del mensaje.|37|Sin|  
|RoleName|`nvarchar`|Rol del identificador de conversación. Una de las siguientes opciones:<br /><br /> Initiator. Este agente inició la conversación.<br /><br /> Target. Este agente es el destino de la conversación.|38|Sin|  
|ServerName|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|Severity|`int`|Número de nivel de gravedad para el texto del evento.|29|No|  
|SPID|`int`|Identificador de proceso del servidor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna al proceso asociado al cliente.|12|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|State|`int`|Indica la ubicación en el código fuente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que produjo el evento. Cada lugar en el que se puede producir este evento tiene un código de estado diferente. Un ingeniero de soporte técnico de Microsoft puede utilizar este código de estado para buscar el lugar en que se produjo el evento.|30|No|  
|Correcto|`int`|Tiempo de duración del mensaje. Cuando este valor es mayor o igual que el tiempo de vida, el mensaje se quita.|23|No|  
|TargetLoginName|`nvarchar`|Dirección de red a la que se habría reenviado el mensaje.|42|No|  
|TargetUserName|`nvarchar`|Nombre del servicio que ha iniciado el mensaje.|39|Sin|  
|TextData|`ntext`|Descripción del motivo por el que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quitó el mensaje.|1|Sí|  
|Transaction ID|`bigint`|Identificador de la transacción asignado por el sistema.|4|No|  
  
 La columna TextData de este evento contiene una descripción del motivo por el que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quitó el mensaje.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
