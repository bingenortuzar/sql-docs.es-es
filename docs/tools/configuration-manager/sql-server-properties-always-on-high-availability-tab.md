---
title: Propiedades de SQL Server (pestaña Alta disponibilidad de AlwaysOn) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: d8630923-a600-4f1c-aca1-027453a3ec82
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 04c73d47f8289e5faf1ae5f5074d5e85b1516a50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023963"
---
# <a name="sql-server-properties-always-on-high-availability-tab"></a>Propiedades de SQL Server (pestaña Alta disponibilidad de AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Use la pestaña **Alta disponibilidad de AlwaysOn** del cuadro de diálogo **Propiedades de SQL Server** del Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar o deshabilitar la característica Grupos de disponibilidad AlwaysOn de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. La habilitación de los Grupos de disponibilidad AlwaysOn es un requisito previo para que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use los grupos de disponibilidad como solución de alta disponibilidad y recuperación ante desastres.  
  
##  <a name="Prerequisites"></a> Requisitos previos  
 Para tener habilitados los Grupos de disponibilidad AlwaysOn, una instancia del servidor debe cumplir los requisitos previos siguientes:  
  
-   La instancia de servidor debe residir en un nodo de clústeres de conmutación por error de Windows Server (WSFC).  
  
-   Para pertenecer al mismo grupo de disponibilidad, las instancias deben estar en el mismo clúster de WSFC. Un grupo de disponibilidad no puede abarcar varios clústeres de WSFC.  
  
-   La instancia del servidor debe ejecutar una edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que admita [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
-   Habilite los Grupos de disponibilidad AlwaysOn para las distintas instancias del servidor de una en una. Después de habilitar los Grupos de disponibilidad AlwaysOn, espere hasta que se haya reiniciado el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de habilitar la instancia del servidor siguiente.  
  
> [!NOTE]  
>  Para más información sobre las características admitidas y sobre los requisitos previos, restricciones y recomendaciones adicionales para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], vea los Libros en pantalla de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
## <a name="dialog-options"></a>Opciones del cuadro de diálogo  
 **Nombre del clúster de conmutación por error de Windows**  
 Muestra el nombre del clúster de WSFC en el que el equipo local es un nodo.  
  
 **Habilitar los grupos de disponibilidad AlwaysOn**  
 Use esta casilla para habilitar o deshabilitar los Grupos de disponibilidad AlwaysOn en esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tal como se indica abajo:  
  
-   Si esta casilla está vacía, los Grupos de disponibilidad AlwaysOn estarán deshabilitados. Para habilitar los Grupos de disponibilidad AlwaysOn, seleccione esta casilla, haga clic en **Aceptar**y reinicie manualmente el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Si esta casilla ya está seleccionada, los Grupos de disponibilidad AlwaysOn ya están habilitados. Para deshabilitar los Grupos de disponibilidad AlwaysOn, desactive la casilla y haga clic en **Aceptar**. Esto hace que se reinicie la instancia del servidor.  
  
    > [!TIP]  
    >  Después de deshabilitar los Grupos de disponibilidad AlwaysOn, debe quitar todas las réplicas de disponibilidad locales de la instancia del servidor. Si quita la última réplica de un grupo de disponibilidad determinado, también debe quitar el grupo.  
  
## <a name="uielement-list"></a>Lista de UIElement  
  
> [!NOTE]  
>  Para más información sobre los pasos que se deben seguir después de deshabilitar los Grupos de disponibilidad AlwaysOn y si quiere saber más sobre cómo crear y configurar grupos de disponibilidad, vea los Libros en pantalla de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
  
