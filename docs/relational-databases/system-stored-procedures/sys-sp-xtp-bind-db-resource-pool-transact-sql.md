---
title: Sys.sp_xtp_bind_db_resource_pool (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xtp_bind_db_resource_pool_TSQL
- sp_xtp_bind_db_resource_pool
- sys.sp_xtp_bind_db_resource_pool_TSQL
- sys.sp_xtp_bind_db_resource_pool
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xtp_bind_db_resource_pool
- sys.sp_xtp_bind_db_resource_pool
ms.assetid: c2a78073-626b-4159-996e-1808f6bfb6d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: af0e10f23d376c96fd7be0a75cf713dd76a2c149
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041010"
---
# <a name="sysspxtpbinddbresourcepool-transact-sql"></a>sys.sp_xtp_bind_db_resource_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Enlaza la base de datos de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] indicada para el grupo de recursos de servidor especificado. La base de datos y el grupo de recursos de servidor se deben haber creado antes de ejecutar `sys.sp_xtp_bind_db_resource_pool`.  
  
 Este procedimiento del sistema crea un enlace entre el grupo del regulador de recursos que identificó resource_pool_name y la base de datos que identificó database_name. No se necesita que la base de datos tenga objetos optimizados para memoria en el momento de realizar el enlace. Si no hay objetos optimizados para memoria, no habrá consumo de memoria por parte del grupo de recursos de servidor. Este enlace lo utilizará el regulador de recursos para administrar la memoria que asignan los asignadores de [!INCLUDE[hek_2](../../includes/hek-2-md.md)], tal como se describe a continuación.  
  
 Si ya hay un enlace implementado para una base de datos determinada, el procedimiento devuelve un error.  Una base de datos no podrá en ningún caso tener más de un enlace activo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
sys.sp_xtp_bind_db_resource_pool 'database_name', 'resource_pool_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 database_name  
 Nombre de una base de datos de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] existente habilitada.  
  
 resource_pool_name  
 Nombre de un grupo de recursos de servidor existente.  
  
## <a name="messages"></a>Mensajes  
 Cuando se produce un error, `sp_xtp_bind_db_resource_pool` devuelve uno de estos mensajes.  
  
 **No existe la base de datos**  
 Database_name debe hacer referencia a una base de datos existente. Si no hay bases de datos con el identificador especificado, se devolverá el siguiente mensaje:   
*Id. de base de datos %d no existe.  Use un Id. de base de datos válido para este enlace.*  
  
```  
Msg 911, Level 16, State 18, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Database 'Hekaton_DB213' does not exist. Make sure that the name is entered correctly.  
```  
  
**Base de datos es una base de datos del sistema**  
 Las tablas de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] no se pueden crear en bases de datos del sistema.  Por tanto, no es válido crear un enlace de memoria de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] para tales bases de datos.  Se devuelve el siguiente error:  
*Database_name %s hace referencia a una base de datos del sistema.  Los grupos de recursos solo pueden estar enlazados a una base de datos de usuario.*  
  
```  
Msg 41371, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Binding to a resource pool is not supported for system database 'master'. This operation can only be performed on a user database.  
```  
  
**Grupo de recursos no existe.**  
 El grupo de recursos de servidor que ha identificado resource_pool_name debe haberse creado antes de ejecutar `sp_xtp_bind_db_resource_pool`.  Si no hay un grupo con el identificador especificado, se devolverá el siguiente error:  
*Grupo de recursos %s no existe.  Escriba un nombre de grupo de recursos válido.*  
  
```  
Msg 41370, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Resource pool 'Pool_Hekaton' does not exist or resource governor has not been reconfigured.  
```  
  
**Pool_name se refiere a un grupo de sistema reservado**  
 Los nombres de grupo "INTERNAL" y "DEFAULT" están reservados para los grupos del sistema.  No es válido enlazar explícitamente una base de datos a cualquiera de estos.  Si se especifica un nombre de grupo de servidores del sistema, se devuelve el error siguiente:  
*Grupo de recursos %s es un grupo de recursos del sistema.  Grupos de recursos del sistema no pueden estar enlazados explícitamente a una base de datos mediante este procedimiento.*  
  
```  
Msg 41373, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 51  
Database 'Hekaton_DB' cannot be explicitly bound to the resource pool 'internal'. A database can only be bound only to a user resource pool.  
```  
  
**Base de datos ya está enlazado a otro grupo de recursos**  
 Una base de datos se puede enlazar a solo un grupo de recursos de servidor en todo momento. Los enlaces de la base de datos a grupos de recursos de servidor se deben haber quitado explícitamente antes de que se puedan enlazar a otro grupo. Consulte [sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md).  
*Base de datos %s ya está enlazado al grupo de recursos %s.  Es preciso que quite antes de poder crear un nuevo enlace.*  
  
```  
Msg 41372, Level 16, State 1, Procedure sp_xtp_bind_db_resource_pool_internal, Line 54  
Database 'Hekaton_DB' is currently bound to a resource pool. A database must be unbound before creating a new binding.  
```  
  
 Cuando el proceso se realiza correctamente, `sp_xtp_bind_db_resource_pool` devuelve el siguiente mensaje.  
  
**Enlace correcto**  
 Cuando el proceso es correcto, la función devuelve el siguiente mensaje de operación correcta, que se registra en el registro de errores de SQL  
*Un enlace de recursos se creó correctamente entre el grupo de recursos con Id. %d y de la base de datos con Id. de %d.*  
  
## <a name="examples"></a>Ejemplos  
A.  El siguiente código de ejemplo enlaza la base de datos Hekaton_DB con el grupo de recursos de servidor Pool_Hekaton.  
  
```sql  
sys.sp_xtp_bind_db_resource_pool N'Hekaton_DB', N'Pool_Hekaton'  
```  
 
 El enlace surte efecto la próxima vez que la base de datos pase a estar en línea.  
 
 b. Ejemplo ampliado de ejemplo que incluye algunas comprobaciones básicas anterior.  Ejecute el siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]\:
 
```sql
DECLARE @resourcePool sysname = N'Pool_Hekaton';
DECLARE @database sysname = N'Hekaton_DB';

-- Check whether resource pool exists
IF NOT EXISTS (
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = @resourcePool
    )
BEGIN
    SELECT N'Resource pool "' + @resourcePool + N'" does not exist or resource governor has not been reconfigured.';
END
-- Check whether database is already bound to a resource pool
ELSE IF EXISTS (
    SELECT p.name
    FROM sys.databases d
    JOIN sys.resource_governor_resource_pools p
    ON d.resource_pool_id = p.pool_id
    WHERE d.name = @database
    )
BEGIN
    SELECT N'Database "' + @database + N'" is currently bound to resource pool "' + @resourcePool  + N'". A database must be unbound before creating a new binding.';
END
-- Bind resource pool to database.
ELSE BEGIN
    EXEC sp_xtp_bind_db_resource_pool @database, @resourcePool; 
END 
``` 
  
## <a name="requirements"></a>Requisitos  
  
-   Tanto la base de datos que ha especificado `database_name`, como el grupo de recursos de servidor que ha especificado `resource_pool_name` deben haberse creado antes de enlazarlos.  
  
-   Requiere el permiso CONTROL SERVER.  
  
## <a name="see-also"></a>Vea también  
 [Enlazar una base de datos con tablas con optimización para memoria a un grupo de recursos de servidor](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql.md)  
  
  
