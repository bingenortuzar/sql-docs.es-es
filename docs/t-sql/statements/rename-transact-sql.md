---
title: RENAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 0907cfd9-33a6-4fa6-91da-7d6679fee878
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 624131beece632cffd13bde3d6ad378f67b3a340
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141274"
---
# <a name="rename-transact-sql"></a>RENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Cambia el nombre de una tabla creada por el usuario en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Cambia el nombre de una tabla o base de datos creada por el usuario en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].

> [!NOTE]
> Para cambiar el nombre de una base de datos en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], use [ALTER DATABASE (Azure SQL Data Warehouse](alter-database-transact-sql.md?view=aps-pdw-2016-au7). Para cambiar el nombre de una base de datos en Azure SQL Database, use la instrucción [ALTER DATABASE (Azure SQL Database)](alter-database-transact-sql.md?view=azuresqldb-mi-current). Para cambiar el nombre de una base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use el procedimiento almacenado [sp_renamedb](../../relational-databases/system-stored-procedures/sp-renamedb-transact-sql.md).

## <a name="syntax"></a>Sintaxis

```
-- Syntax for Azure SQL Data Warehouse

-- Rename a table.
RENAME OBJECT [::] [ [ database_name . [schema_name ] ] . ] | [schema_name . ] ] table_name TO new_table_name
[;]

```

```
-- Syntax for Analytics Platform System

-- Rename a table
RENAME OBJECT [::] [ [ database_name . [ schema_name ] . ] | [ schema_name . ] ] table_name TO new_table_name
[;]

-- Rename a database
RENAME DATABASE [::] database_name TO new_database_name
[;]
```

## <a name="arguments"></a>Argumentos

RENAME OBJECT [::] [ [*database_name* . [ *schema_name* ] . ] | [ *schema_name* . ] ]*table_name* TO *new_table_name*
**APPLIES TO:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

Sirve para cambiar el nombre de una tabla definida por el usuario. Especifique la tabla cuyo nombre va a cambiar por un nombre de una, dos o tres partes. Especifique la nueva tabla *new_table_name* como un nombre de una sola parte.

RENAME DATABASE [::] [ *database_name* TO *new_database_name*
**APPLIES TO:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

Sirve para cambiar el nombre de una base de datos definida por el usuario de *database_name* a *new_database_name*. El nombre de una base de datos no se puede cambiar a ninguno de los siguientes nombres de base de datos reservados de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]:

- maestra
- model
- msdb
- tempdb
- pdwtempdb1
- pdwtempdb2
- DWConfiguration
- DWDiagnostics
- DWQueue

## <a name="permissions"></a>Permisos

Para ejecutar este comando, necesita el permiso siguiente:

- Permiso **ALTER** en la tabla.

## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones

### <a name="cannot-rename-an-external-table-indexes-or-views"></a>No se puede cambiar el nombre de tablas externas, índices ni vistas

El nombre de tablas externas, índices o vistas no se puede cambiar. En lugar de cambiarlo, puede quitar la tabla externa, índice o vista en cuestión y, luego, volver a crearlo con el nuevo nombre.

### <a name="cannot-rename-a-table-in-use"></a>No se puede cambiar el nombre de una tabla en uso

No se puede cambiar el nombre una tabla o una base de datos mientras estas están en uso. Cambiar el nombre de una tabla requiere un bloqueo exclusivo en dicha tabla. Si la tabla está en uso, puede que tenga que finalizar las sesiones que la estén usando. Para ello, puede usar el comando KILL. Use KILL con precaución, ya que cuando una sesión se finaliza, se revertirán todos los trabajos que no estén confirmados. Las sesiones en SQL Data Warehouse llevan el prefijo "SID". Incluya "SID" y el número de sesión al invocar el comando KILL. En este ejemplo se muestra una lista de sesiones activas o inactivas y, luego, finaliza la sesión "SID1234".

### <a name="views-are-not-updated"></a>Las vistas no se actualizan

Al cambiar el nombre de una base de datos, todas las vistas que usan el nombre de la base de datos anterior dejarán de ser válidas. Este comportamiento se produce con las vistas tanto dentro como fuera de la base de datos. Por ejemplo, si se cambia el nombre de la base de datos Sales, una vista que contenga `SELECT * FROM Sales.dbo.table1` dejará de ser válida. Para resolver este problema, puede abstenerse de usar nombres de tres partes en las vistas, o bien actualizar las vistas para que hagan referencia al nombre de la nueva base de datos.

Al cambiar el nombre de una tabla, las vistas no se actualizan para que hagan referencia el nuevo nombre de tabla. Cada vista (ya sea dentro o fuera de la base de datos) que haga referencia al nombre de tabla anterior dejará de ser válida. Para resolver este problema, puede actualizar cada vista para que haga referencia al nombre de la nueva tabla.

## <a name="locking"></a>Bloqueo

Al cambiar el nombre de una tabla, se efectúa un bloqueo compartido en el objeto DATABASE, un bloqueo compartido en el objeto SCHEMA y un bloqueo exclusivo en la tabla.

## <a name="examples"></a>Ejemplos

### <a name="a-rename-a-database"></a>A. Cambiar el nombre de una base de datos

**SE APLICA A:** [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] solo

En este ejemplo se cambia el nombre de la base de datos definida por el usuario de AdWorks a AdWorks2.

```sql
-- Rename the user defined database AdWorks
RENAME DATABASE AdWorks to AdWorks2;

```

 Al cambiar el nombre de una tabla, se actualizan todos los objetos y propiedades asociados a esa tabla para que hagan referencia al nombre de la nueva tabla. Así, por ejemplo, se actualizan las definiciones, índices, restricciones y permisos de la de tabla. Las vistas no se actualizan.

### <a name="b-rename-a-table"></a>B. Cambiar de nombre una tabla

**SE APLICA A:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

En este ejemplo se cambia el nombre de la tabla Customer a Customer1.

```sql
-- Rename the customer table
RENAME OBJECT Customer TO Customer1;

RENAME OBJECT mydb.dbo.Customer TO Customer1;
```

Al cambiar el nombre de una tabla, se actualizan todos los objetos y propiedades asociados a esa tabla para que hagan referencia al nombre de la nueva tabla. Así, por ejemplo, se actualizan las definiciones, índices, restricciones y permisos de la de tabla. Las vistas no se actualizan.

### <a name="c-move-a-table-to-a-different-schema"></a>C. Mover una tabla a otro esquema

**SE APLICA A:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

Si trata de mover el objeto a otro esquema, use [ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md). Por ejemplo, con la siguiente instrucción se mueve el elemento de tabla desde el esquema product al esquema dbo.

```sql
ALTER SCHEMA dbo TRANSFER OBJECT::product.item;
```

### <a name="d-terminate-sessions-before-renaming-a-table"></a>D. Terminar las sesiones antes de cambiar el nombre de una tabla

**SE APLICA A:** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

Es importante recordar que no se puede cambiar el nombre una tabla mientras está en uso. Cambiar el nombre de una tabla requiere un bloqueo exclusivo en dicha tabla. Si la tabla está en uso, puede que tenga que finalizar la sesión que la esté usando. Para ello, puede usar el comando KILL. Use KILL con precaución, ya que cuando una sesión se finaliza, se revertirán todos los trabajos que no estén confirmados. Las sesiones en SQL Data Warehouse llevan el prefijo "SID". Cuando invoque el comando KILL, deberá incluir "SID", así como el número de la sesión. En este ejemplo se muestra una lista de sesiones activas o inactivas y, luego, finaliza la sesión "SID1234".

```sql
-- View a list of the current sessions
SELECT session_id, login_name, status
FROM sys.dm_pdw_exec_sessions
WHERE status='Active' OR status='Idle';

-- Terminate a session using the session_id.
KILL 'SID1234';
```