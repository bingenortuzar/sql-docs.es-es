---
title: Eliminar una versión (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- versions [Master Data Services], deleting
- deleting versions [Master Data Services]
ms.assetid: 2a4eeffe-8379-4744-ad44-c27d8c8ac9a8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e0886701a5e3554702c077c2a165029af71a545e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906418"
---
# <a name="delete-a-version-master-data-services"></a>Eliminar una versión (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], elimine una versión cuando esté seguro de que ya no necesita los datos maestros asociados a la misma. Después de eliminar una versión, no puede recuperar los datos maestros asociados.  
  
> [!WARNING]  
>  Si un modelo tiene solo una versión y lo elimina, el modelo se vuelve inutilizable.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe tener el permiso para ver la vista mdm.viw_SYSTEM_SCHEMA_VERSION y para ejecutar el procedimiento almacenado mds.udpVersionDelete en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para obtener más información, consulte [Seguridad de objetos de base de datos &#40;Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md).  
  
### <a name="to-delete-a-version"></a>Para eliminar una versión  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] para la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Abra la vista mdm.viw_SYSTEM_SCHEMA_VERSION.  
  
3.  Busque la versión del modelo que desea eliminar y copie el valor en el campo **ID** .  
  
4.  Cree una nueva consulta.  
  
5.  Escriba el siguiente texto y reemplace *version_ID* con el valor que ha copiado en el paso 2.  
  
    ```  
    EXEC [mdm].[udpVersionDelete] @Version_ID='version_ID'  
    ```  
  
6.  Ejecuta la consulta.  
  
    > [!NOTE]  
    >  Puede que tenga que esperar unos minutos antes de que la aplicación web refleje el cambio.  
  
## <a name="see-also"></a>Vea también  
 [Versiones &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Copiar una versión &#40;Master Data Services&#41;](../master-data-services/copy-a-version-master-data-services.md)  
  
  
