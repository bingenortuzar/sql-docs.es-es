---
title: sp_vupgrade_replication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
author: stevestein
ms.author: sstein
ms.openlocfilehash: f6b2c736087b2f860bf8419264904e8669ba8951
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771546"
---
# <a name="spvupgradereplication-transact-sql"></a>sp_vupgrade_replication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Se activa durante la instalación al actualizar un servidor de replicación. Actualiza los datos del esquema y del sistema de tal modo que admitan la replicación en el nivel de producto actual. Crea los nuevos objetos del sistema de replicación en las bases de datos del sistema y de usuarios. Este procedimiento almacenado se ejecuta en el equipo donde tendrá lugar la actualización de replicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_vupgrade_replication [ [@login=] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @ver_old= ] 'old_version' ]  
    [ , [ @force_remove= ] 'force_removal' ]  
    [ , [ @security_mode= ] security_mode ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @login = ] 'login'`Es el inicio de sesión del administrador del sistema que se va a usar al crear nuevos objetos del sistema en la base de datos de distribución. *login* es de tipo **sysname** y su valor predeterminado es NULL. Este parámetro no es necesario si *security_mode* está establecido en **1**, que es la autenticación de Windows.  
  
> [!NOTE]  
>  Este parámetro se omite al actualizar a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores.  
  
`[ @password = ] 'password'`Es la contraseña de administrador del sistema que se va a usar al crear nuevos objetos del sistema en la base de datos de distribución. *password* es de **tipo sysname y su**valor predeterminado es **' '** (cadena vacía). Este parámetro no es necesario si *security_mode* está establecido en **1**, que es la autenticación de Windows.  
  
> [!NOTE]  
>  Este parámetro se omite al actualizar a SQL [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores.  
  
`[ @ver_old = ] 'old_version'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 Este procedimiento almacenado ha quedado desusado y se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
`[ @force_remove = ] 'force_removal'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @security_mode = ] 'security_mode'`Es el modo de seguridad de inicio de sesión que se va a usar al crear nuevos objetos del sistema en la base de datos de distribución. *security_mode* es de **bit** con un valor predeterminado de **0**. Sies 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se usará la autenticación. Si es **1**, se utilizará la autenticación de Windows.  
  
> [!NOTE]  
>  Este parámetro se omite al actualizar a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_vupgrade_replication** se usa al actualizar todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_vupgrade_replication**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Validar datos replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
