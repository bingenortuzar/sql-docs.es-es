---
title: ALTER ASYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.date: 04/12/2017
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_ASYMMETRIC_KEY_TSQL
- ALTER ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTION BY PASSWORD option
- passwords [SQL Server], asymmetric keys
- encryption [SQL Server], asymmetric keys
- DECRYPTION BY PASSWORD option
- ALTER ASYMMETRIC KEY statement
- asymmetric keys [SQL Server], modifying
ms.assetid: 958e95d6-fbe6-43e8-abbd-ccedbac2dbac
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 06263499babe005bca36a982bc863dfa24356b5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066073"
---
# <a name="alter-asymmetric-key-transact-sql"></a>ALTER ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cambia las propiedades de una clave asimétrica.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER ASYMMETRIC KEY Asym_Key_Name <alter_option>  
  
<alter_option> ::=  
      <password_change_option>   
    | REMOVE PRIVATE KEY   

<password_change_option> ::=  
    WITH PRIVATE KEY ( <password_option> [ , <password_option> ] )  

<password_option> ::=  
      ENCRYPTION BY PASSWORD = 'strongPassword'  
    | DECRYPTION BY PASSWORD = 'oldPassword'  
```  
  
## <a name="arguments"></a>Argumentos  
 *Asym_Key_Name*  
 Es el nombre por el que se conoce la clave asimétrica en la base de datos.  
  
 REMOVE PRIVATE KEY  
 Quita la clave privada de la clave asimétrica. No se quita la clave pública.  
  
 WITH PRIVATE KEY  
 Cambia la protección de la clave privada.  
  
 ENCRYPTION BY PASSWORD **="***contraseñaSegura***"**  
 Especifica una nueva contraseña para proteger la clave privada. *password* debe cumplir los requisitos de la directiva de contraseñas de Windows del equipo que ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si se omite esta opción, la clave privada se cifrará con la clave maestra de la base de datos.  
  
 DECRYPTION BY PASSWORD **='***oldPassword***'**  
 Especifica la antigua contraseña con la que está protegida la clave privada. No es necesario si la clave privada está cifrada con la clave maestra de la base de datos.  
  
## <a name="remarks"></a>Notas  
 Si no hay una clave maestra de base de datos, es necesaria la opción ENCRYPTION BY PASSWORD y la operación registrará errores si no se proporciona una contraseña. Para más información sobre cómo crear una clave maestra de base de datos, vea [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md).  
  
 Puede utilizar ALTER ASYMMETRIC KEY para cambiar la protección de la clave privada si especifica las opciones de PRIVATE KEY como se muestra en la siguiente tabla.  
  
|Cambiar protección de|ENCRYPTION BY PASSWORD|DECRYPTION BY PASSWORD|  
|----------------------------|----------------------------|----------------------------|  
|Antigua contraseña a nueva contraseña|Obligatorio|Obligatorio|  
|Contraseña a clave maestra|Omitir|Obligatorio|  
|Clave maestra a contraseña|Obligatorio|Omitir|  
  
 Es necesario abrir la clave maestra de la base de datos antes de utilizarla para proteger una clave privada. Para más información, vea [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md).  
  
 Para cambiar la propiedad de una clave asimétrica, use [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL en la clave asimétrica si se quita la clave privada.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-password-of-the-private-key"></a>A. Cambiar la contraseña de la clave privada  
 En el siguiente ejemplo se cambia la contraseña utilizada para proteger la clave privada de la clave asimétrica `PacificSales09`. La nueva contraseña será `<enterStrongPasswordHere>`.  
  
```  
ALTER ASYMMETRIC KEY PacificSales09   
    WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<oldPassword>',  
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>');  
GO  
```  
  
### <a name="b-removing-the-private-key-from-an-asymmetric-key"></a>B. Quitar la clave privada de una clave asimétrica  
 En el siguiente ejemplo se quita la clave privada de `PacificSales19` y se mantiene solamente la clave pública.  
  
```  
ALTER ASYMMETRIC KEY PacificSales19 REMOVE PRIVATE KEY;  
GO  
```  
  
### <a name="c-removing-password-protection-from-a-private-key"></a>C. Quitar la protección mediante contraseña de una clave privada  
 En el siguiente ejemplo se quita la protección mediante contraseña de una clave privada y se protege con la clave maestra de la base de datos.  
  
```  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<database master key password>';  
ALTER ASYMMETRIC KEY PacificSales09 WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<enterStrongPasswordHere>' );  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [SQL Server y claves de cifrado de base de datos &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
