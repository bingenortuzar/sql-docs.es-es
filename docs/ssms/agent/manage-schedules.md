---
title: Administrar programaciones | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.manageschedules.f1
ms.assetid: f56c0736-dccc-41d2-afcf-71344aff143a
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d193c516566635bae1cfba0d691f823b2cba5d31
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68257822"
---
# <a name="manage-schedules"></a>Administrar programaciones
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Le permite ver y cambiar propiedades para la programación del trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
**Programaciones disponibles**  
Muestra las programaciones disponibles para este usuario. Tenga en cuenta que un trabajo y una programación deben tener el mismo propietario. Por lo tanto, esta lista solo incluye programaciones que pertenecen al propietario del trabajo.  
  
**Nombre**  
Muestra el nombre de la programación.  
  
**Enabled**  
Seleccione esta opción para habilitar la programación.  
  
**Descripción**  
Describe las condiciones bajo las cuales la programación ejecuta el trabajo.  
  
**Trabajos en programación**  
Muestra los números de los trabajos adjuntados a la programación. Haga clic en un número para ver las propiedades del trabajo.  
  
**Nueva**  
Haga clic en este botón para crear una programación nueva.  
  
**Eliminar**  
Haga clic en este botón para eliminar la programación seleccionada.  
  
**Propiedades**  
Haga clic en este botón para cambiar las propiedades de la programación seleccionada.  
  
## <a name="see-also"></a>Consulte también  
[Crear y adjuntar programaciones a trabajos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
  
