---
title: LEN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/03/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LEN
- LEN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- LEN function
- characters [SQL Server], number of
- number of characters
ms.assetid: fa20fee4-884d-4301-891a-c03e901345ae
author: pmasl
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0b6f470a08c3605f9ea5afa5fff1f7b6cbd17f1b
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653245"
---
# <a name="len-transact-sql"></a>LEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el número de caracteres de la expresión de cadena especificada, excluidos los espacios finales.  
  
> [!NOTE]  
> Para devolver el número de bytes usado para representar una expresión, use la función [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
LEN ( string_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *string_expression*  
 Es la [expression](../../t-sql/language-elements/expressions-transact-sql.md) de cadena que se va a evaluar. *string_expression* puede ser una constante, una variable o una columna de datos binarios o de caracteres.  
  
## <a name="return-types"></a>Tipos devueltos  
 **bigint** si *expression* es de los tipos de datos **varchar(max)** , **nvarchar(max)** o **varbinary(max)** ; en caso contrario, es **int**.  
  
 Si utiliza intercalaciones de SC, el valor entero devuelto cuenta los pares suplentes UTF-16 como un solo carácter. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="remarks"></a>Notas  
LEN no incluye espacios finales. Si esto supone un problema, considere la opción de usar la función [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md), que no recorta la cadena. Si se procesa una cadena unicode, DATALENGTH devolverá un número que tal vez no sea igual al número de caracteres. En este ejemplo se muestra LEN y DATALENGTH con un espacio final.  
  
```sql  
DECLARE @v1 varchar(40),  
    @v2 nvarchar(40);  
SELECT   
@v1 = 'Test of 22 characters ',   
@v2 = 'Test of 22 characters ';  
SELECT LEN(@v1) AS [varchar LEN] , DATALENGTH(@v1) AS [varchar DATALENGTH];  
SELECT LEN(@v2) AS [nvarchar LEN], DATALENGTH(@v2) AS [nvarchar DATALENGTH];  
```  

> [!NOTE]
> Use [LEN](../../t-sql/functions/len-transact-sql.md) para devolver el número de caracteres codificados en una expresión de cadena determinada y [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) para devolver el tamaño en bytes para una expresión de cadena determinada. Estos resultados pueden diferir en función del tipo de datos y del tipo de codificación utilizado en la columna. Para obtener más información sobre las diferencias de almacenamiento entre los distintos tipos de codificación, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).

## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente selecciona el número de caracteres y los datos en `FirstName` para las personas que se encuentran en `Australia`. En este ejemplo se utiliza la base de datos de AdventureWorks.  
  
```sql  
SELECT LEN(FirstName) AS Length, FirstName, LastName   
FROM Sales.vIndividualCustomer  
WHERE CountryRegionName = 'Australia';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En este ejemplo se devuelve el número de caracteres en la columna `FirstName` y los nombres y apellidos de los empleados que se encuentran en `Australia`.  
  
```sql  
USE AdventureWorks2016  
GO  
SELECT DISTINCT LEN(FirstName) AS FNameLength, FirstName, LastName   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.DimGeography AS g   
    ON e.SalesTerritoryKey = g.SalesTerritoryKey   
WHERE EnglishCountryRegionName = 'Australia';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
FNameLength  FirstName  LastName  
-----------  ---------  ---------------  
4            Lynn       Tsoflias
```  
  
## <a name="see-also"></a>Consulte también  
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [CHARINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)   
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
