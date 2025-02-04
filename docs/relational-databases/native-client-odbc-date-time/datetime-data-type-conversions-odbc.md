---
title: fecha y hora de las conversiones de tipo de datos (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC]
- bindings [ODBC]
- ODBC, bindings and conversions
ms.assetid: 66b9d282-c88d-40e5-93c2-fd5499a74458
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d16221a47f2cee588d0c5ef38aaa179b61bdf8f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030392"
---
# <a name="datetime-data-type-conversions-odbc"></a>Conversiones del tipo de datos de fecha y hora (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Las conversiones siguientes ya están definidas por ODBC o son una extensión coherente de ODBC. La comunidad atendida por el proveedor determina las conversiones proporcionadas por cada proveedor y, a consecuencia de ello, hay incoherencias a menudo entre los proveedores. Los valores entre corchetes son opcionales.  
  
-   El formato de las cadenas de fecha y hora es 'aaaa-mm-dd [hh:mm:ss [,9999999] [más/menos hh:mm]]'  
  
-   El formato de las cadenas de hora es 'hh:mm:ss [,9999999]'  
  
-   El formato de las cadenas de fecha es 'aaaa-mm-dd'  
  
 Las conversiones de las cadenas permiten flexibilidad en los espacios en blanco y el ancho de campo. Para obtener más información, consulte la "formatos de datos: Sección de cadenas y literales"de [compatibilidad con tipos de datos de ODBC mejoras de fecha y hora](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md).  
  
 A continuación figuran las reglas de conversión generales:  
  
-   Si no está presente la hora pero el receptor puede almacenar la hora, esta última se establece en cero.  
  
-   Si no está presente la fecha pero el receptor puede almacenar fechas, se utiliza la fecha actual.  
  
-   Si no está presente la zona horaria en el tipo de datos que el cliente utiliza pero el servidor puede almacenar la zona horaria, se almacena la fecha en la zona horaria del cliente. Observe que esto difiere del comportamiento del servidor.  
  
-   Si no está presente la zona horaria en el tipo de servidor pero el tipo de cliente tiene una zona horaria, la hora se convierte en UTC antes de almacenarse en el servidor.  
  
-   Si está presente la hora pero el receptor no puede almacenar la hora, se omite el componente de hora.  
  
-   Si está presente la fecha pero el receptor no puede almacenar la fecha, se omite el componente de fecha.  
  
-   Si se produce una truncación de segundos o fracciones de segundo al convertir de C a SQL, se genera un registro de diagnóstico con SQLSTATE 22008 y el mensaje "Desbordamiento del campo DateTime".  
  
-   Si se produce una truncación de segundos o fracciones de segundo al convertir de SQL a C, se genera un registro de diagnóstico con SQLSTATE 01S07 y el mensaje "Truncamiento fraccionario".  
  
## <a name="in-this-section"></a>En esta sección  
 [Conversiones de C a SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)  
 Se enumeran los problemas a tener en cuenta al convertir de tipos de C a tipos de fecha y hora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Conversiones de SQL a C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)  
 Se enumeran los problemas a tener en cuenta al convertir de tipos de fecha y hora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a tipos de C.  
  
## <a name="see-also"></a>Vea también  
 [Mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
