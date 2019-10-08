---
title: REPLACE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- REPLACE_TSQL
- REPLACE
dev_langs:
- TSQL
helpviewer_keywords:
- first string expression [SQL Server]
- replacing string expression
- third string expressions [SQL Server]
- second string expressions [SQL Server]
- REPLACE function
ms.assetid: 8a7aaaf2-62e3-46c0-8e44-fa22290dd86b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 59cbaf203b8e877f9476e807008345b9af05b0fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944534"
---
# <a name="replace-transact-sql"></a>REPLACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Reemplaza todas las instancias de un valor de cadena especificado por otro valor de cadena.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
REPLACE ( string_expression , string_pattern , string_replacement )  
```  
  
## <a name="arguments"></a>Argumentos  
 *string_expression*  
 Es la [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cadena que se va a buscar. *string_expression* puede ser de un tipo de datos binario o de caracteres.  
  
 *string\_pattern*  
 Es la subcadena en la que se va a buscar. *string_pattern* puede ser de un tipo de datos binario o de caracteres. *string_pattern* no puede ser una cadena vacía ('') y no debe superar el número máximo de bytes que cabe en una página.  
  
 *string\_replacement*  
 Es la cadena de reemplazo. *string_replacement* puede tener un tipo de datos de carácter o binario.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve **nvarchar** si uno de los argumentos de entrada tiene el tipo de datos **nvarchar**; de lo contrario, REPLACE devuelve **varchar**.  
  
 Devuelve NULL si alguno de los argumentos es NULL.  
  
 Si *string_expression* no es de tipo **varchar(max)** o **nvarchar(max), REPLACE** trunca el valor devuelto en 8000 bytes. Para devolver valores mayores de 8000 bytes, *string_expression* se debe convertir explícitamente en un tipo de datos de valores grandes.  
  
## <a name="remarks"></a>Notas  
 REPLACE realiza comparaciones basándose en la intercalación de la entrada. Para realizar una comparación de una intercalación especificada, puede usar [COLLATE](~/t-sql/statements/collations.md) para aplicar una intercalación explícita a la entrada.  
  
 0x0000 (**char(0)** ) es un carácter no definido en las intercalaciones de Windows y no se puede incluir en REPLACE.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo reemplaza la cadena `cde` de `abcdefghi` por `xxx`.  
  
```sql  
SELECT REPLACE('abcdefghicde','cde','xxx');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
abxxxfghixxx  
(1 row(s) affected)  
```  
  
 El siguiente ejemplo utiliza la función `COLLATE`.  
  
```sql  
SELECT REPLACE('This is a Test'  COLLATE Latin1_General_BIN,  
'Test', 'desk' );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
This is a desk  
(1 row(s) affected)  
```  

  
## <a name="see-also"></a>Consulte también  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
