---
title: FULLTEXTSERVICEPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FULLTEXTSERVICEPROPERTY_TSQL
- FULLTEXTSERVICEPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], properties
- FULLTEXTSERVICEPROPERTY function
- services [SQL Server], full-text search properties
- test
ms.assetid: b7dcacb0-af83-4807-9d1e-49148b56b59c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 726b071c222580ec75091477dc68509cdb71e1e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940252"
---
# <a name="fulltextserviceproperty-transact-sql"></a>FULLTEXTSERVICEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información relacionada con las propiedades del motor de búsqueda de texto completo. Estas propiedades se pueden establecer y recuperar usando **sp_fulltext_service**.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FULLTEXTSERVICEPROPERTY ('property')  
```  
  
## <a name="arguments"></a>Argumentos  
 *property*  
 Es una expresión que contiene el nombre de la propiedad del servicio de búsqueda en texto completo. La tabla presenta las propiedades y proporciona descripciones de la información que se devuelve.  
  
> [!NOTE]
>  Las propiedades siguientes se quitarán en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **ConnectTimeout**, **DataTimeout** y **ResourceUsage**. Evite el uso de estas propiedades en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que las usan actualmente.  
  
|Propiedad|Valor|  
|--------------|-----------|  
|**ResourceUsage**|Devuelve 0. Se admite únicamente por compatibilidad con versiones anteriores.|  
|**ConnectTimeout**|Devuelve 0. Se admite únicamente por compatibilidad con versiones anteriores.|  
|**IsFulltextInstalled**|El componente de texto completo se instala con la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = El componente de texto completo no está instalado.<br /><br /> 1 = El componente de texto completo está instalado.<br /><br /> NULL = Entrada no válida o error.|  
|**DataTimeout**|Devuelve 0. Se admite únicamente por compatibilidad con versiones anteriores.|  
|**LoadOSResources**|Indica si los separadores de palabras y filtros del sistema operativo se registran y utilizan con esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, esta propiedad está deshabilitada para impedir cambios de comportamiento involuntarios por actualizaciones del sistema operativo. Habilitar el uso de recursos del sistema operativo proporciona acceso a recursos de idiomas y tipos de documento registrados en los Servicios de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Index Server, pero que no tienen instalado un recurso específico de la instancia. Si habilita la carga de recursos del sistema operativo, asegúrese de que son binarios con firma de confianza; de lo contrario, no se pueden cargar cuando **VerifySignature** se establece en 1.<br /><br /> 0 = Utiliza solo los filtros y separadores de palabras específicos de esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = Cargar filtros del sistema operativo y separadores de palabras.|  
|**VerifySignature**|Especifica si el servicio de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search carga solo binarios con firma. De forma predeterminada, solo se cargan binarios con firma de confianza.<br /><br /> 0 = No comprueba si los binarios están firmados.<br /><br /> 1 = Comprueba que solo se cargan binarios con firma de confianza.|  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se comprueba si solo se cargan binarios con firma, y el valor devuelto indica que esta comprobación no se está produciendo.  
  
```  
SELECT fulltextserviceproperty('VerifySignature');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
0  
```  
  
 Tenga en cuenta que para restablecer la comprobación de firmas en su valor predeterminado, 1, puede utilizar la instrucción `sp_fulltext_service` siguiente:  
  
```  
EXEC sp_fulltext_service @action='verify_signature', @value=1;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
  
  
