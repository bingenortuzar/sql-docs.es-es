---
title: NOT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NOT_TSQL
- NOT
dev_langs:
- TSQL
helpviewer_keywords:
- negating Boolean input
- NOT operator [Transact-SQL]
- expressions [SQL Server], negating
- reversing Boolean expression values
ms.assetid: dc07cc35-20f1-46e6-9995-2938390dc19a
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 30977ed0baff058c838403b436a4da497c5ac4c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121988"
---
# <a name="not-transact-sql"></a>NOT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Niega la entrada de un valor booleano.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
[ NOT ] boolean_expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 Es cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) booleana válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Boolean**  
  
## <a name="result-value"></a>Valor del resultado  
 NOT invierte el valor de cualquier expresión booleana.  
  
## <a name="remarks"></a>Notas  
 El uso de NOT niega una expresión.  
  
 La tabla siguiente muestra el resultado de comparar los valores TRUE y FALSE mediante el operador NOT.  
  
||NOT|  
|------|---------|  
|**TRUE**|FALSE|  
|**FALSE**|TRUE|  
|**UNKNOWN**|UNKNOWN|  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se buscan todas las bicicletas Silver que no tienen un precio estándar superior a los 400 $.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID, Name, Color, StandardCost  
FROM Production.Product  
WHERE ProductNumber LIKE 'BK-%' AND Color = 'Silver' AND NOT StandardCost > 400;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ProductID   Name                     Color         StandardCost
 ---------   -------------------      ------      ------------
 984         Mountain-500 Silver, 40  Silver        308.2179
 985         Mountain-500 Silver, 42  Silver        308.2179
 986         Mountain-500 Silver, 44  Silver        308.2179
 987         Mountain-500 Silver, 48  Silver        308.2179
 988         Mountain-500 Silver, 52  Silver        308.2179
 (6 row(s) affected)
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el siguiente ejemplo, los resultados de `SalesOrderNumber` se restringen a los valores que comiencen por `SO6` y a valores de `ProductKeys` mayores o iguales que 400.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductKey, CustomerKey, OrderDateKey, ShipDateKey  
FROM FactInternetSales  
WHERE SalesOrderNumber LIKE 'SO6%' AND NOT ProductKey < 400;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


