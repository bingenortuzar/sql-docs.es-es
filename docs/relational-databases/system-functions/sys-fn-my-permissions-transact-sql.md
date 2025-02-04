---
title: Sys.fn_my_permissions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_my_permissions_TSQL
- fn_my_permissions_TSQL
- sys.fn_my_permissions
- fn_my_permissions
dev_langs:
- TSQL
helpviewer_keywords:
- fn_my_permissions function
- sys.fn_my_permissions function
ms.assetid: 30f97f00-03d8-443a-9de9-9ec420b7699b
author: rothja
ms.author: jroth
ms.openlocfilehash: 0a64db42ba04e864752559bb2d2b895625f2c9f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122633"
---
# <a name="sysfnmypermissions-transact-sql"></a>sys.fn_my_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una lista de los permisos concedidos a la entidad de seguridad para un elemento protegible. Una función relacionada es [HAS_PERMS_BY_NAME](../../t-sql/functions/has-perms-by-name-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn_my_permissions ( securable , 'securable_class' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *securable*  
 Es el nombre del elemento protegible. Si el elemento protegible es el servidor o una base de datos, este valor debe establecerse en NULL. *securable* es una expresión escalar de tipo **sysname**. *elemento protegible* puede ser un nombre de varias partes.  
  
 '*securable_class*'  
 Es el nombre de la clase de protegible cuyos permisos se muestran. *securable_class* es un **sysname**. *securable_class* debe ser uno de los siguientes: ROL DE APLICACIÓN, ENSAMBLADO, CLAVE ASIMÉTRICA, CERTIFICADO, CONTRATO, BASE DE DATOS, ENDPOINT, FULLTEXT CATALOG, INICIO DE SESIÓN, TIPO DE MENSAJE, OBJETO, ENLACE DE SERVICIO REMOTO, ROL, RUTA, ESQUEMA, SERVIDOR, SERVICIO, CLAVE SIMÉTRICA, TIPO, USUARIO, COLECCIÓN DE ESQUEMAS XML.  
  
## <a name="columns-returned"></a>Columnas devueltas  
 La tabla siguiente enumeran las columnas que **fn_my_permissions** devuelve. En cada fila devuelta se describe un permiso correspondiente al contexto de seguridad actual del elemento protegible. Devuelve NULL si la consulta da error.  
  
|Nombre de columna|Type|Descripción|  
|-----------------|----------|-----------------|  
|entity_name|**sysname**|Nombre del elemento protegible en el que se conceden los permisos indicados.|  
|subentity_name|**sysname**|Nombre de columna si el elemento protegible tiene columnas; de lo contrario, es NULL.|  
|permission_name|**nvarchar**|Nombre del permiso.|  
  
## <a name="remarks"></a>Comentarios  
 Esta función con valores de tabla devuelve una lista de los permisos efectivos correspondientes a la entidad de seguridad que realiza la llamada para un elemento protegible determinado. Un permiso efectivo es cualquiera de los siguientes:  
  
-   Un permiso concedido directamente a la entidad de seguridad, no denegado.  
  
-   Un permiso implícito en un permiso de nivel superior de la entidad de seguridad, no denegado.  
  
-   Un permiso concedido a un rol o grupo al que pertenece la entidad de seguridad, no denegado.  
  
-   Un permiso de un rol o grupo al que pertenece la entidad de seguridad, no denegado.  
  
 La evaluación de permisos siempre se realiza en el contexto de seguridad del autor de la llamada. Para determinar si otra entidad de seguridad tiene un permiso efectivo, el autor de la llamada debe tener el permiso IMPERSONATE en dicha entidad.  
  
 En el caso de entidades de esquema, se aceptan nombres no NULL de una, dos o tres partes. Para las entidades de nivel de base de datos, se acepta un nombre de una parte, con un valor null que significa "*base de datos actual*". En el caso del servidor, es necesario un valor NULL (que significa "servidor actual"). **fn_my_permissions** no se puede comprobar los permisos en un servidor vinculado.  
  
 La consulta siguiente devuelve una lista de clases de elementos protegibles integrados:  
  
```  
SELECT DISTINCT class_desc FROM fn_builtin_permissions(default)  
    ORDER BY class_desc;  
GO  
```  
  
 Si se especifica DEFAULT como valor de *protegible* o *securable_class*, el valor se interpretará como NULL.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-effective-permissions-on-the-server"></a>A. Enumerar los permisos efectivos del servidor  
 El ejemplo siguiente devuelve una lista de los permisos efectivos del autor de la llamada en el servidor.  
  
```  
SELECT * FROM fn_my_permissions(NULL, 'SERVER');  
GO  
```  
  
### <a name="b-listing-effective-permissions-on-the-database"></a>b. Enumerar los permisos efectivos de la base de datos  
 El ejemplo siguiente devuelve una lista de los permisos efectivos del autor de la llamada en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions (NULL, 'DATABASE');  
GO  
```  
  
### <a name="c-listing-effective-permissions-on-a-view"></a>C. Enumerar los permisos efectivos de una vista  
 El ejemplo siguiente devuelve una lista de los permisos efectivos del autor de la llamada en la vista `vIndividualCustomer` del esquema `Sales` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions('Sales.vIndividualCustomer', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;   
GO   
```  
  
### <a name="d-listing-effective-permissions-of-another-user"></a>D. Enumerar los permisos efectivos de otro usuario  
 El ejemplo siguiente devuelve una lista de los permisos efectivos del usuario de base de datos `Wanida` en la tabla `Employee` del esquema `HumanResources` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. El autor de la llamada requiere el permiso IMPERSONATE en el usuario `Wanida`.  
  
```  
EXECUTE AS USER = 'Wanida';  
SELECT * FROM fn_my_permissions('HumanResources.Employee', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;    
REVERT;  
GO  
```  
  
### <a name="e-listing-effective-permissions-on-a-certificate"></a>E. Enumerar los permisos efectivos de un certificado  
 El ejemplo siguiente devuelve una lista de los permisos efectivos del autor de la llamada en un certificado denominado `Shipping47` en la base de datos actual.  
  
```  
SELECT * FROM fn_my_permissions('Shipping47', 'CERTIFICATE');  
GO  
```  
  
### <a name="f-listing-effective-permissions-on-an-xml-schema-collection"></a>F. Enumerar los permisos efectivos de una colección de esquemas XML  
 El ejemplo siguiente devuelve una lista de los permisos efectivos del autor de llamada en una colección de esquemas XML denominada `ProductDescriptionSchemaCollection` en el [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] base de datos.  
  
```  
USE AdventureWorks2012;  
SELECT * FROM fn_my_permissions('ProductDescriptionSchemaCollection',  
    'XML SCHEMA COLLECTION');  
GO  
```  
  
### <a name="g-listing-effective-permissions-on-a-database-user"></a>G. Enumerar los permisos efectivos de un usuario de base de datos  
 El ejemplo siguiente devuelve una lista de los permisos efectivos del autor de la llamada en un usuario denominado `MalikAr` en la base de datos actual.  
  
```  
SELECT * FROM fn_my_permissions('MalikAr', 'USER');  
GO  
```  
  
### <a name="h-listing-effective-permissions-of-another-login"></a>H. Enumerar los permisos efectivos de otro inicio de sesión  
 El ejemplo siguiente devuelve una lista de los permisos efectivos del inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `WanidaBenshoof` en la tabla `Employee` del esquema `HumanResources` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. El autor de la llamada requiere el permiso IMPERSONATE en el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `WanidaBenshoof`.  
  
```  
EXECUTE AS LOGIN = 'WanidaBenshoof';  
SELECT * FROM fn_my_permissions('AdventureWorks2012.HumanResources.Employee', 'OBJECT')   
    ORDER BY subentity_name, permission_name ;    
REVERT;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [Jerarquía de permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  
