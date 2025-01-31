---
title: Acceso por navegación (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- navigational access [Master Data Services]
- security [Master Data Services], navigational access
ms.assetid: 3403b7b0-44e2-48c3-a1b7-9c4612b874b8
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 1d190d55c45530adde1b41658c975bbfc19c0b91
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482637"
---
# <a name="navigational-access-master-data-services"></a>Acceso por navegación (Master Data Services)
  El acceso por navegación se aplica a la seguridad de los objetos de modelos, que se asigna en la pestaña **Modelos** .  
  
 El acceso por navegación es el que se obtiene para niveles superiores a los que su seguridad le haya asignado.  
  
 En este ejemplo, los permisos se asignan a una entidad y el acceso por navegación se concede en el nivel de modelo.  
  
 ![mds_conc_inheritance_model](../../2014/master-data-services/media/mds-conc-inheritance-model.gif "mds_conc_inheritance_model")  
  
 **Entidades**  
  
 Cuando se asigna permiso a una entidad, a sus miembros hoja o a sus miembros consolidados, el acceso por navegación significa que se pueden leer o actualizar el nombre y el código de todos los miembros. También se puede leer el nombre del modelo.  
  
 **Atributos**  
  
 Cuando se asigna permiso a un atributo, el acceso por navegación significa que se pueden leer o actualizar el nombre y el código de todos los miembros de la entidad. También se puede leer el nombre del modelo.  
  
 **Colecciones**  
  
 Cuando se asignan permisos a las colecciones, se pueden leer o actualizar el nombre, el código, la descripción y el identificador del propietario. También se puede leer el nombre del modelo.  
  
## <a name="see-also"></a>Vea también  
 [Cómo se determinan los permisos &#40;Master Data Services&#41;](how-permissions-are-determined-master-data-services.md)  
  
  
