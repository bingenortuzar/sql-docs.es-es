---
title: LineSeparator (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0343954f549f2cba4b535b8ab4ebafec5a842015
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918284"
---
# <a name="lineseparator-property-ado"></a>Separador de línea (propiedad, ADO)
Indica el carácter binario que se usará como separador de línea en texto [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md) valor que indica el carácter de separador de línea utilizado en el **Stream**. El valor predeterminado es **adCRLF**.  
  
## <a name="remarks"></a>Comentarios  
 **LineSeparator** se usa para interpretar líneas al leer el contenido de un texto **Stream**. Se pueden omitir las líneas con el [SkipLine](../../../ado/reference/ado-api/skipline-method.md) método.  
  
 **LineSeparator** solo se usa con texto **Stream** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) es **adTypeText**). Esta propiedad se omite si **tipo** es **adTypeBinary**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
