---
title: Database (DTA, elemento de Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5817a6d32ff94aaba7e4c0a573e6cd6a5fd586dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116929"
---
# <a name="database-element-for-server-dta"></a>Elemento Database para servidor (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifica la base de datos que se desea optimizar en un servidor concreto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno.|  
|Valor predeterminado|Ninguno.|  
|Repetición|Obligatoria una o más veces por elemento **Server** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|Elemento primario|[Server &#40;DTA, elemento&#41;](../../tools/dta/server-element-dta.md)|  
|Elementos secundarios|[Name &#40;DTA, elemento de Database&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Schema &#40;DTA, elemento de Database&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Notas  
 Este elemento tiene el nombre **DatabaseDetailsTypecomplexType** en el esquema XML del Asistente para la optimización de motor de base de datos. No confunda este elemento **Database** con el que tiene al elemento **Configuration** como raíz primaria. Para obtener más información, vea [Database &#40;DTA, elemento de Configuration&#41;](../../tools/dta/database-element-for-configuration-dta.md).  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo del uso del elemento **Database** , vea [Server &#40;DTA, elemento&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
