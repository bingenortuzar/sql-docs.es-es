---
title: Clase de eventos de carga de ensamblado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Assembly Load event class
ms.assetid: cfb0b69d-4ce0-4067-a3df-d82775e57886
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 17a2c847e906616c4555d37e641f76eeb73391ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065257"
---
# <a name="assembly-load-event-class"></a>Assembly Load (clase de eventos)
  La clase de evento **Assembly Load** se produce cuando se ejecuta una solicitud de carga de un ensamblado.  
  
 Incluya la clase de evento **Assembly Load** en seguimientos en los que desea supervisar las cargas de ensamblado. Puede resultar útil al solucionar problemas de una consulta que utilice CLR, de un servidor que se ejecute lentamente al ejecutar consultas CLR o al supervisar un servidor para recopilar información de usuarios, bases de datos, éxitos, etc. sobre las cargas de ensamblado.  
  
## <a name="assembly-load-event-class-data-columns"></a>Columnas de datos de la clase de evento Assembly Load  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nombre de la aplicación que solicitó la carga.|10|Sí|  
|**ClientProcessID**|**int**|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Sí|  
|**DatabaseID**|**int**|Identificador de la base de datos especificada mediante la instrucción USE database o la base de datos predeterminada si no se emite la instrucción USE database para una determinada instancia. [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos **ServerName** en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|**DatabaseName**|**nvarchar**|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|**EventSequence**|**int**|Secuencia de un evento determinado de la solicitud.|51|No|  
|**GroupID**|**int**|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
|**HostName**|**nvarchar**|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|**LoginName**|**nvarchar**|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|**LoginSID**|**image**|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede encontrar esta información en la vista de catálogo **sys.server_principals** . Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|**NTDomainName**|**nvarchar**|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|**NTUserName**|**nvarchar**|Nombre del usuario de Windows.|6|Sí|  
|**ObjectID**|**int**|Id. de ensamblado|22|Sí|  
|**ObjectName**|**nvarchar**|Nombre completo del ensamblado.|34|Sí|  
|**IdSolicitud**|**int**|Identificador de la solicitud que contiene la instrucción.|49|Sí|  
|**ServerName**|**nvarchar**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|Sin|  
|**SessionLoginName**|**nvarchar**|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, **SessionLoginName** muestra inicioDeSesión1 y **LoginName** muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|**SPID**|**int**|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|**StartTime**|**datetime**|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|**Correcto**|**int**|Indica si la carga de ensamblado se realizó satisfactoriamente (1) o produjo errores (0).|23|Sí|  
|**TextData**|**ntext**|"Carga de ensamblado satisfactoria" si la carga se realiza satisfactoriamente; de lo contrario, "Error en la carga de ensamblado".|1|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../relational-databases/extended-events/extended-events.md)   
 [Ensamblados &#40;motor de la base de datos&#41;](../relational-databases/clr-integration/assemblies-database-engine.md)  
  
  
