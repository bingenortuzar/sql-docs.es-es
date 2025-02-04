---
title: SUSER_SID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_SID
- SUSER_SID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], users
- SIDs [SQL Server]
- security identifiers [SQL Server]
- users [SQL Server], logins
- 15401 (Database Engine error)
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- SUSER_SID function
ms.assetid: 57b42a74-94e1-4326-85f1-701b9de53c7d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6eed882fffc8d6752d4884f006450efc5b9257be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117598"
---
# <a name="susersid-transact-sql"></a>SUSER_SID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el número de identificación de seguridad (SID) que corresponde al nombre de inicio de sesión especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SUSER_SID ( [ 'login' ] [ , Param2 ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *login* **'**  
**Se aplica a**: de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Nombre de inicio de sesión del usuario. *login* es **sysname**. *login*, que es opcional, puede ser un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un usuario o un grupo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Si no se especifica *login*, se devuelve información sobre el contexto de seguridad actual. Si el parámetro contiene la palabra NULL, se devolverá NULL.  
  
 *Param2*  
**Se aplica a**: de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica si se valida el nombre de inicio de sesión. *Param2* es de tipo **int** y es opcional. Cuando *Param2* es 0, no se valida el nombre de inicio de sesión. Cuando *Param2* no se especifica como 0, se comprueba el nombre de inicio de sesión de Windows para ver si coincide exactamente con el nombre de inicio de sesión almacenado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-types"></a>Tipos devueltos  
 **varbinary(85)**  
  
## <a name="remarks"></a>Notas  
 SUSER_SID puede utilizarse como una restricción DEFAULT en ALTER TABLE o CREATE TABLE. Se puede utilizar SUSER_SID en una lista de selección, en una cláusula WHERE y en cualquier lugar en el que se permita una expresión. SUSER_SID siempre debe ir seguido de paréntesis, aunque no se especifique ningún parámetro.  
  
 Cuando se llama sin ningún argumento, SUSER_SID devuelve el SID del contexto de seguridad actual. Cuando se llama sin ningún argumento en un lote que ha cambiado de contexto mediante EXECUTE AS, SUSER_SID devuelve el SID del contexto suplantado. Si se llama desde un contexto suplantado, SUSER_SID(ORIGINAL_LOGIN()) devuelve el SID del contexto original.  
  
 Cuando la intercalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la intercalación de Windows son diferentes, SUSER_SID puede producir un error cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Windows almacenan el inicio de sesión en un formato diferente. Por ejemplo, si el equipo con Windows TestComputer tiene el inicio de sesión User y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacena el inicio de sesión como TESTCOMPUTER\User, la búsqueda del inicio de sesión TestComputer\User puede que no resuelva el nombre de inicio de sesión correctamente. Para omitir esta validación del nombre de inicio de sesión, use *Param2*. Las distintas intercalaciones a menudo son una causa del error 15401 de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 `Windows NT user or group '%s' not found. Check the name again.`  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-susersid"></a>A. Usar SUSER_SID  
 En el ejemplo siguiente se devuelve el número de identificación de seguridad (SID) del contexto de seguridad actual.  
  
```  
SELECT SUSER_SID();  
```  
  
### <a name="b-using-susersid-with-a-specific-login"></a>B. Utilizar SUSER_SID con un inicio de sesión específico  
 En el ejemplo siguiente se devuelve el número de identificación de seguridad del inicio de sesión `sa` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Se aplica a**: de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SID('sa');  
GO  
```  
  
### <a name="c-using-susersid-with-a-windows-user-name"></a>C. Usar SUSER_SID con un nombre de usuario de Windows  
 En el ejemplo siguiente se devuelve el número de identificación de seguridad del usuario de Windows `London\Workstation1`.  
  
**Se aplica a**: de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SID('London\Workstation1');  
GO  
```  
  
### <a name="d-using-susersid-as-a-default-constraint"></a>D. Usar SUSER_SID como una restricción DEFAULT  
 En el ejemplo siguiente se utiliza `SUSER_SID` como restricción `DEFAULT` en una instrucción `CREATE TABLE`.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sid_example  
(  
login_sid   varbinary(85) DEFAULT SUSER_SID(),  
login_name  varchar(30) DEFAULT SYSTEM_USER,  
login_dept  varchar(10) DEFAULT 'SALES',  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sid_example DEFAULT VALUES;  
GO  
```  
  
### <a name="e-comparing-the-windows-login-name-to-the-login-name-stored-in-sql-server"></a>E. Comparar el nombre de inicio de sesión de Windows con el nombre de inicio de sesión almacenado en SQL Server  
 En el ejemplo siguiente se muestra cómo se usa *Param2* para obtener el SID de Windows y se utiliza ese SID como entrada para la función `SUSER_SNAME`. En el ejemplo se proporciona el inicio de sesión en el formato en que se almacena en Windows (`TestComputer\User`) y se devuelve en el formato en que se almacena en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (`TESTCOMPUTER\User`.  
  
**Se aplica a**: de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME(SUSER_SID('TestComputer\User', 0));  
```  
  
## <a name="see-also"></a>Consulte también  
 [ORIGINAL_LOGIN &#40;Transact-SQL&#41;](../../t-sql/functions/original-login-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [binary y varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)   
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
