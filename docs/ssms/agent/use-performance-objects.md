---
title: Usar objetos de rendimiento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 73e36b4d0ee10d42ec7774e20693d217ee274344
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260909"
---
# <a name="use-performance-objects"></a>Usar objetos de rendimiento
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente incluye objetos y contadores de rendimiento para supervisar el rendimiento del servicio. Estos objetos de rendimiento le permiten utilizar el Monitor de rendimiento, una herramienta de Windows, para identificar las actividades que realiza el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en segundo plano. Por ejemplo, puede identificar cuántos trabajos activos ejecuta actualmente el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para identificar los trabajos bloqueados.  
  
Hay objetos y contadores de rendimiento del servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada en el equipo. La denominación que adoptan los objetos de rendimiento depende de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que representa cada uno de ellos.  
  
La tabla siguiente muestra cómo se denominan los objetos de rendimiento del servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Tipo de instancia|Nombre del objeto|  
|-----------------|---------------|  
|Valor predeterminado|**SQLAgent:** _objeto_:_contador_|  
|Con nombre|**SQLAgent$**<br /> **&#42;nombre_instancia&#42; :** _objeto_:_contador_|  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye los siguientes objetos de rendimiento para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Nombre del objeto|Descripción|  
|---------------|---------------|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|Información de rendimiento acerca de trabajos que se han iniciado, tasas de éxito y estado actual|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|Información de estado acerca de pasos de trabajos|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|Información acerca del número de alertas y notificaciones|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|Información general de rendimiento|  
  
## <a name="see-also"></a>Consulte también  
[Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
[Cómo: Iniciar el Monitor de sistema (Windows)](https://msdn.microsoft.com/5e51bb79-5737-470b-9c47-fac330c001c5)  
  
