---
title: Modelo de objetos SMO | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], object model
- SQL Server Management Objects, object model
ms.assetid: bd6e59b6-ca46-42c0-adb2-c9d64cf6e00b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 637c60fd6d7ba53087a145135d7152066983b644
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63130613"
---
# <a name="smo-object-model"></a>Modelo de objetos SMO
  El modelo de objetos SMO se compone de una jerarquía de objetos. El objeto <xref:Microsoft.SqlServer.Management.Smo.Server> es el objeto de nivel superior y todos los objetos de clase de instancia se encuentran debajo del objeto <xref:Microsoft.SqlServer.Management.Smo.Server>.  
  
 La clase <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> es una clase de nivel superior con una jerarquía de objeto independiente. El <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> objeto representa [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicios y la configuración de red disponible a través del proveedor de WMI.  
  
 Además de los objetos <xref:Microsoft.SqlServer.Management.Smo.Server> y <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer>, hay varias clases de utilidad que representan tareas u operaciones, como <xref:Microsoft.SqlServer.Management.Smo.Transfer>, <xref:Microsoft.SqlServer.Management.Smo.Backup> o <xref:Microsoft.SqlServer.Management.Smo.Restore>  
  
 El modelo de objetos SMO se compone de varios espacios de nombres. Para más información, vea [Espacios de nombres SMO](smo-object-model-namespaces.md).  
  
## <a name="see-also"></a>Vea también  
 [Diagrama de modelo de objetos SMO](smo-object-model-diagram.md)   
 [Espacios de nombres SMO](smo-object-model-namespaces.md)   
 [Conceptos del proveedor WMI de administración de configuración](../wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  
