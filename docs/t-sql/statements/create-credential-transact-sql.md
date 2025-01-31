---
title: CREATE CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREDENTIAL_TSQL
- SQL13.SWB.CREDENTIAL.GENERAL.F1
- CREATE CREDENTIAL
- CREATE_CREDENTIAL_TSQL
- CREDENTIAL
dev_langs:
- TSQL
helpviewer_keywords:
- SECRET clause
- authentication [SQL Server], credentials
- CREATE CREDENTIAL statement
- credentials [SQL Server], CREATE CREDENTIAL statement
ms.assetid: d5e9ae69-41d9-4e46-b13d-404b88a32d9d
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 875b66df7f2788d253bad98b92f19c7d63393885
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061029"
---
# <a name="create-credential-transact-sql"></a>CREATE CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Crea una credencial de nivel de servidor. Una credencial es un registro que contiene la información de autenticación necesaria para conectarse a un recurso fuera de SQL Server. La mayoría de las credenciales incluyen un usuario y una contraseña de Windows. Por ejemplo, guardar una copia de seguridad de base de datos en una ubicación cualquiera podría requerir que SQL Server proporcione credenciales especiales para tener acceso a esa ubicación. Para más información, vea [Credenciales (motor de base de datos)](../../relational-databases/security/authentication-access/credentials-database-engine.md).

> [!NOTE]  
>  Para establecer la credencial en el nivel de base de datos, vea [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md). Use una credencial de nivel de servidor cuando necesite usar la misma credencial para varias bases de datos en el servidor. Use una credencial de ámbito de base de datos para hacer que la base de datos sea más portátil. Cuando una base de datos se mueve a un nuevo servidor, la credencial de ámbito de la base de datos se moverá con ella. Use credenciales con ámbito de base de datos en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
        [ FOR CRYPTOGRAPHIC PROVIDER cryptographic_provider_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Especifica el nombre de la credencial que se va a crear. *credential_name* no puede comenzar por el signo de almohadilla (#). Las credenciales del sistema comienzan por ##.  Cuando se usa una Firma de acceso compartido (SAS), este nombre debe coincidir con la ruta de acceso de contenedor, comenzar por https y no contener una barra diagonal. Vea el ejemplo D de abajo.  
  
 IDENTITY **='** _identity\_name_ **'**  
 Especifica el nombre de la cuenta que se utilizará para conectarse fuera del servidor. Cuando la credencial se usa para tener acceso a Azure Key Vault, **IDENTITY** es el nombre del almacén de claves. Vea el ejemplo C más adelante. Cuando la credencial usa una Firma de acceso compartido (SAS), **IDENTITY** es *SHARED ACCESS SIGNATURE*. Vea el ejemplo D de abajo.  
 
> [!IMPORTANT]
> Azure SQL Database solo admite las identidades de Azure Key Vault y de Firma de acceso compartido. No se admiten las identidades de usuario de Windows.
 
 SECRET **='** _secret_ **'**  
 Especifica el secreto necesario para la autenticación de salida.  
  
 Cuando se usa la credencial para acceder a Azure Key Vault, el argumento **SECRET** de **CREATE CREDENTIAL** requiere que los valores de *\<Client ID>* (sin guiones) y *\<Secret>* de una **entidad de servicio** en Azure Active Directory se pasen entre sí sin un espacio entre ellos. Vea el ejemplo C más adelante. Cuando la credencial usa una Firma de acceso compartido (SAS), **SECRET** es el token de la Firma de acceso compartido. Vea el ejemplo D de abajo.  Para información sobre cómo crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure, consulte [Lección 1: Crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure](../../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md).  
  
 FOR CRYPTOGRAPHIC PROVIDER *cryptographic_provider_name*  
 Especifica el nombre de un *Proveedor de administración de claves de la empresa (EKM)* . Para más información sobre la administración de claves, vea [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Notas  

 Si IDENTITY es un usuario de Windows, el secreto puede ser la contraseña. El secreto se cifra usando la clave maestra de servicio. Si se vuelve a generar la clave maestra de servicio, el secreto se vuelve a cifrar con la nueva clave maestra de servicio.  
  
 Una vez creada una credencial, puede asignarla a un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por medio de [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) o [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md). Un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solamente se puede asignar a una credencial, pero una credencial puede asignarse a varios inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, vea [Credenciales &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md). Una credencial de nivel de servidor solo se puede asignar a un inicio de sesión, no a un usuario de base de datos. 
  
 Encontrará más información sobre las credenciales en la vista de catálogo [sys.credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md).  
  
 Si no hay ninguna credencial de inicio de sesión asignada para el proveedor, se utiliza la credencial asignada a la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Un inicio de sesión puede tener asignadas varias credenciales, siempre y cuando se utilicen con proveedores distintos. Solo debe haber una credencial asignada por cada proveedor y por cada inicio de sesión. La misma credencial puede estar asignada a otros inicios de sesión.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso **ALTER ANY CREDENTIAL**.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-basic-example"></a>A. Ejemplo básico  
 En el ejemplo siguiente se crea la credencial denominada `AlterEgo`. La credencial contiene el usuario de Windows `Mary5` y una contraseña.  
  
```  
CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-credential-for-ekm"></a>B. Crear una credencial de EKM  
 En el ejemplo siguiente se utiliza una cuenta creada previamente denominada `User1OnEKM` en un módulo EKM a través de las herramientas de administración de EKM, con un tipo de cuenta y una contraseña básicos. La cuenta **sysadmin** del servidor crea una credencial que se usa para conectar la cuenta de EKM y la asigna a la cuenta `User1` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
CREATE CREDENTIAL CredentialForEKM  
    WITH IDENTITY='User1OnEKM', SECRET='<EnterStrongPasswordHere>'  
    FOR CRYPTOGRAPHIC PROVIDER MyEKMProvider;  
GO  
  
/* Modify the login to assign the cryptographic provider credential */  
ALTER LOGIN Login1  
ADD CREDENTIAL CredentialForEKM;  
  
/* Modify the login to assign a non cryptographic provider credential */   
ALTER LOGIN Login1  
WITH CREDENTIAL = AlterEgo;  
GO  
```  
  
### <a name="c-creating-a-credential-for-ekm-using-the-azure-key-vault"></a>C. Crear una credencial de EKM con Azure Key Vault  
 En el siguiente ejemplo se crea una credencial de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que [!INCLUDE[ssDE](../../includes/ssde-md.md)] la use al tener acceso a Azure Key Vault con el **Conector de SQL Server para Azure Key Vault**. Para ver un ejemplo completo sobre cómo usar el Conector de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Administración extensible de claves con el Almacén de claves de Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
> [!IMPORTANT]  
>  El argumento **IDENTITY** de **CREATE CREDENTIAL** requiere el nombre del Almacén de claves. El argumento **SECRET** de **CREATE CREDENTIAL** requiere que los valores de *\<Client ID>* (sin guiones) y *\<Secret>* se pasen juntos, sin un espacio entre ellos.  
  
 En el ejemplo siguiente, el **Id. de cliente** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) se deja sin guiones y se introduce como la cadena `EF5C8E094D2A4A769998D93440D8115D` . El **secreto** se representa con la cadena *SECRET_DBEngine*.  
  
```  
USE master;  
CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault',   
    SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
```  
  
 En el siguiente ejemplo se crea la misma credencial usando variables para las cadenas **Client ID** y **Secret**, que luego se concatenan entre sí para formar el argumento **SECRET**. La función **REPLACE** se usa para quitar los guiones del identificador de cliente.  
  
```  
DECLARE @AuthClientId uniqueidentifier = 'EF5C8E09-4D2A-4A76-9998-D93440D8115D';  
DECLARE @AuthClientSecret varchar(200) = 'SECRET_DBEngine';  
DECLARE @pwd varchar(max) = REPLACE(CONVERT(varchar(36), @AuthClientId) , '-', '') + @AuthClientSecret;  
  
EXEC ('CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault', SECRET = ''' + @PWD + '''   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;');  
```  
  
### <a name="d-creating-a-credential-using-a-sas-token"></a>D. Crear una credencial con un token de SAS  
 **Se aplica a**: de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a la [versión actual](https://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
 En el siguiente ejemplo se crea una credencial de firma de acceso compartido con un token de SAS.  Para ver un tutorial sobre cómo crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure y, luego, crear una credencial usando la firma de acceso compartido, consulte [Tutorial: Uso del servicio Microsoft Azure Blob Storage con bases de datos de SQL Server 2016](../../relational-databases/tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
> [!IMPORTANT]  
>  El argumento **CREDENCIAL NAME** requiere que el nombre coincida con la ruta de acceso del contenedor, comience por https y no contenga una barra diagonal. El argumento **IDENTITY** requiere el nombre, *SHARED ACCESS SIGNATURE*. El argumento **SECRET** requiere el token de firma de acceso compartido.  
>
>  El secreto **SHARED ACCESS SIGNATURE** no debe tener el signo **?** inicial.
  
```  
USE master  
CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a trailing forward slash.  
   WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
   , SECRET = 'sharedaccesssignature' -- this is the shared access signature token   
GO    
```  
  
## <a name="see-also"></a>Consulte también  
 [Credenciales &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [Lección 2: Crear una credencial de SQL Server con una firma de acceso compartido](../../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)   
 [Firmas de acceso compartido](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
  
  
