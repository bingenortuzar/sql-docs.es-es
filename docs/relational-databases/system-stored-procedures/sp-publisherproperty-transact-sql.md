---
title: sp_publisherproperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publisherproperty
- sp_publisherproperty_TSQL
helpviewer_keywords:
- sp_publisherproperty
ms.assetid: 0ed1ebc1-a1bd-4aed-9f46-615c5cf07827
author: stevestein
ms.author: sstein
ms.openlocfilehash: 185ad0ad33419b20fffae9bff3e5562761ea7b31
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771173"
---
# <a name="sppublisherproperty-transact-sql"></a>sp_publisherproperty (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Muestra o cambia las propiedades del publicador [!INCLUDE[msCoName](../../includes/msconame-md.md)] para los publicadores que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este procedimiento almacenado se ejecuta en el distribuidor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_publisherproperty [ @publisher = ] 'publisher'   
   [ , [ @propertyname = ] 'propertyname' ]   
   [ , [ @propertyvalue = ] 'propertyvalue' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publicador***'**  
 Es el nombre del publicador heterogéneo. *Publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
 [ **@propertyname** =] **'***PropertyName***'**  
 Es el nombre de la propiedad que se va a establecer. *PropertyName* es de **tipo sysname**y puede tener uno de los valores siguientes.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**xactsetbatching**|Si las transacciones en el publicador están agrupadas en conjuntos transaccionalmente coherentes para el procesamiento subsiguiente, denominado Xactsets. Un valor de **habilitado** significa que Xactsets se puede crear, que es el valor predeterminado. Un valor de Disabled significa que los Xactsets existentes se procesan sin que se creen nuevos Xactsets.|  
|**xactsetjob**|Si el trabajo Xactset está habilitado para la creación de Xactsets. Un valor de **habilitado** significa que el trabajo Xactset se ejecuta periódicamente para crear Xactsets en el publicador. Un valor de deshabilitado significa que los Xactsets solo los crea el agente de registro del log cuando sondea el publicador en busca de cambios.|  
|**xactsetjobinterval**|Intervalo entre ejecuciones del trabajo Xactset, en minutos.|  
  
 Cuando *PropertyName* se omite, se devuelven todas las propiedades que se pueden establecer.  
  
 [ **@propertyvalue** =] **'***PropertyValue***'**  
 Es el nuevo valor de la propiedad especificada. *PropertyValue* es de **tipo sysname y su**valor predeterminado es NULL. Cuando se omite *PropertyValue* , se devuelve la configuración actual de la propiedad.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**propertyname**|**sysname**|Devuelve las siguientes propiedades de publicación que se pueden establecer:<br /><br /> **xactsetbatching**<br /><br /> **xactsetjob**<br /><br /> **xactsetjobinterval**|  
|**PropertyValue**|**sysname**|Es el valor actual de la propiedad en la columna **PropertyName** .|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_publisherproperty** se utiliza en la replicación transaccional para publicadores que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no son de.  
  
 Cuando solo se especifica Publisher, el conjunto de resultados incluye la configuración actual de todas las propiedades que se pueden establecer.  
  
 Cuando se especifica *PropertyName* , solo aparece la propiedad con nombre en el conjunto de resultados.  
  
 Cuando se especifican todos los parámetros, la propiedad se cambia y no se devuelve un conjunto de resultados.  
  
 Al cambiar la propiedad **xactsetjobinterval** de un trabajo en ejecución, debe reiniciar el trabajo para que el nuevo intervalo surta efecto.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** en el distribuidor pueden ejecutar **sp_publisherproperty**.  
  
## <a name="see-also"></a>Vea también  
 [Configuración del trabajo del conjunto de transacciones para un publicador de Oracle&#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
