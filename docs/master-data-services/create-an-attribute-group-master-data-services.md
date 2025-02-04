---
title: Crear un grupo de atributos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], creating
- creating attribute groups [Master Data Services]
ms.assetid: 798c325e-e8d8-412a-b02e-118f2741d1c7
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 988d57ab3d0f86c3da1e45109a6ad818cecb894e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906574"
---
# <a name="create-an-attribute-group-master-data-services"></a>Crear un grupo de atributos (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree grupos de atributos cuando desee mostrar los atributos en pestañas individuales en la cuadrícula **Explorador** .  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Por lo menos debe existir un atributo. Para obtener más información, consulte [Crear un atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md).  
  
### <a name="to-create-an-attribute-group"></a>Para crear un grupo de atributos  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Manage Model** (Administrar modelo), seleccione un modelo de la cuadrícula y después haga clic en **Entidades**.  
  
3.  En la página **Manage Entity** (Administrar entidad), en la cuadrícula, seleccione la fila de la entidad para la que desea crear un grupo de atributos.  
  
4.  Haga clic en **Grupos de atributos**.  
  
5.  En la página Administrar grupos de atributos, realice una de las siguientes acciones y luego haga clic en **Agregar**.  
  
     Si el grupo de atributos es para miembros hoja, seleccione **Hoja** en la lista desplegable **Member Types** (Tipos de miembros) en la parte superior de la página.  
  
     Si el grupo de atributos es para miembros consolidados, seleccione **Consolidado** en la lista desplegable **Member Types** (Tipos de miembros).  
  
     Si el grupo de atributos es para colecciones, seleccione **Colección** en la lista desplegable **Member Types** (Tipos de miembros).  
  
6.  Haga clic en **Grupos hoja**, **Grupos consolidados**o **Grupos de colecciones** para crear un grupo de atributos para los miembros hoja, los miembros consolidados o las colecciones, respectivamente.  
  
7.  En el cuadro **Nombre** , escriba un nombre para el grupo de atributos. Este es el nombre que se muestra en la pestaña del **Explorador**.  
  
8.  Para agregar un atributo, haga clic en el atributo en el cuadro **Atributos disponibles** y luego haga clic en la flecha **Agregar** . Para agregar todos los atributos, haga clic en la flecha **Agregar todo** .  
  
9. Haga clic en las flechas **arriba** y **abajo** para cambiar el orden de izquierda a derecha de los atributos.  
  
10. Haga clic en los usuarios del cuadro **Usuarios disponibles** y luego haga clic en la flecha **Agregar** . Para agregar todos los usuarios, haga clic en la flecha **Agregar todo** .  
  
11. Haga clic en los grupos del cuadro **Grupos disponibles** y luego haga clic en la flecha **Agregar** . Para agregar todos los grupos, haga clic en la flecha **Agregar todo** .  
  
12. Haga clic en **Guardar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Hacer que un grupo de atributos sea visible para los usuarios &#40;Master Data Services&#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Grupos de atributos &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [Cambiar el nombre de un grupo de atributos &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [Eliminar un grupo de atributos &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-group-master-data-services.md)   
 [Permisos de hoja &#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)   
   
  
  
