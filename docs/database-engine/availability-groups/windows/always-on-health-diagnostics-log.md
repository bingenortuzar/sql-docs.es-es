---
title: Registros de diagnóstico de mantenimiento de la DLL del recurso de SQL Server para grupos de disponibilidad
description: Se describe cómo la DLL del recurso de SQL Server supervisa el estado del grupo de disponibilidad Always On.
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: c1862d8a-5f82-4647-a280-3e588b82a6dc
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a4ff7c777add4fa2228fb6525d24f172533a609
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014712"
---
# <a name="sql-server-resource-dll-health-diagnostic-logs-for-availability-groups"></a>Registros de diagnóstico de mantenimiento de la DLL del recurso de SQL Server para grupos de disponibilidad
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para supervisar el estado de la réplica de disponibilidad principal, la DLL del recurso de SQL Server ejecutada por el clúster de clústeres de conmutación por error de Windows Server (WSFC) usa un procedimiento almacenado de la instancia de SQL Server denominado [sp_server_diagnostics](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md).  
  
 La DLL del recurso de SQL Server mantiene una conexión abierta dedicada con la instancia de SQL Server a través de la que la instancia de SQL Server envía periódicamente diagnósticos de estado detallados a la DLL del recurso de SQL Server. Los diagnósticos de estado, junto con la directiva de conmutación por error configurada en el recurso de grupo de disponibilidad del clúster (la propiedad FailoverConditionLevel), son usados por el clúster para determinar si se debe reiniciar o conmutar por error el recurso de grupo de disponibilidad. Este procedimiento almacenado es la instancia de "latido" de SQL Server 2012 y superior para el clúster WSFC, que es más granular y confiable que en SQL Server 2008 R2 o anterior, donde una conexión periódica a la instancia se establece con la consulta `SELECT @@SERVERNAME`. Luego puede controlar las condiciones que desencadenan las conmutaciones por error al establecer la propiedad FailureConditonLevel del grupo de disponibilidad.  
  
 **Usar los registros de diagnóstico del clúster de conmutación por error de SQL Server**
 
 Todos los diagnósticos de estado que recibe la DLL del recurso de SQL Server desde sp_server_diagnostics se guardan automáticamente en el directorio Log predeterminado de la instancia de SQL Server (%PROGRAMFILES%\Microsoft SQL Server\MSSQL11. MSSQLSERVER\MSSQL\Log). Estos registros se conocen como registros SQLDIAG y se guardan en el formato de archivo XEL (eventos extendidos). Estos archivos del directorio Log de SQL Server tienen el formato siguiente: \<NOMBRE_DE_HOST>_\<NOMBRE_DE_INSTANCIA>_SQLDIAG_X_XXXXXXXXX.xel. Al examinar los registros SQLDIAG, es posible determinar la causa raíz de un error o un evento de conmutación por error del recurso de grupo de disponibilidad.  
  
 Para ver un registro SQLDIAG, arrastre el archivo .xel a SQL Server Management Studio.  
  
  
