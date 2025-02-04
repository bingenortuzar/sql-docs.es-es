---
title: Guardar paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0e4e9c8ea3300c35cb75d451206ab9869f932814
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62889328"
---
# <a name="save-packages"></a>Guardar paquetes
  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] , se generan los paquetes con el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] y se guardan en el sistema de archivos como archivos XML (archivos .dtsx). También puede guardar copias del archivo XML de paquete en la base de datos msdb, en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , o en el almacén de paquetes. El almacén de paquetes representa las carpetas en la ubicación del sistema de archivos que el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] administra.  
  
 Si guarda un paquete en el sistema de archivos, puede usar más tarde el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para importar el paquete a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o al almacén de paquetes. Para más información, vea [Importar y exportar paquetes servicio &#40;SSIS&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md).  
  
 También puede usar una utilidad de símbolo del sistema, **dtutil**, para copiar un paquete entre el sistema de archivos y msdb. Para más información, consulte [dtutil Utility](dtutil-utility.md).  
  
### <a name="to-save-a-package"></a>Para guardar un paquete  
  
-   [Guardar un paquete en el sistema de archivos](../../2014/integration-services/save-a-package-to-the-file-system.md)  
  
-   [Guardar una copia de un paquete](../../2014/integration-services/save-a-copy-of-a-package.md)  
  
  
