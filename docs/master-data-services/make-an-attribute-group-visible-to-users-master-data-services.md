---
title: Hacer que un grupo de atributos sea visible para los usuarios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ce8d0490625780459ecafd8e9d346af0fc9bd1f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054531"
---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>Hacer que un grupo de atributos sea visible para los usuarios (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], haga que un grupo de atributos sea visible para los usuarios o los grupos cuando desee que los usuarios tengan pestañas en la cuadrícula del área funcional de **Explorador** .  
  
 Cuando se crea un grupo de atributos, se oculta automáticamente para todos los usuarios excepto para la persona que lo creó.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Por lo menos debe existir un grupo de atributos. Para obtener más información, vea [Crear un grupo de atributos &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md).  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>Para hacer que un grupo de atributos sea visible para los usuarios  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Manage Model** (Administrar modelo), seleccione un modelo de la cuadrícula y después haga clic en **Entidades**.  
  
3.  En la página **Manage Entity** (Administrar entidad), en la cuadrícula, seleccione la fila de la entidad para la que desea editar el grupo de atributos.  
  
4.  Haga clic en **Grupos de atributos**.  
  
5.  En la página **Administrar grupos de atributos** , seleccione el tipo de miembro en la lista desplegable **Member Types** (Tipos de miembros) para expandir **Hoja**, **Consolidado** o **Colección**, según el tipo de grupo que quiera hacer visible.  
  
6.  Seleccione el grupo de atributos que desea editar en la cuadrícula y después haga clic en **Editar**.  
  
7.  Haga clic en un usuario o grupo del cuadro **Disponible** y haga clic en la flecha **Agregar** . Para agregarlos todos, haga clic en la flecha **Agregar todo** .  
  
8.  Haga clic en **Guardar**.  
  
## <a name="see-also"></a>Vea también  
 [Grupos de atributos &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [Crear un grupo de atributos &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
