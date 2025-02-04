---
title: sysmail_configure_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_configure_sp_TSQL
- sysmail_configure_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_configure_sp
ms.assetid: 73b33c56-2bff-446a-b495-ae198ad74db1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7984fba52f813644c9dcb25bca2beb123be85622
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017725"
---
# <a name="sysmailconfiguresp-transact-sql"></a>sysmail_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia los valores de configuración de Correo electrónico de base de datos. Los valores de configuración especificados con **sysmail_configure_sp** se aplican a toda la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_configure_sp [ [ @parameter_name = ] 'parameter_name' ]  
    [ , [ @parameter_value = ] 'parameter_value' ]  
    [ , [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@parameter_name** =] **'** _parameter_name_ **'**  
 Nombre del parámetro que se va a cambiar.  
  
 [ **@parameter_value** =] **'** _parameter_value_ **'**  
 Valor nuevo del parámetro.  
  
 [ **@description** =] **'** _descripción_ **'**  
 Descripción del parámetro.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 El Correo electrónico de base de datos utiliza los siguientes parámetros:  
  
||||  
|-|-|-|  
|Nombre de parámetro|Descripción|Valor predeterminado|  
|*AccountRetryAttempts*|Número de veces que el proceso de correo electrónico externo intenta enviar el mensaje de correo electrónico con cada cuenta del perfil especificado.|**1**|  
|*AccountRetryDelay*|Cantidad de tiempo en segundos que el proceso de correo electrónico externo espera entre cada intento de envío de un mensaje.|**5000**|  
|*DatabaseMailExeMinimumLifeTime*|Cantidad de tiempo mínima en segundos que el proceso de correo electrónico externo permanece activo. Si el Correo electrónico de base de datos está enviando muchos mensajes, aumente este valor para mantener activo el Correo electrónico de base de datos y evitar una sobrecarga de inicios y detenciones frecuentes.|**600**|  
|*DefaultAttachmentEncoding*|Codificación predeterminada para los datos adjuntos de correo electrónico.|MIME|  
|*MaxFileSize*|Tamaño máximo de los datos adjuntos en bytes.|**1000000**|  
|*ProhibitedExtensions*|Lista de extensiones separadas por comas que no se puede enviar como datos adjuntos en un mensaje de correo electrónico.|**exe, dll, vbs, js**|  
|*LoggingLevel*|Sirve para especificar qué mensajes se deben registrar en el registro de Correo electrónico de base de datos. Uno de los valores numéricos siguientes:<br /><br /> 1 - Éste es el modo normal. Solo registra los errores.<br /><br /> 2 - Éste es el modo extendido. Registra errores, advertencias y mensajes informativos.<br /><br /> 3 - Éste es el modo detallado. Registra errores, advertencias, mensajes informativos, mensajes de acciones correctas y otros mensajes internos. Utilice este modo para solucionar problemas.|**2**|  
  
 El procedimiento almacenado **sysmail_configure_sp** está en el **msdb** de base de datos y que pertenece el **dbo** esquema. El procedimiento debe ejecutarse con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución de este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 **A. Configurar el correo electrónico de base de datos para reintentar con cada cuenta 10 veces**  
  
 En el siguiente ejemplo se muestra el valor del Correo electrónico de base de datos para reintentar con cada cuenta diez veces antes de determinar que no se puede obtener acceso a la cuenta.  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'AccountRetryAttempts', '10' ;  
```  
  
 **B. Establecer el tamaño máximo de datos adjuntos en dos megabytes**  
  
 En el siguiente ejemplo se muestra cómo se establece el tamaño máximo de los datos adjuntos en 2 megabytes.  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'MaxFileSize', '2097152' ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_help_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-help-configure-sp-transact-sql.md)   
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
