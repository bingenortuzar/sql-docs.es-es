---
title: El servicio servicios de acceso a la integración | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- viewing packages while running
- displaying packacges while running
- security [Integration Services], running packages
- packages [Integration Services], security
- current packages running
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 1088aafc-14c5-4e7d-9930-606a24c3049b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e3654be0afe51be6566a09897a2656dd53c77696
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062236"
---
# <a name="access-to-the-integration-services-service"></a>Acceso al servicio Integration Services
  Los niveles de protección de paquetes pueden limitar quién puede editar y ejecutar un paquete. Es necesaria protección adicional para limitar quién puede ver la lista de paquetes actualmente en ejecución en un servidor y quién puede detener dicha ejecución en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] utiliza el servicio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para mostrar los paquetes que se están ejecutando. Los miembros del grupo Administradores de Windows pueden ver y detener todos los paquetes en ejecución. Los usuarios que no sean miembros del grupo Administradores solo pueden ver y detener los paquetes que han iniciado ellos mismos.  
  
 Es importante restringir el acceso a los equipos que ejecutan un servicio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , especialmente un servicio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que puede mostrar carpetas remotas. Cualquier usuario autenticado puede solicitar la enumeración de los paquetes. Incluso si la no servicio no encontró el servicio, el servicio enumera las carpetas. Estos nombres de carpeta pueden ser útiles para un usuario malintencionado. Si un administrador configura el servicio para que enumere las carpetas en un equipo remoto, los usuarios también podrán ver los nombres de las carpetas que normalmente no podrían ver.  
  
  
