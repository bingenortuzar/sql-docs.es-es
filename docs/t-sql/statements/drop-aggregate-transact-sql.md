---
title: DROP AGGREGATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_AGGREGATE_TSQL
- DROP AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- aggregate functions [SQL Server], removing
- removing user-defined functions
- dropping user-defined functions
- user-defined functions [CLR integration]
- deleting user-defined functions
- DROP AGGREGATE statement
ms.assetid: 84ffc4e7-c451-4f1f-9a67-7fc3a120e53f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 356d08eaeeb470500ccf39c86872806cf2a9be9e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984316"
---
# <a name="drop-aggregate-transact-sql"></a>DROP AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una función de agregado definida por el usuario de la base de datos actual. Las funciones de agregado definidas por el usuario se crean con [CREATE AGGREGATE](../../t-sql/statements/create-aggregate-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DROP AGGREGATE [ IF EXISTS ] [ schema_name . ] aggregate_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTS*  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta la [versión actual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Quita condicionalmente el agregado solo si ya existe.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece la función de agregado definida por el usuario.  
  
 *aggregate_name*  
 Es el nombre de la función de agregado definida por el usuario que se desea quitar.  
  
## <a name="remarks"></a>Notas  
 DROP AGGREGATE no se ejecuta si hay vistas, funciones o procedimientos almacenados creados con enlaces de esquema que hacen referencia a la función de agregado definida por el usuario que se desea quitar.  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar DROP AGGREGATE, el usuario debe tener, como mínimo, el permiso ALTER para el esquema al que pertenece el agregado definido por el usuario o el permiso CONTROL para el agregado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el agregado `Concatenate`.  
  
```  
DROP AGGREGATE dbo.Concatenate;  
```  
  
## <a name="see-also"></a>Consulte también  
 [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [Crear funciones de agregado definidas por el usuario](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)  
  
  
