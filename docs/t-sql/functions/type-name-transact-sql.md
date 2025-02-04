---
title: TYPE_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TYPE_NAME_TSQL
- TYPE_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- names [SQL Server], data types
- unqualified type names
- type names [SQL Server]
- data types [SQL Server], names
- TYPE_NAME function
ms.assetid: e4075a2e-5f70-440f-986b-9ec8434e07c1
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 33f282c79c15a8b9548d799ef86e026fd7357d00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098706"
---
# <a name="typename-transact-sql"></a>TYPE_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el nombre de tipo no calificado de un Id. de tipo específico.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
TYPE_NAME ( type_id )   
```  
  
## <a name="arguments"></a>Argumentos  
 *type_id*  
 Es el identificador del tipo que se va a utilizar. *type_id* es de tipo **int** y puede hacer referencia a un tipo de cualquier esquema al que el autor de la llamada tenga permiso de acceso.  
  
## <a name="return-types"></a>Tipos devueltos  
 **sysname**  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como TYPE_NAME, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Notas  
 TYPE_NAME devolverá un NULL cuando *type_id* no sea válido o cuando el autor de la llamada no cuente con los permisos necesarios para hacer referencia al tipo.  
  
 TYPE_NAME funciona con tipos de datos de sistema así como con tipos de datos definidos por el usuario. El tipo puede estar contenido en cualquier esquema, pero siempre se devuelve un nombre de tipo no calificado. Esto significa que el nombre no tiene el prefijo _schema_ **.** Prefix.  
  
 Las funciones del sistema se pueden usar en la lista de selección, en la cláusula WHERE y en cualquier lugar donde se permita una expresión. Para más información, vea [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md) y [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el nombre del objeto, de la columna y del tipo perteneciente a cada columna de la tabla `Vendor` de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
SELECT o.name AS obj_name, c.name AS col_name,  
       TYPE_NAME(c.user_type_id) AS type_name  
FROM sys.objects AS o   
JOIN sys.columns AS c  ON o.object_id = c.object_id  
WHERE o.name = 'Vendor'  
ORDER BY col_name;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
obj_name        col_name                  type_name
--------------- ------------------------ --------------
Vendor          AccountNumber            AccountNumber
Vendor          ActiveFlag               Flag
Vendor          BusinessEntityID         int
Vendor          CreditRating             tinyint
Vendor          ModifiedDate             datetime
Vendor          Name                     Name
Vendor          PreferredVendorStatus    Flag
Vendor          PurchasingWebServiceURL  nvarchar

(8 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En este siguiente ejemplo se devuelve el valor de `TYPE ID` para el tipo de datos del sistema con identificador `1`.  
  
```  
SELECT TYPE_NAME(36) AS Type36, TYPE_NAME(239) AS Type239;  
GO  
```  
  
 Para ver una lista de tipos, consulte sys.types.  
  
```  
SELECT * FROM sys.types;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [TYPE_ID &#40;Transact-SQL&#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
  
  

