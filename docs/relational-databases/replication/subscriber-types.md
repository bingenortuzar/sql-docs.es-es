---
title: Tipos de suscriptor | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 1958e6f85dfe6451cca24926a4c0ea8afedfe3a5
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768394"
---
# <a name="subscriber-types"></a>Tipos de suscriptor
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La replicación de mezcla le permite especificar los tipos de suscriptor compatibles con una publicación. Si selecciona Tipos de suscriptor, podrá establecer el *nivel de compatibilidad de la publicación*, que determina las características que puede usar una publicación.  
  
 Una vez creada una instantánea de publicación, se puede aumentar (restringir) el nivel de compatibilidad de la publicación en la página **General** del cuadro de diálogo **Propiedades de la publicación** ; no se puede reducir el nivel de compatibilidad.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>Opciones  
 Seleccione los tipos de suscriptor compatibles con la publicación.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 La publicación podrá usar todas las características.  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 La publicación necesita que los archivos de instantáneas tengan un formato de caracteres (el agente de instantáneas lo controlará automáticamente). [!INCLUDE[ssEW](../../includes/ssew-md.md)] también presenta varias restricciones no relacionadas con el nivel de compatibilidad.  
  
 Si selecciona esta opción, se habilitará la opción de sincronización web para la publicación. Para obtener más información acerca de la sincronización web, vea [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
## <a name="see-also"></a>Consulte también  
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
  
  
