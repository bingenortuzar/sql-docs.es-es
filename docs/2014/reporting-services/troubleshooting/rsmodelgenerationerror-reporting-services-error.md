---
title: 'rsModelGenerationError: error de Reporting Services | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsModelGenerationError
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 713de57f0f2957983966f8ef0345bb374c311781
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099223"
---
# <a name="rsmodelgenerationerror---reporting-services-error"></a>rsModelGenerationError - Error de Reporting Services
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|rsRenderingError|  
|Origen del evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto del mensaje|Error al generar el modelo. (rsModelGenerationError) (ReportingServicesLibrary) %1|  
  
## <a name="explanation"></a>Explicación  
 No se puede generar el modelo de informe. En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 SP1 y en versiones anteriores, es más probable que se muestre este error cuando el objeto System.Data.DataSet no puede controlar una tabla o relación del esquema de la base de datos, como cuando, por ejemplo, se definen dos claves externas para la misma columna de una tabla.  
  
## <a name="user-action"></a>Acción del usuario  
 Para determinar el motivo específico por el que aparece este mensaje de error, revise los archivos de registro del servidor de informes, que se encuentran en \Microsoft SQL Server\\<Instancia de SQL Server\>\Reporting Services\LogFiles.  
  
## <a name="internal-only"></a>Solo para uso interno  
  
