---
title: Propiedad PropertyValType (clase ServerNetworkProtocolProperty) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- PropertyValType Property (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- PropertyValType property
ms.assetid: fbd42e8e-0642-4a19-b3c8-6ce88345145f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4a69cb8f0817c086537381a87b96dfb237b8d59c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62643196"
---
# <a name="propertyvaltype-property-servernetworkprotocolproperty-class"></a>Propiedad PropertyValType (clase ServerNetworkProtocolProperty)
  Obtiene el tipo de datos del valor almacenado en la propiedad a la que se hace referencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.PropertyValType [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Un [clase ServerNetworkProtocolProperty](servernetworkprotocolproperty-class.md) objeto que representa un atributo del protocolo de red en la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor `uint32` que especifica el tipo de datos del valor de propiedad. Devuelve 0 para un valor de cadena y 1 para un tipo numérico.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de red de servidor y las bibliotecas de red](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
