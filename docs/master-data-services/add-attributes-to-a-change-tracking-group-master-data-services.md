---
title: Agregar atributos a un grupo de seguimiento de cambios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking groups [Master Data Services]
- attributes [Master Data Services], change tracking groups
- change tracking groups [Master Data Services], adding attributes
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f3ba92322f64550f8a773b49ba533e96e113e17f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047889"
---
# <a name="add-attributes-to-a-change-tracking-group-master-data-services"></a>Agregar atributos a un grupo de seguimiento de cambios (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], agregue los atributos a un grupo de seguimiento de cambios cuando desee realizar el seguimiento de los cambios de los valores de atributos.  
  
> [!NOTE]  
>  Después de agregar un atributo a un grupo de seguimiento de cambios, cuando los valores del atributo cambian, el atributo se marca como que ha cambiado en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Cree una regla de negocios para realizar una acción según el cambio.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Los atributos deben existir para agregarlos al grupo de seguimiento de cambios. Para obtener más información, vea [Crear un atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md).  
  
### <a name="to-add-attributes-to-a-change-tracking-group"></a>Agregar atributos a un grupo de seguimiento de cambios  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Manage Model** (Administrar modelo), seleccione un modelo de la cuadrícula y después haga clic en **Entidades**.  
  
3.  En la página **Manage Entity** (Administrar entidad), seleccione la fila de la entidad para la que desea crear un atributo.  
  
4.  Haga clic en **Atributos**.  
  
5.  En la página **Administrar atributos** , realice una de las siguientes acciones.  
  
    -   Si el atributo es para miembros hoja, seleccione **Hoja** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
    -   Si el atributo es para miembros consolidados, seleccione **Consolidado** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
    -   Si el atributo es para colecciones, seleccione **Colección** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
6.  Seleccione la fila del atributo que desea editar y después haga clic en **Editar**.  
  
7.  Active la casilla **Habilitar seguimiento de cambios** .  
  
8.  En el cuadro **Grupo de seguimiento de cambios** , escriba un número para el grupo.  
  
9. Haga clic en **Guardar atributo**.  
  
     En el caso del atributo editado, la columna **Enable Change Tracking Group** (Habilitar grupo de seguimiento de cambios) de la cuadrícula cambia a **Yes (Group: entered group number)** [Sí (Grupo: número de grupo especificado)].  
  
10. Repita este procedimiento para todos los atributos que desea incluir en el grupo. Utilice el mismo número de grupo de seguimiento de cambios para cada atributo del grupo.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
-   [Iniciar acciones según los cambios de valores de atributos &#40;Master Data Services&#41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear un atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [Crear un atributo basado en dominio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
