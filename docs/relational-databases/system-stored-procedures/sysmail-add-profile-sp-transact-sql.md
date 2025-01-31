---
title: sysmail_add_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
author: stevestein
ms.author: sstein
ms.openlocfilehash: a4bd7f90688d61f9ecee487d553393e38bed82e3
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211281"
---
# <a name="sysmail_add_profile_sp-transact-sql"></a>sysmail_add_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Crea un nuevo perfil de Correo electrónico de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_name = ] 'profile\_name'`Nombre del nuevo perfil. *profile_name* es de **tipo sysname**y no tiene ningún valor predeterminado.  
 
   > [!NOTE]
   > El nombre de perfil que usa Azure SQL Instancia administrada Agente SQL debe llamarse **AzureManagedInstance_dbmail_profile**
  
`[ @description = ] 'description'`Descripción opcional del nuevo perfil. la *Descripción* es de tipo **nvarchar (256)** y no tiene ningún valor predeterminado.  
  
`[ @profile_id = ] _new\_profile\_id OUTPUT`Devuelve el identificador del nuevo perfil. *new_profile_id* es de **tipo int**y su valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Un perfil de Correo electrónico de base de datos contiene cualquier número de cuentas de Correo electrónico de base de datos. Los procedimientos almacenados de Correo electrónico de base de datos pueden hacer referencia a un perfil por el nombre o por el Id. del perfil generado por este procedimiento. Para obtener más información sobre cómo agregar una cuenta a un perfil, vea [sysmail_add_profileaccount_sp &#40;Transact&#41;-SQL](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md).  
  
 El nombre y la descripción del perfil se pueden cambiar con el procedimiento almacenado **sysmail_update_profile_sp**, mientras que el ID. de perfil permanece constante para la vida del perfil.  
  
 El nombre del perfil debe ser único para el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] de Microsoft o el procedimiento almacenado devuelve un error.  
  
 El procedimiento almacenado **sysmail_add_profile_sp** está en la base de datos **msdb** y pertenece al esquema **DBO** . El procedimiento se debe ejecutar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Los permisos de ejecución para este procedimiento tienen como valor predeterminado los miembros del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 **A. Crear un nuevo perfil**  
  
 En el ejemplo siguiente se crea un nuevo perfil de Correo electrónico de base de datos denominado `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **B. Crear un nuevo perfil y guardar el identificador de perfil en una variable**  
  
 En el ejemplo siguiente se crea un nuevo perfil de Correo electrónico de base de datos denominado `AdventureWorks Administrator`. En el ejemplo se almacena el Id. del perfil en la variable `@profileId` y se devuelve un conjunto de resultados que contiene el Id. del nuevo perfil.  
  
```  
DECLARE @profileId INT ;  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.',  
       @profile_id = @profileId OUTPUT ;  
  
SELECT @profileId ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Creación de una cuenta de Correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Correo electrónico de base de datos objetos de configuración](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimientos &#40;almacenados de correo electrónico de base de datos TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
