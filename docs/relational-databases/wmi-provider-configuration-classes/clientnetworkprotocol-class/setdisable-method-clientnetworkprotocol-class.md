---
title: Método SetDisable (clase ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDisable Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDisable method
ms.assetid: bce69ab9-ea5b-43fd-8114-08b1b5890755
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f85c61369c2b5e8b8ec0bd24607d82a8dcc39cfd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040859"
---
# <a name="setdisable-method-clientnetworkprotocol-class"></a>Método SetDisable (clase ClientNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Deshabilita el protocolo de red de cliente especificado por el [configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetDisable()  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [clase ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa el protocolo de red utilizado por el cliente de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar bibliotecas de red y protocolos de red de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
