---
title: Método SetValue (clase ServerSettingsGeneralFlag) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetValue Method (ServerSettingsGeneralFlag Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetValue method
ms.assetid: a889feac-c0e0-4635-b506-843863d86967
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ec0a215db84b8b1d8dbd2d12e603a365f6a54023
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68052671"
---
# <a name="setvalue-method-serversettingsgeneralflag-class"></a>Método SetValue (clase ServerSettingsGeneralFlag)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Establece todos los valores de la marca a la que se hace referencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetValue(Value)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase ServerSettingsGeneralFlag](../../../relational-databases/wmi-provider-configuration-classes/serversettingsgeneralflag-class/serversettingsgeneralflag-class.md) que representa una marca general para la configuración del servidor.  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*Valor*|Valor booleano que especifica el valor de la marca.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de red de servidor y las bibliotecas de red](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
