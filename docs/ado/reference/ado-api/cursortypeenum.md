---
title: CursorTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorTypeEnum
helpviewer_keywords:
- CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6333934997c9de38b8df1dd08849886ff3dd7f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933272"
---
# <a name="cursortypeenum"></a>CursorTypeEnum
Especifica el tipo de cursor utilizado en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|Utiliza un cursor dinámico. Las adiciones, cambios y eliminaciones realizadas por otros usuarios están visibles y todos los tipos de movimiento a través de la **Recordset** tienen, excepto para marcadores, si el proveedor no los admite.|  
|**adOpenForwardOnly**|0|Predeterminado: Utiliza un cursor de solo avance. Es idéntico a un cursor estático, excepto que solo puede desplazarse hacia delante por los registros. Esto mejora el rendimiento cuando necesite realizar solo un pase a través de un **Recordset**.|  
|**adOpenKeyset**|1|Utiliza un cursor keyset. Al igual que un cursor dinámico, salvo que no puede ver los registros que se agregan otros usuarios, aunque los registros que otros usuarios eliminan son inaccesibles desde su **Recordset**. Cambios en los datos por otros usuarios siguen siendo visibles.|  
|**adOpenStatic**|3|Utiliza un cursor estático, que es una copia estática de un conjunto de registros que puede usar para buscar datos o generar informes. Las adiciones, cambios o eliminaciones realizadas por otros usuarios no son visibles.|  
|**adOpenUnspecified**|-1|No se especifica el tipo de cursor.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CursorType.DYNAMIC|  
|AdoEnums.CursorType.FORWARDONLY|  
|AdoEnums.CursorType.KEYSET|  
|AdoEnums.CursorType.STATIC|  
|AdoEnums.CursorType.UNSPECIFIED|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
