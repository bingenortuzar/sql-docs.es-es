---
title: Propiedad DatabaseLogonType (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- DatabaseLogonType
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonType property
ms.assetid: 6b592582-4c35-4029-ab86-982fff47d8d6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b58c380b85e412554eb47315dfe356d3bff08d03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097818"
---
# <a name="databaselogontype-property-wmi-msreportserverconfigurationsetting"></a>Propiedad DatabaseLogonType (WMI MSReportServer_ConfigurationSetting)
  Especifica si el servidor de informes usa una cuenta de servicio de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, una cuenta de usuario de Windows o un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tener acceso a la base de datos del servidor de informes. Solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Un objeto `integer` que representa el tipo de inicio de sesión.  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Los valores son:  
  
-   0 para el inicio de sesión de Windows  
  
-   1 para el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 para el inicio de sesión como un servicio  
  
 Si especifica 0 (Windows), debe establecer el valor de la propiedad [DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md) en una cuenta de usuario de Windows válida correspondiente.  
  
 Si especifica 1 (SQL Server), asegúrese de que el valor de [DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md) se corresponda con un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido.  
  
 Si especifica 2 (servicio de Windows), el servidor de informes usará una cuenta de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] y la cuenta de servicio de Windows para tener acceso a la base de datos del servidor de informes. Se omite la propiedad DatabaseLogonAccount.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
