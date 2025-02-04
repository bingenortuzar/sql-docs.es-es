---
title: BACKUP CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DUMP_CERTIFICATE_TSQL
- BACKUP CERTIFICATE
- sql13.swb.exportcertificate.f1
- DUMP CERTIFICATE
- BACKUP_CERTIFICATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], certificates
- decryption [SQL Server], certificates
- exporting certificates
- certificates [SQL Server], exporting
- BACKUP CERTIFICATE statement
- backing up certificates [SQL Server]
- decryption [SQL Server]
- cryptography [SQL Server], certificates
ms.assetid: 509b9462-819b-4c45-baae-3d2d90d14a1c
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 7b2559ca1eee0f2787fbf74adba97b03671d6faf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091764"
---
# <a name="backup-certificate-transact-sql"></a>BACKUP CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Exporta un certificado a un archivo.  
  
 ![Icono de vínculo](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server  
  
BACKUP CERTIFICATE certname TO FILE = 'path_to_file'  
    [ WITH PRIVATE KEY   
      (   
        FILE = 'path_to_private_key_file' ,  
        ENCRYPTION BY PASSWORD = 'encryption_password'   
        [ , DECRYPTION BY PASSWORD = 'decryption_password' ]   
      )   
    ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
BACKUP CERTIFICATE certname TO FILE ='path_to_file'  
      WITH PRIVATE KEY   
      (   
        FILE ='path_to_private_key_file',  
        ENCRYPTION BY PASSWORD ='encryption_password'   
      )   
```  
  
## <a name="arguments"></a>Argumentos  
 *certname*  
 Es el nombre del certificado del que se va a hacer una copia de seguridad.

 TO FILE = '*path_to_file*'  
 Especifica la ruta de acceso completa, incluido el nombre de archivo, al archivo en el que se almacenará el certificado. Esta ruta de acceso puede ser una ruta de acceso local o una ruta UNC a una ubicación de red. Si solo se especifica un nombre de archivo, el archivo se guardará en la carpeta de datos de usuario predeterminada de la instancia (que puede ser o no ser la carpeta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data). Para LocalDB de SQL Server Express, la carpeta de datos de usuario predeterminada de la instancia es la ruta de acceso especificada por la variable de entorno `%USERPROFILE%` para la cuenta que ha creado la instancia.  

 WITH PRIVATE KEY Especifica que la clave privada del certificado se tiene que guardar en un archivo. Esta cláusula es opcional.

 FILE = '*path_to_private_key_file*'  
 Especifica la ruta de acceso completa, incluido el nombre de archivo, al archivo en el que se almacenará la clave privada. Esta ruta de acceso puede ser una ruta de acceso local o una ruta UNC a una ubicación de red. Si solo se especifica un nombre de archivo, el archivo se guardará en la carpeta de datos de usuario predeterminada de la instancia (que puede ser o no ser la carpeta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data). Para LocalDB de SQL Server Express, la carpeta de datos de usuario predeterminada de la instancia es la ruta de acceso especificada por la variable de entorno `%USERPROFILE%` para la cuenta que ha creado la instancia.  

 ENCRYPTION BY PASSWORD = '*encryption_password*'  
 Es la contraseña que se utiliza para cifrar la clave privada antes de escribir la clave en el archivo de copia de seguridad. La contraseña se somete a comprobaciones de complejidad.  
  
 DECRYPTION BY PASSWORD = '*decryption_password*'  
 Es la contraseña que se utiliza para descifrar la clave privada antes de realizar una copia de seguridad de la clave. Este argumento no es necesario si el certificado está cifrado con la clave maestra. 
  
## <a name="remarks"></a>Notas  
 Si la clave privada se cifra con una contraseña en la base de datos, es necesario especificar la contraseña de descifrado.  
  
 Para realizar una copia de seguridad de la clave privada en un archivo es necesario el cifrado. La contraseña utilizada para proteger la clave privada del archivo no es la misma que la usada para cifrar la clave privada del certificado en la base de datos.  

 Las claves privadas se guardan en un formato de archivo PVK.

 Para restaurar la copia de seguridad de un certificado, con o sin clave privada, use la instrucción [CREATE CERTIFICATE](../../t-sql/statements/create-certificate-transact-sql.md).
 
 Para restaurar una clave privada en un certificado existente en la base de datos, use la instrucción [ALTER CERTIFICATE](../../t-sql/statements/alter-certificate-transact-sql.md).
 
 Al realizar una copia de seguridad, los archivos se agregan a la lista de control de acceso de la cuenta de servicio de la instancia de SQL Server. Si es necesario restaurar el certificado en un servidor que se ejecuta en otra cuenta, deberá ajustar los permisos en los archivos para que la nueva cuenta pueda leerlos. 
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL en el certificado y conocimiento de la contraseña que se utiliza para cifrar la clave privada. Si solo se hace una copia de seguridad de la parte pública del certificado, este comando necesita algún permiso en el certificado y que el llamador no haya denegado el permiso VIEW en el certificado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-exporting-a-certificate-to-a-file"></a>A. Exportar un certificado a un archivo  
 El siguiente ejemplo exporta un certificado a un archivo.  
  
```  
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert';  
GO  
```  
  
### <a name="b-exporting-a-certificate-and-a-private-key"></a>B. Exportar un certificado y una clave privada  
 En el siguiente ejemplo, la clave privada del certificado del que se realiza una copia de seguridad se cifra con la contraseña `997jkhUbhk$w4ez0876hKHJH5gh`.  
  
```  
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert'  
    WITH PRIVATE KEY ( FILE = 'c:\storedkeys\sales05key' ,   
    ENCRYPTION BY PASSWORD = '997jkhUbhk$w4ez0876hKHJH5gh' );  
GO  
```  
  
### <a name="c-exporting-a-certificate-that-has-an-encrypted-private-key"></a>C. Exportar un certificado con una clave privada cifrada  
 En el siguiente ejemplo, la clave privada del certificado se cifra en la base de datos. La clave privada debe descifrarse con la contraseña `9875t6#6rfid7vble7r`. Cuando se guarda el certificado en el archivo de copia de seguridad, la clave privada se cifra con la contraseña `9n34khUbhk$w4ecJH5gh`.  
  
```  
BACKUP CERTIFICATE sales09 TO FILE = 'c:\storedcerts\sales09cert'   
    WITH PRIVATE KEY ( DECRYPTION BY PASSWORD = '9875t6#6rfid7vble7r' ,  
    FILE = 'c:\storedkeys\sales09key' ,   
    ENCRYPTION BY PASSWORD = '9n34khUbhk$w4ecJH5gh' );  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)  
 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)  
 [CERTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/certproperty-transact-sql.md)  
  
  

