---
title: SET QUOTED_IDENTIFIER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- QUOTED_IDENTIFIER_TSQL
- SET_QUOTED_IDENTIFIER_TSQL
- SET QUOTED_IDENTIFIER
- QUOTED_IDENTIFIER
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- identifiers [SQL Server], delimited
- QUOTED_IDENTIFIER option
- quoted identifiers
- ISO delimited identifiers rules
- SET QUOTED_IDENTIFIER statement
ms.assetid: 10f66b71-9241-4a3a-9292-455ae7252565
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b080efcb7af0f813f798c7f572f464d4718fdd75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008896"
---
# <a name="set-quotedidentifier-transact-sql"></a>SET QUOTED_IDENTIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Hace que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siga las reglas de ISO en cuanto a comillas delimitadoras de identificadores y cadenas literales se refiere. Los identificadores delimitados con comillas dobles pueden ser palabras clave reservadas de [!INCLUDE[tsql](../../includes/tsql-md.md)] o pueden contener caracteres normalmente no admitidos por las reglas sintácticas para identificadores de [!INCLUDE[tsql](../../includes/tsql-md.md)].

![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxis

```
-- Syntax for SQL Server and Azure SQL Database

SET QUOTED_IDENTIFIER { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET QUOTED_IDENTIFIER ON
```

## <a name="remarks"></a>Notas

Cuando SET QUOTED_IDENTIFIER es ON, los identificadores pueden delimitarse con comillas dobles y los literales deben delimitarse con comillas simples. Cuando SET QUOTED_IDENTIFIER es OFF, los identificadores no pueden entrecomillarse y deben seguir todas las reglas para identificadores de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md). Los literales se pueden delimitar con comillas simples o dobles.

Cuando SET QUOTED_IDENTIFIER es ON (valor predeterminado), todas las cadenas delimitadas con comillas dobles se interpretan como identificadores de objeto. Por ello, los identificadores entrecomillados no tienen que seguir las reglas para identificadores de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Pueden ser palabras clave reservadas e incluir caracteres que normalmente no se admiten en los identificadores de [!INCLUDE[tsql](../../includes/tsql-md.md)]. No se pueden utilizar comillas dobles para delimitar expresiones de cadenas literales; para delimitar las cadenas literales se deberán utilizar comillas simples. Si una comilla simple ( **'** ) forma parte de la cadena literal, se puede representar mediante dos comillas simples ( **"** ). SET QUOTED_IDENTIFIER debe ser ON cuando se utilicen palabras reservadas como nombres de objetos de la base de datos.

Cuando SET QUOTED_IDENTIFIER es OFF, las cadenas literales de las expresiones se pueden delimitar con comillas simples o dobles. Si una cadena literal se delimita con comillas dobles, podrá contener comillas simples incrustadas, como, por ejemplo, apóstrofos.

SET QUOTED_IDENTIFIER debe ser ON al crear o cambiar índices en columnas calculadas o vistas indizadas. Si SET QUOTED_IDENTIFIER es OFF, las instrucciones CREATE, UPDATE, INSERT y DELETE provocarán errores en tablas con índices en columnas calculadas o vistas indizadas. Para más información sobre las configuraciones de las opciones SET necesarias con vistas indizadas e índices en columnas calculadas, vea el apartado "Consideraciones al utilizar las instrucciones SET" en [Instrucciones SET](../../t-sql/statements/set-statements-transact-sql.md).

SET QUOTED_IDENTIFIER debe ser ON cuando se crea un índice filtrado.

SET QUOTED_IDENTIFIER debe ser ON cuando se invocan métodos del tipo de datos XML.

El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establecen automáticamente QUOTED_IDENTIFIER en ON al conectarse. Esta opción se puede configurar en los orígenes de datos ODBC, en los atributos de conexión ODBC o en las propiedades de conexión OLE DB. El valor predeterminado de SET QUOTED_IDENTIFIER es OFF para las conexiones desde aplicaciones DB-Library.

Cuando se crea una tabla, la opción QUOTED IDENTIFIER siempre se almacena como ON en los metadatos de la tabla, aunque se haya establecido en OFF al crear la tabla.

Cuando se crea un procedimiento almacenado, los valores de SET QUOTED_IDENTIFIER y SET ANSI_NULLS se capturan y se utilizan en las siguientes llamadas a ese procedimiento almacenado.

Cuando se ejecuta dentro de un procedimiento almacenado, la opción SET QUOTED_IDENTIFIER no cambia.

Cuando SET ANSI_DEFAULTS es ON, se habilita SET QUOTED_IDENTIFIER.

SET QUOTED_IDENTIFIER también se corresponde con el valor QUOTED_IDENTIFIER de ALTER DATABASE. Para más información sobre la configuración de bases de datos, vea [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).

SET QUOTED_IDENTIFIER tiene efecto en tiempo de análisis y solo afecta al análisis, no a la ejecución de la consulta.

Para un lote ad hoc de nivel superior, el análisis empieza usando la opción actual de la sesión para QUOTED_IDENTIFIER. Mientras se analiza el lote, cualquier aparición de SET QUOTED_IDENTIFIER cambiará el comportamiento del análisis a partir de ese punto y guardará ese valor para la sesión. Después de analizarse y ejecutarse el lote, el valor QUOTED_IDENTIFER de la sesión se establecerá según la última aparición de SET QUOTED_IDENTIFIER en el lote.

El SQL estático en un procedimiento almacenado se analiza mediante el valor QUOTED_IDENTIFIER que esté en vigor para el lote que creó o modificó el procedimiento almacenado. SET QUOTED_IDENTIFIER no tiene ningún efecto cuando aparece en el cuerpo de un procedimiento almacenado como SQL estático.

Para un lote anidado mediante sp_executesql o exec(), el análisis empieza usando el valor QUOTED_IDENTIFIER de la sesión. Si el lote anidado está dentro de un procedimiento almacenado, el análisis empieza usando el valor QUOTED_IDENTIFIER del procedimiento almacenado. Mientras se analiza el lote anidado, cualquier aparición de SET QUOTED_IDENTIFIER cambiará el comportamiento del análisis a partir de ese punto, pero no se actualizará el valor QUOTED_IDENTIFIER de la sesión.

La opción QUOTED_IDENTIFIER no afecta al uso de los corchetes **[** and **]** para delimitar identificadores.

Para ver la configuración actual de este valor, ejecute la consulta siguiente.

```sql
DECLARE @QUOTED_IDENTIFIER VARCHAR(3) = 'OFF';
IF ( (256 & @@OPTIONS) = 256 ) SET @QUOTED_IDENTIFIER = 'ON';
SELECT @QUOTED_IDENTIFIER AS QUOTED_IDENTIFIER;

```

## <a name="permissions"></a>Permisos

Debe pertenecer al rol public.

## <a name="examples"></a>Ejemplos

### <a name="a-using-the-quoted-identifier-setting-and-reserved-word-object-names"></a>A. Utilizar la opción de identificador entre comillas y nombres de objeto con palabras reservadas

En este ejemplo se muestra que, para crear y utilizar objetos cuyos nombres contienen palabras clave reservadas, `SET QUOTED_IDENTIFIER` debe ser `ON` y las palabras clave reservadas de los nombres de tabla se deben indicar entre comillas dobles.

```sql
SET QUOTED_IDENTIFIER OFF
GO
-- An attempt to create a table with a reserved keyword as a name
-- should fail.
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);
GO

SET QUOTED_IDENTIFIER ON;
GO

-- Will succeed.
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);
GO

SELECT "identity","order"
FROM "select"
ORDER BY "order";
GO

DROP TABLE "SELECT";
GO

SET QUOTED_IDENTIFIER OFF;
GO
```

### <a name="b-using-the-quoted-identifier-setting-with-single-and-double-quotation-marks"></a>B. Utilizar la opción de identificador entre comillas simples y dobles

 En este ejemplo se muestra el uso de las comillas simples y dobles en las expresiones de cadena con `SET QUOTED_IDENTIFIER` establecido en `ON` y `OFF`.

```sql
SET QUOTED_IDENTIFIER OFF;
GO
USE AdventureWorks2012;
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES
    WHERE TABLE_NAME = 'Test')
    DROP TABLE dbo.Test;
GO
USE AdventureWorks2012;
CREATE TABLE dbo.Test (ID INT, String VARCHAR(30)) ;
GO

-- Literal strings can be in single or double quotation marks.
INSERT INTO dbo.Test VALUES (1, "'Text in single quotes'");
INSERT INTO dbo.Test VALUES (2, '''Text in single quotes''');
INSERT INTO dbo.Test VALUES (3, 'Text with 2 '''' single quotes');
INSERT INTO dbo.Test VALUES (4, '"Text in double quotes"');
INSERT INTO dbo.Test VALUES (5, """Text in double quotes""");
INSERT INTO dbo.Test VALUES (6, "Text with 2 """" double quotes");
GO

SET QUOTED_IDENTIFIER ON;
GO

-- Strings inside double quotation marks are now treated
-- as object names, so they cannot be used for literals.
INSERT INTO dbo."Test" VALUES (7, 'Text with a single '' quote');
GO

-- Object identifiers do not have to be in double quotation marks
-- if they are not reserved keywords.
SELECT ID, String
FROM dbo.Test;
GO

DROP TABLE dbo.Test;
GO

SET QUOTED_IDENTIFIER OFF;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
 ID          String
 ----------- ------------------------------
 1           'Text in single quotes'
 2           'Text in single quotes'
 3           Text with 2 '' single quotes
 4           "Text in double quotes"
 5           "Text in double quotes"
 6           Text with 2 "" double quotes
 7           Text with a single ' quote
 ```

## <a name="see-also"></a>Consulte también

- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?view=sql-server-2017)
- [CREATE DEFAULT](../../t-sql/statements/create-default-transact-sql.md)
- [CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)
- [CREATE RULE](../../t-sql/statements/create-rule-transact-sql.md)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)
- [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md)
- [CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)
- [Tipos de datos](../../t-sql/data-types/data-types-transact-sql.md)
- [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md)
- [SELECT](../../t-sql/queries/select-transact-sql.md)
- [SET, instrucciones](../../t-sql/statements/set-statements-transact-sql.md)
- [SET ANSI_DEFAULTS](../../t-sql/statements/set-ansi-defaults-transact-sql.md)
- [sp_rename](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
