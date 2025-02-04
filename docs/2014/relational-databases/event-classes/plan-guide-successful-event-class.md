---
title: Clase de evento Guía de plan correcta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Plan Guide Successful event class
ms.assetid: fecfbb6c-56c9-4db4-84d3-00d6e338355a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 56157ce2c29a95d35198ab44835b50e45d7831a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827208"
---
# <a name="plan-guide-successful-event-class"></a>Clase de evento Guía de plan correcta
  La clase de eventos Guía de plan correcta indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pudo generar correctamente un plan de ejecución para una consulta o lote que contenía una guía de plan. El evento se disparará cuando se cumplan las siguientes condiciones:  
  
-   El lote o módulo de la definición de la guía de plan coincide con el lote o módulo que se está ejecutando.  
  
-   La consulta de la definición de la guía de plan coincide con la consulta que se está ejecutando.  
  
-   Las sugerencias en la definición de la guía de plan, incluyendo la sugerencia USE PLAN, se aplicaron correctamente a la consulta. Es decir, el plan de consulta compilado cumplió con las sugerencias especificadas.  
  
## <a name="plan-guide-successful-event-class-data-columns"></a>Columnas de datos de la clase de eventos Guía de plan correcta  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra del programa.|10|Sí|  
|ClientProcessID|`int`|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Sí|  
|DatabaseID|`int`|Identificador de la base de datos especificada mediante la instrucción USE *database* o la base de datos predeterminada si no se emite la instrucción USE *database* para una determinada instancia. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos ServerName en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DatabaseName|`nvarchar`|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|EventClass|`int`|Tipo de evento = 214.|27|No|  
|EventSequence|`int`|Secuencia de un evento determinado de la solicitud.|51|No|  
|HostName|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IsSystem|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario: 1 = sistema, 0 = usuario.|60|Sí|  
|LoginName|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\\*nombreDeUsuario*).|11|Sí|  
|LoginSid|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Encontrará esta información en la vista [sys.server_principals](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql) o en las vistas de catálogo [sys.sql_logins](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql) . Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NTDomainName|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|`nvarchar`|Nombre del usuario de Windows.|6|Sí|  
|ObjectID|`int`|Id. de objeto del módulo que se estaba compilando cuando se aplicó la guía de plan. Si la guía de plan no se aplicó a un módulo, esta columna estará establecida en NULL.|22|Sí|  
|IdSolicitud|`int`|Id. de la solicitud que contiene la instrucción.|49|Sí|  
|ServerName|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuyo seguimiento se realiza.|26|Sin|  
|SessionLoginName|`nvarchar`|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|`int`|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|TextData|`ntext`|Nombre de la guía de plan.|1|Sí|  
|TransactionID|`bigint`|Id. de la transacción asignado por el sistema.|4|Sí|  
|XactSequence|`bigint`|Token que describe la transacción actual.|50|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Clase de eventos Plan Guide Unsuccessful](plan-guide-unsuccessful-event-class.md)   
 [Eventos extendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
