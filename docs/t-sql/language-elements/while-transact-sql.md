---
title: WHILE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WHILE_TSQL
- WHILE
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], repeated executions
- statement blocks [SQL Server]
- repeated statement executions
- nested WHILE loops
- WHILE keyword
ms.assetid: 52dd29ab-25d7-4fd3-a960-ac55c30c9ea9
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 16ae636e92d109ea8bc9f9ddd67f70a1657cb564
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388445"
---
# <a name="while-transact-sql"></a>WHILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]


  Establece una condición para la ejecución repetida de una instrucción o bloque de instrucciones SQL. Las instrucciones se ejecutan repetidamente siempre que la condición especificada sea verdadera. Se puede controlar la ejecución de instrucciones en el bucle WHILE con las palabras clave BREAK y CONTINUE.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
WHILE Boolean_expression   
     { sql_statement | statement_block | BREAK | CONTINUE }  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
WHILE Boolean_expression   
     { sql_statement | statement_block | BREAK }  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Boolean_expression*  
 Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) que devuelve **TRUE** o **FALSE**. Si la expresión booleana contiene una instrucción SELECT, la instrucción SELECT debe ir entre paréntesis.  
  
 {*sql_statement* | *statement_block*}  
 Se trata de cualquier instrucción o grupo de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] definidas con un bloque de instrucciones. Para definir un bloque de instrucciones, utilice las palabras clave de control de flujo BEGIN y END.  
  
 BREAK  
 Produce la salida del bucle WHILE más interno. Se ejecutan las instrucciones que aparecen después de la palabra clave END, que marca el final del bucle.  
  
 CONTINUE  
 Hace que se reinicie el bucle WHILE y omite las instrucciones que haya después de la palabra clave CONTINUE.  
  
## <a name="remarks"></a>Notas  
 Si dos o más bucles WHILE están anidados, la instrucción BREAK interna sale al siguiente bucle más externo. Todas las instrucciones que se encuentran después del final del bucle interno deben ejecutarse primero y después se reinicia el siguiente bucle más externo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-break-and-continue-with-nested-ifelse-and-while"></a>A. Utilizar BREAK y CONTINUE con IF…ELSE y WHILE anidados  
 En el ejemplo siguiente, si el precio de venta promedio de un producto es inferior a `$300`, el bucle `WHILE` dobla los precios y, a continuación, selecciona el precio máximo. Si el precio máximo es menor o igual que `$500`, el bucle `WHILE` se reinicia y vuelve a doblar los precios. Este bucle continúa doblando los precios hasta que el precio máximo es mayor que `$500`, después de lo cual sale del bucle `WHILE` e imprime un mensaje.  
  
```  
USE AdventureWorks2012;  
GO  
WHILE (SELECT AVG(ListPrice) FROM Production.Product) < $300  
BEGIN  
   UPDATE Production.Product  
      SET ListPrice = ListPrice * 2  
   SELECT MAX(ListPrice) FROM Production.Product  
   IF (SELECT MAX(ListPrice) FROM Production.Product) > $500  
      BREAK  
   ELSE  
      CONTINUE  
END  
PRINT 'Too much for the market to bear';  
```  
  
### <a name="b-using-while-in-a-cursor"></a>B. Usar WHILE en un cursor  
 En el ejemplo siguiente se usa `@@FETCH_STATUS` para controlar las actividades del cursor en un bucle `WHILE`.  
  
```  
DECLARE @EmployeeID as nvarchar(256)
DECLARE @Title as nvarchar(50)

DECLARE Employee_Cursor CURSOR FOR  
SELECT LoginID, JobTitle   
FROM AdventureWorks2012.HumanResources.Employee  
WHERE JobTitle = 'Marketing Specialist';  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor INTO @EmployeeID, @Title;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      Print '   ' + @EmployeeID + '      '+  @Title 
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO 
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-while-loop"></a>C. Bucle WHILE simple  
 En el ejemplo siguiente, si el precio de venta promedio de un producto es inferior a `$300`, el bucle `WHILE` dobla los precios y, a continuación, selecciona el precio máximo. Si el precio máximo es menor o igual que `$500`, el bucle `WHILE` se reinicia y vuelve a doblar los precios. Este bucle continúa doblando los precios hasta que el precio máximo es mayor que `$500`, después de lo cual sale del bucle `WHILE`.  
  
```  
-- Uses AdventureWorks  
  
WHILE ( SELECT AVG(ListPrice) FROM dbo.DimProduct) < $300  
BEGIN  
    UPDATE dbo.DimProduct  
        SET ListPrice = ListPrice * 2;  
    SELECT MAX ( ListPrice) FROM dbo.DimProduct  
    IF ( SELECT MAX (ListPrice) FROM dbo.DimProduct) > $500  
        BREAK;  
END  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Lenguaje de control de flujo &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Cursores &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  


