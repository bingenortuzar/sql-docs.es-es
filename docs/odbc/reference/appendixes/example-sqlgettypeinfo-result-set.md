---
title: Conjunto de resultados de SQLGetTypeInfo de ejemplo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], examples
- SQLGetTypeInfo function [ODBC], examples
- data types [ODBC], SQL data types
ms.assetid: dc1952cc-7581-4d69-9c72-7dc1cd370836
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8264f1dfad8bff5d676cd4de8c8b9d7763b39b52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948749"
---
# <a name="example-sqlgettypeinfo-result-set"></a>Conjunto de resultados de SQLGetTypeInfo de ejemplo
Una aplicación llama a **SQLGetTypeInfo** para determinar qué tipos de datos son compatibles con un origen de datos y las características de esos tipos de datos. Las siguientes tablas muestran un conjunto de resultados de ejemplo devuelto por **SQLGetTypeInfo** para un origen de datos que admita SQL_CHAR, SQL_LONGVARCHAR, SQL_DECIMAL, SQL_REAL, SQL_DATETIME, SQL_INTERVAL_YEAR y SQL_INTERVAL_DAY_TO_SECOND.  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|"char"|SQL_CHAR|255|"'"|"'"|"longitud de|SQL_TRUE|  
|"text"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<Null >|SQL_TRUE|  
|"decimal"|SQL_DECIMAL|28|\<Null >|\<Null >|"precisión,<br />escala"|SQL_TRUE|  
|"real"|SQL_REAL|7|\<Null >|\<Null >|\<Null >|SQL_TRUE|  
|"datetime"|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<Null >|SQL_TRUE|  
|"INTERVALO YEAR() AÑO"|SQL_INTERVAL_YEAR|9|"'"|"'"|"precisión"|SQL_TRUE|  
|"INTERVALO DAY() A FRACTION(5)"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|"precisión"|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<Null >|SQL_FALSE|\<Null >|"char"|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<Null >|SQL_FALSE|\<Null >|"text"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"decimal"|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|"real"|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<Null >|SQL_FALSE|\<Null >|"datetime"|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<Null >|SQL_FALSE|\<Null >|"INTERVALO YEAR() AÑO"|  
|**SQL_INTERVAL_DAY_TO_SECOND**|SQL_FALSE|SQL_PRED_BASIC|\<Null >|SQL_FALSE|\<Null >|"INTERVALO DAY() A FRACTION(5)"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<Null >|\<Null >|SQL_CHAR|\<Null >|\<Null >|\<Null >|  
|**SQL_LONGVARCHAR**|\<Null >|\<Null >|SQL_LONGVARCHAR|\<Null >|\<Null >|\<Null >|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<Null >|10|\<Null >|  
|**SQL_REAL**|\<Null >|\<Null >|SQL_REAL|\<Null >|10|\<Null >|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<Null >|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<Null >|9|  
|**SQL_INTERVAL_DAY_TO_SECOND**|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<Null >|9|
