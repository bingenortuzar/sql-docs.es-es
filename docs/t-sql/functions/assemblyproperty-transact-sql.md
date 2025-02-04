---
title: ASSEMBLYPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASSEMBLYPROPERTY_TSQL
- ASSEMBLYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASSEMBLYPROPERTY statement
- assemblies [CLR integration], properties
ms.assetid: cf03d1b1-724c-48bf-a8df-3fe2586b150a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ac25131e24aa89253abfc13eac69a4a60d0b7aee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040291"
---
# <a name="assemblyproperty-transact-sql"></a>ASSEMBLYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Esta función devuelve información sobre una propiedad de un ensamblado.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
ASSEMBLYPROPERTY('assembly_name', 'property_name')  
```  
  
## <a name="arguments"></a>Argumentos  
*assembly_name*  
Nombre del ensamblado.
  
*property_name*  
El nombre de una propiedad de la que se va a recuperar información. *property_name* puede tener uno de los valores siguientes:
  
|Valor|Descripción|  
|---|---|
|**CultureInfo**|Configuración regional del ensamblado.|  
|**PublicKey**|Clave pública o símbolo (token) de clave pública del ensamblado.|  
|**MvID**|Número completo de identificación de versión del ensamblado generado por el compilador.|  
|**VersionMajor**|Componente principal (primera parte) del número de identificación de la versión de cuatro partes del ensamblado.|  
|**VersionMinor**|Componente secundario (segunda parte) del número de identificación de la versión de cuatro partes del ensamblado.|  
|**VersionBuild**|Componente de generación (tercera parte) del número de identificación de la versión de cuatro partes del ensamblado.|  
|**VersionRevision**|Componente de revisión (cuarta parte) del número de identificación de la versión de cuatro partes del ensamblado.|  
|**SimpleName**|Nombre sencillo del ensamblado.|  
|**Arquitectura**|Arquitectura del procesador del ensamblado.|  
|**CLRName**|Cadena canónica que codifica el nombre sencillo, número de versión, referencia cultural, clave pública y arquitectura del ensamblado. Este valor identifica de forma única el ensamblado en Common Language Runtime (CLR).|  
  
## <a name="return-type"></a>Tipo de valor devuelto
**sql_variant**
  
## <a name="examples"></a>Ejemplos  
En este ejemplo, se supone que se registra un ensamblado de `HelloWorld` en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Para más información, vea [Ejemplo de Hola a todos](https://msdn.microsoft.com/library/fed6c358-f5ee-4d4c-9ad6-089778383ba7).
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ASSEMBLYPROPERTY ('HelloWorld' , 'PublicKey');  
```  
  
## <a name="see-also"></a>Vea también
[CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
[DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)
  
  
