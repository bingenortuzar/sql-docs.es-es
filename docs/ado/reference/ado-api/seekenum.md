---
title: SeekEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 886825b4d32354572a5162487add419b00ec35d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931062"
---
# <a name="seekenum"></a>SeekEnum
Especifica el tipo de [Seek](../../../ado/reference/ado-api/seek-method.md) para ejecutar.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|Busca la primera clave igual a *KeyValues*.|  
|**adSeekLastEQ**|2|Busca la última clave igual a *KeyValues*.|  
|**adSeekAfterEQ**|4|Busca una clave igual a *KeyValues* o justo después de donde se habría producido esa coincidencia.|  
|**adSeekAfter**|8|Busca una clave justo después de donde una coincidencia con *KeyValues* habría producido.|  
|**adSeekBeforeEQ**|16|Busca una clave igual a *KeyValues*o justo antes de donde se habría producido esa coincidencia.|  
|**adSeekBefore**|32|Busca una clave justo antes de que una coincidencia con *KeyValues* habría producido.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>Se aplica a  
 [El método de búsqueda](../../../ado/reference/ado-api/seek-method.md)
