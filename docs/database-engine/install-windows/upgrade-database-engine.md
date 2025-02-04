---
title: Actualizar el motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cff2727815c5cd6cada3d2111e0aada4e722f800
ms.sourcegitcommit: a1ddeabe94cd9555f3afdc210aec5728f0315b14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2019
ms.locfileid: "70122960"
---
# <a name="upgrade-database-engine"></a>Actualizar el motor de base de datos

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
  Con los artículos de esta sección aprenderá a actualizar el motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
1.  [Elija un método de actualización del motor de base de datos](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md). Antes de comenzar una actualización, debe comprender los distintos métodos de actualización. En este artículo se describen los métodos de actualización y los pasos implicados en cada método de actualización.  
  
2.  [Planee y pruebe el plan de actualización del motor de base de datos](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md). Después de revisar los métodos de actualización, está a punto para desarrollar el método de actualización adecuado para su entorno y, después, probar el método de actualización antes de actualizar el entorno existente. En este artículo se describe el desarrollo de un plan de actualización y su prueba.  
  
3.  [Complete la actualización del motor de base de datos](../../database-engine/install-windows/complete-the-database-engine-upgrade.md). Una vez que se haya actualizado el motor de base de datos a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y las bases de datos estén en línea, debe realizar otros pasos, como efectuar una copia de seguridad nueva, actualizar la funcionalidad de las bases de datos para habilitar nuevas características y volver a rellenar los catálogos de texto completo. En este artículo se describen estos pasos.  
  
4.  Actualice el [nivel de compatibilidad de la base de datos](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades) (**se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]). Uno de los pasos que debe realizar cuando las bases de datos estén en línea en la nueva versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] puede ser actualizar el modo de funcionalidad de estas para habilitar las nuevas características cambiando el nivel de compatibilidad de la base de datos. Esto se puede hacer manualmente a través del Asistente para optimización de consultas. 

    - [Cambie el nivel de compatibilidad de la base de datos y use el Almacén de consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md). Después de cambiar manualmente el nivel de compatibilidad de la base de datos, use el Almacén de consultas para supervisar el rendimiento e identificar posibles regresiones. En este artículo se explica el proceso recomendado y se proporciona un flujo de trabajo recomendado.  

    - [Cambie el modo de compatibilidad de la base de datos con el Asistente para consultas](../../relational-databases/performance/upgrade-dbcompat-using-qta.md). Como alternativa a un cambio manual, use el **Asistente para optimización de consultas (QTA)** , que le guiará a través del proceso recomendado para cambiar el nivel de compatibilidad de la base de datos. En este artículo se explica este proceso y se proporcionan instrucciones sobre el flujo de trabajo de QTA.  

    Para obtener más información sobre las nuevas características y los comportamientos mejorados disponibles después de cambiar el nivel de compatibilidad de la base de datos, vea [Niveles de compatibilidad y procedimientos almacenados](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-stored-procedures).

5.  [Aproveche las nuevas características de SQL Server](https://www.microsoft.com/sql-server/sql-server-2017). Finalmente, después de haber completado los pasos anteriores, ya está a punto para sacar partido de las nuevas mejoras del motor de base de datos específicas. En este artículo se sugieren algunas de estas mejoras y se ofrecen vínculos para ampliar información.  
  
  
