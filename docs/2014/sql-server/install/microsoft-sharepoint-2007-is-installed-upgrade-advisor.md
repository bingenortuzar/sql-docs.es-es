---
title: Microsoft SharePoint 2007 está instalado (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6f1da295-d9b7-4948-99d3-ebd3587337c6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 84672ddf6a9b2912f3d53eef8d40727369376ba5
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952094"
---
# <a name="microsoft-sharepoint-2007-is-installed-upgrade-advisor"></a>Microsoft SharePoint 2007 está instalado (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado una versión no compatible de un producto o una tecnología de SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** @no__t el modo de SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no se actualizará ni instalará en SharePoint 2007. La actualización está bloqueada.  
  
## <a name="corrective-action"></a>Acción correctora  
 Para continuar con la actualización, debe desinstalar SharePoint 2007 o actualizar SharePoint 2007 a un producto SharePoint 2010. Una vez que haya actualizado la instalación de SharePoint, vuelva a ejecutar el Asesor de actualizaciones para confirmar que no hay otros problemas de actualización.  
  
 No es posible actualizar directamente de SharePoint 2007 a SharePoint 2013. pero puede hacer lo que se conoce como adjuntar una base de datos de "salto doble" para actualizar desde Office SharePoint Server 2007 a SharePoint Server 2010 y, a continuación, desde SharePoint Server 2010 a SharePoint Server 2013.  
  
## <a name="see-also"></a>Vea también  
 [Asesor de actualizaciones &#40;de Reporting Services upgrade issues&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
