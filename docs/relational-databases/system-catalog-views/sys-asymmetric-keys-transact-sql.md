---
title: Sys.asymmetric_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- asymmetric_keys
- sys.asymmetric_keys_TSQL
- asymmetric_keys_TSQL
- sys.asymmetric_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.asymmetric_keys catalog view
ms.assetid: bbca796a-9bb5-4a62-9ca8-1d255984553d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c05aa2d1543cfc3ebd1cbab6c199cd2992febfe2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070472"
---
# <a name="sysasymmetrickeys-transact-sql"></a>sys.asymmetric_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada clave asimétrica.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre de la clave. Es único en la base de datos.|  
|**principal_id**|**int**|Id. de la entidad de seguridad de la base de datos propietaria de la clave.|  
|**asymmetric_key_id**|**int**|Id. de la clave. Es único en la base de datos.|  
|**pvt_key_encryption_type**|**char(2)**|Forma en que se cifra la contraseña.<br /><br /> NA = No cifrada.<br /><br /> MK = La clave está cifrada mediante la clave maestra<br /><br /> PW = La clave está cifrada mediante una contraseña definida por el usuario<br /><br /> SK = La clave está cifrada mediante la clave maestra de servicio.|  
|**pvt_key_encryption_type_desc**|**nvarchar(60)**|Descripción de cómo se ha cifrado la clave privada.<br /><br /> NO_PRIVATE_KEY<br /><br /> ENCRYPTED_BY_MASTER_KEY<br /><br /> ENCRYPTED_BY_PASSWORD<br /><br /> ENCRYPTED_BY_SERVICE_MASTER_KEY|  
|**thumbprint**|**varbinary(32)**|Hash de la tecla 1 SHA. El hash es globalmente único.|  
|**algorithm**|**char(2)**|Algoritmo usado con la clave.<br /><br /> 1R = RSA de 512 bits<br /><br /> 2R = RSA de 1024 bits<br /><br /> 3R = RSA de 2048 bits|  
|**algorithm_desc**|**nvarchar(60)**|Descripción del algoritmo usado con la clave.<br /><br /> RSA_512<br /><br /> RSA_1024<br /><br /> RSA_2048|  
|**key_length**|**int**|Longitud en bits de la clave|  
|**sid**|**varbinary(85)**|SID del inicio de sesión de esta clave Para las claves de Administración extensible de claves, este valor será NULL.|  
|**string_sid**|**nvarchar(128)**|Representación de cadena del SID de inicio de sesión de la clave Para las claves de Administración extensible de claves, este valor será NULL.|  
|**public_key**|**varbinary(max)**|Public_key|  
|**attested_by**|**nvarchar(260)**|Solo para uso del sistema.|  
|**provider_type**|**nvarchar(120)**|Tipo de proveedor criptográfico:<br /><br /> CRYPTOGRAPHIC PROVIDER = claves de Administración extensible de claves<br /><br /> NULL = Claves que no sean de Administración extensible de claves|  
|**cryptographic_provider_guid**|**uniqueidentifier**|GUID del proveedor criptográfico. Para las claves que no sean de Administración extensible de claves, este valor será NULL.|  
|**cryptographic_provider_algid**|**sql_variant**|Identificador del algoritmo del proveedor criptográfico. Para las claves que no sean de Administración extensible de claves, este valor será NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
  
