---
title: La propiedad MarshalOptions (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0212f3b4cb663bd56adaa1bdbc3ab6675c3ce888
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932266"
---
# <a name="marshaloptions-property-ado"></a>Propiedad MarshalOptions (ADO)
Indica qué registros de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) van a calcularse las referencias al servidor.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md) valor. El valor predeterminado es **adMarshalAll**.  
  
## <a name="remarks"></a>Comentarios  
 Cuando se usa un cliente [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), los registros que se han modificado en el cliente se reescriben en el nivel intermedio o un servidor Web a través de una técnica denominada cálculo de referencias, el proceso de empaquetado y envío de método de interfaz parámetros a través de límites de proceso o subproceso. Establecer el **MarshalOptions** propiedad puede mejorar el rendimiento cuando se calculan las referencias de datos remotos modificados para la actualización en el nivel intermedio o un servidor Web.  
  
> [!NOTE]
>  **Uso del servicio de datos remoto** esta propiedad se usa solo en un cliente **Recordset**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad MarshalOptions (VB)](../../../ado/reference/ado-api/marshaloptions-property-example-vb.md)   
 [Ejemplo de la propiedad MarshalOptions (VC ++)](../../../ado/reference/ado-api/marshaloptions-property-example-vc.md)   
