---
title: Clase de eventos Broker:Conversation Group | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Conversation Group event class
ms.assetid: 6595bef6-9d40-42eb-a934-735622dd23fb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 23e39e48b8c4c20ab0e847d87b7193179e8d74ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62664238"
---
# <a name="brokerconversation-group-event-class"></a>Broker:Conversation Group, clase de eventos
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un evento **Broker:Conversation Group** cuando Service Broker crea un grupo de conversación nuevo o quita un grupo de conversación existente.  
  
## <a name="brokerconversation-group-event-class-data-columns"></a>Columnas de datos de la clase de eventos Broker:Conversation Group  
  
|Columna de datos|Tipo|Descripción|Número de columna|Filtrable|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|**ClientProcessID**|`int`|Id. que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Sí|  
|**DatabaseID**|`int`|Identificador de la base de datos especificada mediante la instrucción USE *baseDeDatos* o identificador de la base de datos predeterminada si no se emite la instrucción USE *baseDeDatos* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos **ServerName** en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|**EventClass**|`int`|Tipo de clase de eventos capturado. Es siempre **136** para **Broker:Conversation Group**.|27|Sin|  
|**EventSequence**|`int`|Número de secuencia de este evento.|51|Sin|  
|**EventSubClass**|`nvarchar`|Tipo de subclase de evento que proporciona más información acerca de cada clase de evento. Esta columna puede incluir los valores siguientes:<br /><br /> **Crear**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creó un nuevo grupo de conversación.<br /><br /> **Quitar**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eliminó un nuevo grupo de conversación.|21|Sí|  
|**GUID**|`uniqueidentifier`|Identificador del grupo de conversación que se describe en este evento.|54|Sin|  
|**HostName**|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|**IsSystem**|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sin|  
|**LoginSid**|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|**NTDomainName**|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|**NTUserName**|`nvarchar`|Nombre del usuario al que pertenece la conexión que generó este evento.|6|Sí|  
|**ServerName**|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|Sin|  
|**SPID**|`int`|Identificador de proceso del servidor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna al proceso asociado al cliente.|12|Sí|  
|**StartTime**|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|**TransactionID**|`bigint`|Identificador de la transacción asignado por el sistema.|4|Sin|  
  
  
