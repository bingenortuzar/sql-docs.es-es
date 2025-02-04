---
title: SET FMTONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FMTONLY_TSQL
- FMTONLY
- SET FMTONLY
- SET_FMTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server], only metadata returned
- SET FMTONLY statement
- FMTONLY option
ms.assetid: 02a1d9ac-2e58-433c-9a07-2c5a4a2214e1
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d150082120cde1b09d3437a27b2345b036daf8b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929023"
---
# <a name="set-fmtonly-transact-sql"></a>SET FMTONLY (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss-all-md](../../includes/tsql-appliesto-ss-all-md.md)]

  Devuelve solo metadatos al cliente. Se puede usar para probar el formato de la respuesta sin ejecutar realmente la consulta.  

> [!NOTE]
> No utilice esta característica. Esta característica se ha reemplazado por los siguientes elementos:
>
> - [sp_describe_first_result_set (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)
> - [sp_describe_undeclared_parameters (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)
> - [sys.dm_exec_describe_first_result_set (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)
> - [sys.dm_exec_describe_first_result_set_for_object (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SET FMTONLY { ON | OFF }   
```  

## <a name="remarks"></a>Notas

Cuando `FMTONLY` se establece en `ON`, se devuelve un conjunto de filas con los nombres de columna, pero sin ninguna fila de datos.

`SET FMTONLY ON` no tiene ningún efecto cuando el lote de Transact-SQL se analiza. El efecto se produce en el tiempo de ejecución de la ejecución.

El valor predeterminado es `OFF`.

## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol public.  

## <a name="examples"></a>Ejemplos

En el siguiente ejemplo de código de Transact-SQL, `FMTONLY` se establece en `ON`. Esta configuración hace que SQL Server devuelva únicamente información de metadatos relativa a las columnas seleccionadas. En concreto, devuelve los nombres de columna. No se devuelve ninguna fila de datos.

En el ejemplo, la ejecución de prueba del procedimiento almacenado `prc_gm29` devuelve lo siguiente:

- Varios conjuntos de filas.
- Columnas de varias tablas, en una de sus instrucciones `SELECT`.

<!--
Issue 2246 inspired this code example, and the replacement of the two pre-existing examples. 2019/June/03, GM.
-->

```sql
go
SET NoCount ON;

go
DROP PROCEDURE IF EXISTS prc_gm29;

DROP Table IF EXISTS #tabTemp41;
DROP Table IF EXISTS #tabTemp42;
go

CREATE TABLE #tabTemp41
(
   KeyInt41        int           not null,
   Name41          nvarchar(16)  not null,
   TargetDateTime  datetime      not null  default GetDate()
);

CREATE TABLE #tabTemp42
(
   KeyInt42 int          not null,   -- JOIN-able to KeyInt41.
   Name42   nvarchar(16) not null
);
go

INSERT into #tabTemp41 (KeyInt41, Name41) values (10, 't41-c');
INSERT into #tabTemp42 (KeyInt42, Name42) values (10, 't42-p');
go

CREATE PROCEDURE prc_gm29
AS
begin
SELECT * from #tabTemp41;
SELECT * from #tabTemp42;

SELECT t41.KeyInt41, t41.TargetDateTime, t41.Name41, t42.Name42
   from
                 #tabTemp41 as t41
      INNER JOIN #tabTemp42 as t42 on t42.KeyInt42 = t41.KeyInt41
end;
go

SET DATEFORMAT mdy;

SET FMTONLY ON;
EXECUTE prc_gm29;   -- Returns multiple tables.
SET FMTONLY OFF;
go
DROP PROCEDURE IF EXISTS prc_gm29;

DROP Table IF EXISTS #tabTemp41;
DROP Table IF EXISTS #tabTemp42;
go

/****  Actual Output:
[C:\JunkM\]
>> osql.exe -S myazuresqldb.database.windows.net -U somebody -P secret -d MyDatabase -i C:\JunkM\Issue-2246-a.SQL 

 KeyInt41    Name41           TargetDateTime
 ----------- ---------------- -----------------------

 KeyInt42    Name42
 ----------- ----------------

 KeyInt41    TargetDateTime          Name41           Name42
 ----------- ----------------------- ---------------- ----------------


[C:\JunkM\]
>>
****/
```

## <a name="see-also"></a>Consulte también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

