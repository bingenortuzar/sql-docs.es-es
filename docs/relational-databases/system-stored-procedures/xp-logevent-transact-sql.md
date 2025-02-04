---
title: xp_logevent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_logevent
- xp_logevent_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logevent
ms.assetid: 7b379ad0-5b12-4d2e-9c52-62465df1fdbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 77275ee539a6367d7e2e04d03354155a5eff721d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116640"
---
# <a name="xplogevent-transact-sql"></a>xp_logevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra un mensaje definido por el usuario en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] archivo de registro y en el Visor de eventos de Windows. xp_logevent se puede usar para enviar una alerta sin enviar un mensaje al cliente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
xp_logevent { error_number , 'message' } [ , 'severity' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *error_number*  
 Es un número de error definido por el usuario mayor que 50.000. El valor máximo es 2147483647 (2^31 - 1).  
  
 **'** *mensaje* **'**  
 Es una cadena con un máximo de 2048 caracteres.  
  
 **'** *gravedad* **'**  
 Es uno de tres cadenas de caracteres: INFORMATIVO, advertencia o ERROR. *gravedad* es opcional y su valor predeterminado es INFORMATIONAL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 xp_logevent devuelve el siguiente mensaje de error para el ejemplo de código incluido:  
  
 `The command(s) completed successfully.`  
  
## <a name="remarks"></a>Comentarios  
 Al enviar mensajes desde [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos, desencadenadores, lotes y así sucesivamente, utilizan la instrucción RAISERROR en lugar de xp_logevent. xp_logevent no invoca un controlador de mensaje de un cliente ni establece@ERROR. Para escribir mensajes en el Visor de eventos de Windows y en el archivo del registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dentro de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ejecute la instrucción RAISERROR.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol fijo de servidor db_owner o al rol fijo de base de datos maestra o al rol fijo de servidor sysadmin.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se registra el mensaje (con las variables pasadas al mensaje) en el Visor de eventos de Windows.  
  
```  
DECLARE @@TABNAME varchar(30), @@USERNAME varchar(30), @@MESSAGE varchar(255);  
SET @@TABNAME = 'customers';  
SET @@USERNAME = USER_NAME();  
SELECT @@MESSAGE = 'The table ' + @@TABNAME + ' is not owned by the user   
   ' + @@USERNAME + '.';  
  
USE master;  
EXEC xp_logevent 60000, @@MESSAGE, informational;  
```  
  
## <a name="see-also"></a>Vea también  
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados extendidos generales &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
