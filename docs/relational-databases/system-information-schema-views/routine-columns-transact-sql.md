---
title: ROUTINE_COLUMNS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- ROUTINE_COLUMNS_TSQL
- ROUTINE_COLUMNS
dev_langs:
- TSQL
helpviewer_keywords:
- ROUTINE_COLUMNS view
- INFORMATION_SCHEMA.ROUTINE_COLUMNS view
ms.assetid: 91dbc61b-e4c0-4826-976c-b2fce88b7793
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5b0ed500b1217ae70dca72ab6eab64ab661c22ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078535"
---
# <a name="routinecolumns-transact-sql"></a>ROUTINE_COLUMNS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada columna devuelta por las funciones con valores de tabla a las que puede tener acceso el usuario actual en la base de datos actual.  
  
 Para recuperar información desde esta vista, especifique el nombre completo de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|Nombre de catálogo o base de datos de la función con valores de tabla.|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|Nombre del esquema que contiene la función con valores de tabla.<br /><br /> <strong>\*\* Importante \* \*</strong>  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|Nombre de la función con valores de tabla.|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|Nombre de columna.|  
|**ORDINAL_POSITION**|**int**|Número de identificación de la columna.|  
|**COLUMN_DEFAULT**|**nvarchar(** 4000 **)**|Valor predeterminado de la columna.|  
|**IS_NULLABLE**|**varchar(** 3 **)**|Si esta columna permite valores NULL, devuelve YES. De lo contrario, devuelve NO.|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|Tipo de datos proporcionado por el sistema.|  
|**CAMPO CHARACTER_MAXIMUM_LENGTH**|**int**|Longitud máxima, en caracteres, de los datos binarios, de caracteres, o de texto e imagen.<br /><br /> -1 para **xml** y datos de tipo de valor grande. De lo contrario, devuelve NULL. Para obtener más información, vea [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
|**CHARACTER_OCTET_LENGTH**|**int**|Longitud máxima, en bytes, para datos binarios, datos de caracteres o datos de texto e imagen.<br /><br /> -1 para **xml** y datos de tipo de valor grande. De lo contrario, devuelve NULL.|  
|**CAMPO NUMERIC_PRECISION**|**tinyint**|Precisión de los datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. De lo contrario, devuelve NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base de la precisión de datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. De lo contrario, devuelve NULL.|  
|**NUMERIC_SCALE**|**tinyint**|Escala de datos numéricos aproximados, datos numéricos exactos, datos enteros o datos monetarios. De lo contrario, devuelve NULL.|  
|**DATETIME_PRECISION**|**smallint**|Código de subtipo para **datetime** e ISO**entero** tipos de datos. Para otros tipos de datos, devuelve NULL.|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|Devuelve **maestro**. Esto indica que la base de datos en la que se encuentra el conjunto de caracteres si la columna contiene datos de caracteres o **texto** tipo de datos. De lo contrario, devuelve NULL.|  
|**CHARACTER_SET_SCHEMA**|**varchar(** 3 **)**|Siempre devuelve NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|Devuelve el nombre único para el juego de caracteres si esta columna contiene datos de caracteres o **texto** tipo de datos. De lo contrario, devuelve NULL.|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|Siempre devuelve NULL.|  
|**COLLATION_SCHEMA**|**varchar(** 3 **)**|Siempre devuelve NULL.|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|Devuelve el nombre único para el criterio de ordenación si la columna de datos de caracteres o **texto** tipo de datos. De lo contrario, devuelve NULL.|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|Si la columna es de un tipo de datos de alias, esta columna es el nombre de la base de datos en que se creó el tipo de datos definido por el usuario. De lo contrario, devuelve NULL.|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|Si la columna es de un tipo de datos definido por el usuario, esta columna indica el nombre del esquema que contiene el tipo de datos definido por el usuario. De lo contrario, devuelve NULL.<br /><br /> <strong>\*\* Importante \* \*</strong>  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**DOMAIN_NAME**|**nvarchar(** 128 **)**|Si la columna es de un tipo de datos definido por el usuario, esta columna es el nombre del tipo de datos definido por el usuario. De lo contrario, devuelve NULL.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
