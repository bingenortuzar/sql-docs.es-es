---
title: Confirmar una versión (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- committing versions [Master Data Services]
- versions [Master Data Services], committing
ms.assetid: 6b967a39-b333-4b84-9e5f-4fb07e156826
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 65ac3c0c590a3b5d1fc03ab17625f039c163ac57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480034"
---
# <a name="commit-a-version-master-data-services"></a>Confirmar una versión (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], confirme una versión de un modelo para evitar cambios en los miembros del modelo y en sus atributos. Las versiones confirmadas no se pueden desbloquear.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer del permiso para tener acceso al área funcional de **Administración de versiones** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   El estado de la versión debe ser **Bloqueado**. Para obtener más información, vea [Bloquear una versión &#40;Master Data Services&#41;](../../2014/master-data-services/lock-a-version-master-data-services.md).  
  
-   Todos los miembros deben haberse validado correctamente.  
  
### <a name="to-commit-a-version"></a>Para confirmar una versión  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración de versiones**.  
  
2.  En la página **Administrar versiones** , en la barra de menús, haga clic en **Validar versión**.  
  
3.  En la página **Validar versión** , seleccione el modelo y la versión que desea confirmar.  
  
4.  Haga clic en **Confirmar**.  
  
5.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Crear una marca de versión &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md)  
  
-   [Asignar una marca a una versión &#40;Master Data Services&#41;](../../2014/master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
-   [Copiar una versión &#40;Master Data Services&#41;](../../2014/master-data-services/copy-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Versiones &#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
  
