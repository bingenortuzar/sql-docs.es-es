---
title: Asignar tipos de datos XSD a tipos de datos de XPath (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- XPath queries [SQLXML], mapping data types
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XPath data types [SQLXML]
- XSD schemas [SQLXML], mapping data types
ms.assetid: ced1a95e-18d4-4a5a-8da8-dbb6d58bbd45
author: MightyPen
ms.author: genemi
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a7f79a4d756a76dc6b59e76bbbfc28076ba36eae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067048"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>Asignar tipos de datos de XSD a tipos de datos de XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Cuando se ejecuta una consulta XPath en un esquema XSD y se especifica el tipo XSD en el **xsd: Type** atributo, XPath utiliza el tipo de datos especificado al procesar la consulta.  
  
 El tipo de datos XPath de un nodo se deriva del tipo de dato XSD del esquema, como se muestra en la tabla siguiente. (El nodo EmployeeID se usa a modo de ilustración.)  
  
|Tipo de datos XSD|Tipo de datos XDR|Tipo de datos de XPath<br /><br /> equivalente|SQL Server<br /><br /> conversión que se usa|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**base64Binary**<br /><br /> **hexBinary**|**Ninguno**<br /><br /> **bin.base64bin.hex**|**No aplicable**|None<br /><br /> EmployeeID|  
|**Boolean**|**boolean**|**boolean**|CONVERT (bit, IdEmpleado)|  
|**Decimal, integer, float, byte, short, int, long, float, double, unsignedByte, unsignedShort, unsignedInt, unsignedLong**|**número, int, float, i1, i2, i4, i8, r4, r8ui1, ui2, ui4, ui8**|**number**|CONVERT(float(53), EmployeeID)|  
|**Id, idref, idrefsentity, entidades, notación, nmtoken, nmtokens, DateTime, string, AnyURI**|**Id, idref, idrefsentity, entidades, enumeración, notación, nmtoken, nmtokens, char, dateTime, dateTime.tz, string, uri, uuid**|**string**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**No aplicable (no hay ningún tipo de datos de XPath que es equivalente al tipo de datos fixed14.4 XDR).**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**string**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**string**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
