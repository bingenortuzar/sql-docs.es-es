---
title: Conversiones de SQL a C | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], SQL to C
ms.assetid: 059431e2-a65c-4587-ba4a-9929a1611e96
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd19cb92f2d2f333954adeb97229feb718c4b592
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63207036"
---
# <a name="conversions-from-sql-to-c"></a>Conversiones de SQL a C
  En la tabla siguiente se indican los problemas que hay que tener en cuenta a la hora de convertir tipos de fecha y hora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en tipos de C.  
  
## <a name="conversions"></a>Conversiones  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
||SQL_C_DATE|SQL_C_TIME|SQL_C_TIMESTAMP|SQL_C_SS_TIME2|SQL_C_SS_TIMESTAMPOFFSET|SQL_C_BINARY|SQL_C_CHAR|SQL_C_WCHAR|  
|SQL_CHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|1|1|1|  
|SQL_WCHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|1|1|1|  
|SQL_TYPE_DATE|Aceptar|12|13|12|13,23|14|16|16|  
|SQL_SS_TIME2|12|8|15|Aceptar|10,23|17|16|16|  
|SQL_TYPE_TIMESTAMP|18|7,8|Aceptar|7|23|19|16|16|  
|SQL_SS_TIMESTAMPOFFSET|18,22|7,8,20|20|7,20|Aceptar|21|16|16|  
  
## <a name="key-to-symbols"></a>Clave de los símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|Aceptar|Ningún problema de conversión.|  
|1|Se aplican las reglas anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|2|Se omiten los espacios iniciales y finales.|  
|3|La cadena se analiza en un valor de tipo date, time, timezone o timezoneoffset y permite hasta 9 dígitos para las fracciones de segundo. Si se analiza un valor de tipo timezoneoffset, la hora se convierte a la zona horaria del cliente. Si se produce un error durante esta conversión, se genera un registro de diagnóstico con SQLSTATE 22018 y el mensaje "Desbordamiento del campo Datetime".|  
|4|Si el valor no es un valor de tipo date, timestamp o timestampoffset válido, se genera un registro de diagnóstico con SQLSTATE 22018 y el mensaje "Valor de carácter no válido para especificación cast".|  
|5|Si la hora es distinta de cero, se genera un registro de diagnóstico con SQLSTATE 01S07 y el mensaje "Truncamiento fraccionario".|  
|6|Si el valor no es un valor de tipo time, timestamp o timestampoffset válido, se genera un registro de diagnóstico con SQLSTATE 22018 y el mensaje "Valor de carácter no válido para especificación cast".|  
|7|Se omite el componente de fecha.|  
|8|Si las fracciones de segundo son distintas de cero, se genera un registro de diagnóstico con SQLSTATE 01S07 y el mensaje "Truncamiento fraccionario".|  
|9|Si el valor no es un valor de tipo date, time, timestamp o timestampoffset válido, se genera un registro de diagnóstico con SQLSTATE 22018 y el mensaje "Valor de carácter no válido para especificación cast".|  
|10|Si el valor es un valor de tipo time válido, el componente de fecha se establece en la fecha actual del cliente.|  
|11|Si el valor es un valor de tipo date válido, la hora se establece en cero.|  
|12|Se genera un registro de diagnóstico con SQLSTATE 07006 y el mensaje "Infracción del atributo de tipo de datos restringido".|  
|13|La hora se establece en cero.|  
|14|Si el búfer no es suficientemente grande como para alojar SQL_DATE_STRUCT, se genera un registro de diagnóstico con SQLSTATE 22003 y el mensaje "Valor numérico fuera del intervalo".|  
|15|La fecha se establece en la fecha actual del cliente.|  
|16|Si el búfer no es suficientemente grande como para alojar el valor de cadena convertido, sino solamente las fracciones de segundo, los datos se truncan y se genera un registro de diagnóstico con SQLSTATE 01004 y el mensaje "Cadena truncada por la derecha". Si el búfer no es suficientemente grande como para alojar el valor de cadena sin truncamiento de los componentes de fecha, hora o desplazamiento, se genera un registro de diagnóstico con SQLSTATE 22003 y el mensaje "Valor numérico fuera del intervalo". Tenga en cuenta que para los valores de tipo date y timestampoffset, no es posible que se genere SQLSTATE 01004 porque la parte de la cadena convertida situada más a la derecha no contiene fracciones de segundo. Por lo tanto, cualquier truncamiento produce una pérdida de datos.|  
|17|Si el búfer no es suficientemente grande como para alojar SQL_SS_TIME2_STRUCT, se genera un registro de diagnóstico con SQLSTATE 22003 y el mensaje "Valor numérico fuera del intervalo".|  
|18|Si la hora es distinta de cero, se genera un registro de diagnóstico con SQLSTATE 01S07 y el mensaje "Truncamiento fraccionario".|  
|19|Si el tipo de servidor es datetime o smalldatetime, el valor corresponde al formato de conexión TDS y será un valor de 4 bytes para smalldatetime y un valor de 8 bytes para datetime.<br /><br /> Si el tipo de servidor es datetime2, el valor se devuelve como SQL_TIMESTAMP_STRUCT. Si el búfer no es suficientemente grande como para alojar el valor devuelto, se genera un registro de diagnóstico con SQLSTATE 22003 y el mensaje "Valor numérico fuera del intervalo".|  
|20|Se convierte la hora en la zona horaria del cliente. Si se produce un error durante esta conversión, se genera un registro de diagnóstico con SQLSTATE 22008 y el mensaje "Desbordamiento del campo DateTime".|  
|21|Si el búfer es suficientemente grande como para alojar SQL_SS_TIMESTAMPOFFSET_STRUCT, el valor se devuelve como SQL_SS_TIMESTAMPOFFSET_STRUCT. De lo contrario, se genera un registro de diagnóstico con SQLSTATE 22003 y el mensaje "Valor numérico fuera del intervalo".|  
|22|El valor se convierte a la zona horaria del cliente antes de que se extraiga la fecha. Esto proporciona coherencia con otras conversiones con tipos timestampoffset. Si se produce un error durante esta conversión, se genera un registro de diagnóstico con SQLSTATE 22008 y el mensaje "Desbordamiento del campo DateTime". Esto puede dar lugar a una fecha que difiera del valor obtenido por truncamiento simple.|  
  
 En la tabla de este tema se describen las conversiones entre el tipo devuelto al cliente y el tipo del enlace. Para los parámetros de salida, si el tipo de servidor especificado en SQLBindParameter no coincide con el tipo real en el servidor, se realizará una conversión implícita por el servidor y el tipo devuelto al cliente coincidirá con el tipo especificado a través de SQLBindParameter. Esto puede conducir a resultados de conversión inesperados cuando las reglas de conversión del servidor son diferentes de los que aparecen en la tabla anterior. Por ejemplo, cuando es necesario proporcionar una fecha predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa 1900-1-1 en lugar de la fecha actual.  
  
## <a name="see-also"></a>Vea también  
 [Mejoras de fecha y hora &#40;ODBC&#41;](date-and-time-improvements-odbc.md)  
  
  
