---
title: Sys.conversation_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- conversation_endpoints_TSQL
- conversation_endpoints
- sys.conversation_endpoints
- sys.conversation_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.conversation_endpoints catalog view
ms.assetid: 2ed758bc-2a9d-4831-8da2-4b80e218f3ea
author: stevestein
ms.author: sstein
ms.openlocfilehash: 16d29272e4229ac93b3dd5b1eaf5502a07fb0a2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109542"
---
# <a name="sysconversationendpoints-transact-sql"></a>sys.conversation_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cada lado de una conversación de [!INCLUDE[ssSB](../../includes/sssb-md.md)] se representa mediante un extremo de conversación. Esta vista de catálogo contiene una fila por extremo de conversación en la base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|conversation_handle|**uniqueidentifier**|Identificador de este extremo de conversación. No acepta valores NULL.|  
|conversation_id|**uniqueidentifier**|Identificador de la conversación. Este identificador lo comparten los dos participantes en la conversación. Esto, junto a la columna is_initiator, es exclusivo en la base de datos. No acepta valores NULL.|  
|is_initiator|**tinyint**|Si este extremo es el iniciador o el destino de la conversación.  No acepta valores NULL.<br /><br /> 1 = Iniciador<br /><br /> 0 = Destino|  
|service_contract_id|**int**|Identificador del contrato de esta conversación. No acepta valores NULL.|  
|conversation_group_id|**uniqueidentifier**|Identificador del grupo de conversación al que pertenece esta conversación. No acepta valores NULL.|  
|service_id|**int**|Identificador del servicio para este lado de la conversación. No acepta valores NULL.|  
|lifetime|**datetime**|Fecha y hora de expiración de esta conversación. No acepta valores NULL.|  
|state|**char(2)**|El estado actual de la conversación. No acepta valores NULL. Una de las siguientes opciones:<br /><br /> Por lo tanto salida iniciada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procesó una instrucción BEGIN CONVERSATION para esta conversación, pero no se ha enviado todavía ningún mensaje.<br /><br /> SI entrada iniciada. Otra instancia inició una nueva conversación con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ha recibido completamente el primer mensaje. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede crear la conversación en este estado si se fragmenta el primer mensaje o si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recibe los mensajes sin orden. No obstante, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría crear la conversación en el estado CO (conversando) si la primera transmisión recibida de la conversación contiene el primer mensaje completo.<br /><br /> CO empezado una conversación. La conversación está establecida y los dos lados de la conversación pueden enviar mensajes. La mayor parte de la comunicación de un servicio típico tiene lugar cuando la conversación está en este estado.<br /><br /> DI Disconnected entrante. El lado remoto de la conversación ha emitido un END CONVERSATION. La conversación permanece en este estado hasta que el lado local de la conversación emite un END CONVERSATION. Una aplicación podría seguir recibiendo mensajes de la conversación. Puesto que el lado remoto de la conversación ha finalizado la conversación, una aplicación no puede enviar mensajes en esta conversación. Cuando una aplicación emite una instrucción END CONVERSATION, la conversación pasa al estado CD (Cerrada).<br /><br /> DO salida desconectada. El lado local de la conversación ha emitido un END CONVERSATION. La conversación permanece en este estado hasta que el lado remoto de la conversación confirma un END CONVERSATION. Una aplicación no puede seguir enviando ni recibiendo mensajes de la conversación. Cuando el lado remoto de la conversación confirma la instrucción END CONVERSATION, la conversación pasa al estado CD (Cerrada).<br /><br /> Error de recuperación de emergencia. Se ha producido un error en este extremo. El mensaje de error se coloca en la cola de la aplicación. Si la cola de la aplicación está vacía, esto indica que la aplicación ya utilizó el mensaje de error.<br /><br /> Se cerró el CD. El extremo de la conversación ya no se utiliza.|  
|state_desc|**nvarchar(60)**|Descripción del estado de la conversación de punto de conexión. Esta columna es NULLABLE. Una de las siguientes opciones:<br /><br /> **STARTED_OUTBOUND**<br /><br /> **STARTED_INBOUND**<br /><br /> **CONVERSANDO**<br /><br /> **DISCONNECTED_INBOUND**<br /><br /> **DISCONNECTED_OUTBOUND**<br /><br /> **CERRADO**<br /><br /> **ERROR**|  
|far_service|**nvarchar(256)**|Nombre del servicio en el lado remoto de la conversación. No acepta valores NULL.|  
|far_broker_instance|**nvarchar(128)**|Instancia del agente del lado remoto de la conversación. QUE ACEPTA VALORES NULL.|  
|principal_id|**int**|Identificador de la entidad de seguridad cuyo certificado se utiliza en el lado local del diálogo. No acepta valores NULL.|  
|far_principal_id|**int**|Identificador del usuario cuyo certificado se utiliza en el lado remoto del diálogo. No acepta valores NULL.|  
|outbound_session_key_identifier|**uniqueidentifier**|Identificador de la clave de cifrado de salida de este diálogo. No acepta valores NULL.|  
|inbound_session_key_identifier|**uniqueidentifier**|Identificador de la clave de cifrado de entrada de este diálogo. No acepta valores NULL.|  
|security_timestamp|**datetime**|Hora en que se creó la clave de la sesión local. No acepta valores NULL.|  
|dialog_timer|**datetime**|Hora en la que el temporizador de conversación de este diálogo envía un mensaje DialogTimer. No acepta valores NULL.|  
|send_sequence|**bigint**|Número del siguiente mensaje en la secuencia de envío. No acepta valores NULL.|  
|last_send_tran_id|**binary(6)**|Identificador de transacción interno de la última transacción para enviar un mensaje. No acepta valores NULL.|  
|end_dialog_sequence|**bigint**|Número de secuencia del mensaje End Dialog. No acepta valores NULL.|  
|receive_sequence|**bigint**|Número del mensaje siguiente que se esperaba en la secuencia de recepción de mensajes. No acepta valores NULL.|  
|receive_sequence_frag|**int**|Número de fragmento del mensaje siguiente que se esperaba en la secuencia de recepción de mensajes. No acepta valores NULL.|  
|system_sequence|**bigint**|Número de secuencia del último mensaje del sistema para este diálogo. No acepta valores NULL.|  
|first_out_of_order_sequence|**bigint**|Número de secuencia del primer mensaje de los mensajes fuera de secuencia de este diálogo. No acepta valores NULL.|  
|last_out_of_order_sequence|**bigint**|Número de secuencia del último mensaje de los mensajes fuera de secuencia de este diálogo. No acepta valores NULL.|  
|last_out_of_order_frag|**int**|Número de secuencia del último mensaje de los fragmentos no ordenados de este diálogo. No acepta valores NULL.|  
|is_system|**bit**|1 si es un diálogo del sistema. No acepta valores NULL.|  
|prioridad|**tinyint**|La prioridad de conversación que se ha asignado a este extremo de conversación. No acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
