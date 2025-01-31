---
title: Sys. database_service_objectives (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.service: sql-database
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.topic: conceptual
keywords:
- Grupo elástico
- Grupo elástico, administración
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: fc6c0fc0dbd9ce98d3be2e226e6b2ed3c01cb187
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893297"
---
# <a name="sysdatabase_service_objectives-azure-sql-database"></a>Sys. database_service_objectives (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Devuelve la edición (nivel de servicio), el objetivo de servicio (nivel de precios) y el nombre del grupo elástico, si existe, para una base de datos SQL de Azure o una Azure SQL Data Warehouse. Si inició sesión en la base de datos maestra en un servidor de Azure SQL Database, devuelve información sobre todas las bases de datos. Para Azure SQL Data Warehouse, debe estar conectado a la base de datos maestra.  
  
  
 Para obtener información sobre los precios [, consulte Opciones y rendimiento de SQL Database: Precios de SQL Database y precios de [SQL Data Warehouse.](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)](https://azure.microsoft.com/pricing/details/sql-database/)  
  
 Para cambiar la configuración del servicio, vea [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md) y [alter Database (Azure SQL Data Warehouse)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest).  
  
 La vista sys. database_service_objectives contiene las columnas siguientes.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|database_id|int|IDENTIFICADOR de la base de datos, único dentro de una instancia de Azure SQL Database Server. Se combina con [Sys. Databases de &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|edición|sysname|El nivel de servicio para la base de datos o el almacenamiento de datos: **Básico**, **estándar**, **Premium** o **almacenamiento de datos**.|  
|service_objective|sysname|El plan de tarifa de la base de datos. Si la base de datos está en un grupo elástico, devuelve **ElasticPool**.<br /><br /> En el nivel **básico** , devuelve **Basic**.<br /><br /> Una **sola base de datos en un nivel de servicio estándar** devuelve uno de los siguientes: S0, S1, S2, S3, S4, S6, S7, S9 o S12.<br /><br /> **Una sola base de datos en un nivel Premium** devuelve lo siguiente: P1, P2, P4, P6, P11 o p15.<br /><br /> **SQL Data Warehouse** devuelve DW100 a DW30000c.<br /><br /> Para más información, consulte bases de datos [únicas](/azure/sql-database/sql-database-dtu-resource-limits-single-databases/), [grupos elásticos](/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools/), almacenamientos de [datos](/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu/) .|  
|elastic_pool_name|sysname|Nombre del [Grupo elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) al que pertenece la base de datos. Devuelve **null** si la base de datos es una sola base de datos o una warehoue de datos.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso **dbManager** en la base de datos maestra.  En el nivel de base de datos, el usuario debe ser el creador o el propietario.  
  
## <a name="examples"></a>Ejemplos  
 Este ejemplo se puede ejecutar en la base de datos maestra o en Azure SQL Database bases de datos de usuario. La consulta devuelve el nombre, el servicio y la información de nivel de rendimiento de las bases de datos.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
