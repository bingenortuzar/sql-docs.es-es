---
title: Fecha y hora y conjuntos de filas de esquema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
ms.assetid: 8c35e86f-0597-4ef4-b2b8-f643e53ed4c2
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 21f72a13f8f5f7ac93b0f31716632c9280df5fb9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107013"
---
# <a name="metadata---date-and-time-and-schema-rowsets"></a>Metadatos: fecha y hora y conjuntos de filas de esquema
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  En este tema se proporciona información sobre los conjuntos de filas COLUMNS y PROCEDURE_PARAMETERS. Esta información está relacionada con las mejoras realizadas en la fecha y la hora de OLE DB introducidas en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="columns-rowset"></a>Conjunto de filas COLUMNS  
 Para los tipos de fecha y hora se devuelven los siguientes valores de columna:  
  
|Tipo de columna|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|date|DBTYPE_DBDATE|Desactivar|0|  
|time|DBTYPE_DBTIME2|Establecer|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|Desactivar|0|  
|datetime|DBTYPE_DBTIMESTAMP|Desactivar|3|  
|datetime2|DBTYPE_DBTIMESTAMP|Establecer|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|Establecer|0..7|  
  
 En COLUMN_FLAGS, DBCOLUMNFLAGS_ISFIXEDLENGTH es siempre TRUE para los tipos de fecha y hora, y las marcas siguientes son siempre FALSE:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 Se pueden establecer las marcas restantes (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE y DBCOLUMNFLAGS_WRITEUNKNOWN), dependiendo de cómo se defina la columna.  
  
 Se proporciona una nueva marca en COLUMN_FLAGS, DBCOLUMNFLAGS_SS_ISVARIABLESCALE, para permitir que una aplicación determine el tipo de servidor de columnas, donde DATA_TYPE es DBTYPE_DBTIMESTAMP. DATETIME_PRECISION también se debe utilizar para identificar el tipo de servidor.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE es solo válido cuando se conecta a un servidor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o posteriores. DBCOLUMNFLAGS_SS_ISFIXEDSCALE no está definido cuando se conecta a servidores de nivel inferior.  
  
## <a name="procedureparameters-rowset"></a>Conjunto de filas PROCEDURE_PARAMETERS  
 DATA_TYPE contiene los mismos valores que el conjunto de filas de esquema COLUMNS y TYPE_NAME contiene el tipo de servidor.  
  
 Se ha agregado una nueva columna, SS_DATETIME_PRECISION, para devolver la precisión del tipo como en la columna DATETIME_PRECISION, similar al conjunto de filas COLUMNS.  
  
## <a name="providertypes-rowset"></a>Conjunto de filas PROVIDER_TYPES  
 Para los tipos de fecha y hora se devuelven las siguientes filas:  
  
|Tipo -><br /><br /> columna|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|escala|NULL|NULL|escala|escala|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE a menos que se dé uno de los siguientes casos:<br /><br /> Es un cliente conectado a un servidor de nivel inferior.<br /><br /> La propiedad de conexión de compatibilidad de tipo de datos especifica un nivel de compatibilidad igual a 80.|VARIANT_TRUE a menos que se dé uno de los siguientes casos:<br /><br /> Es un cliente conectado a un servidor de nivel inferior.<br /><br /> La propiedad de conexión de compatibilidad de tipo de datos especifica un nivel de compatibilidad igual a 80.|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 OLE DB solamente define MINIMUM_SCALE y MAXIMUM_SCALE para tipos numéricos y decimales, de modo que el uso que hace [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client de estas columnas para time, datetime2 y datetimeoffset no es estándar.  
  
## <a name="see-also"></a>Vea también  
 [Metadatos &#40;OLE DB&#41;](https://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
  
  
