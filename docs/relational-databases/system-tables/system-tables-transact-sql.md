---
title: Tablas del sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server]
- tables [SQL Server], system tables
- information retrieval [SQL Server]
- status information [SQL Server], system tables
- system information [SQL Server]
- system tables [SQL Server]
- system tables [SQL Server], about system tables
- system tables [SQL Server], retrieving information from
- retrieving system table information
ms.assetid: 56b8ad51-930c-4e5c-8d99-8c939d5b70ac
author: stevestein
ms.author: sstein
ms.openlocfilehash: 292b6cdce6b2f13445e50f79c956f07eb8d33de7
ms.sourcegitcommit: 676458a9535198bff4c483d67c7995d727ca4a55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69903597"
---
# <a name="system-tables-transact-sql"></a>Tablas del sistema (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En los temas de esta sección se describen las tablas del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Ningún usuario debe modificar directamente las tablas del sistema. Por ejemplo, no intente modificar tablas del sistema con las instrucciones DELETE, UPDATE o INSERT, ni con desencadenadores definidos por el usuario.  
  
 Se permite hacer referencia a columnas documentadas en las tablas del sistema. Sin embargo, muchas de las columnas de las tablas del sistema no están documentadas. No deben escribirse aplicaciones que consulten directamente columnas no documentadas. En su lugar, las aplicaciones deben usar cualquiera de los componentes siguientes para recuperar la información almacenada en las tablas del sistema:  
  
-   Procedimientos almacenados del sistema  
  
-   Instrucciones y funciones [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Objetos de administración (SMO)  
  
-   Replication Management Objects (RMO)  
  
-   Funciones de catálogo de API de base de datos  
  
 Estos componentes conforman una API publicado para obtener información del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[msCoName](../../includes/msconame-md.md)] mantiene la compatibilidad de estos componentes entre versiones. El formato de las tablas del sistema depende de la arquitectura interna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y puede cambiar de una versión a otra. Por tanto, puede ser necesario modificar las aplicaciones que tienen acceso directo a columnas no documentadas de las tablas del sistema para que puedan tener acceso a una versión posterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas relacionados con las tablas del sistema se organizan según las siguientes áreas de características:  
  
|||  
|-|-|  
|[Tablas &#40;de copia de seguridad y restauración de TRANSACT-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)|[Tablas de trasvase de registros &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)|  
|[Tablas &#40;de captura de datos modificados de TRANSACT-SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)|[Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)|  
|[Tablas &#40;de planes de mantenimiento de bases de datos TRANSACT-SQL&#41;](../../relational-databases/system-tables/database-maintenance-plan-tables-transact-sql.md)|[Tablas &#40;de Agente SQL Server TRANSACT-SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)|  
|[SQL Server tablas &#40;de eventos extendidos de TRANSACT-SQL&#41;](../../relational-databases/extended-events/xevents-references-system-objects.md#system-tables)|[Sys. sysoledbusers &#40;de TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysoledbusers-transact-sql.md)|  
|[Tablas &#40;de Integration Services TRANSACT-SQL&#41;](../../relational-databases/system-tables/integration-services-tables-transact-sql.md)|[Transact &#40;-SQL de systranschemas&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)|  
  
## <a name="see-also"></a>Vea también  
 [Vistas &#40;de compatibilidad de TRANSACT-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
