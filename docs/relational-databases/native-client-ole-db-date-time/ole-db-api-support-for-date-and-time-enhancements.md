---
title: Compatibilidad de la API de OLE DB con las mejoras de fecha y hora | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f99055c13cf04f15d652f79258b10654410e98c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909242"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Compatibilidad de API de OLE DB con las mejoras de fecha y hora
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Las siguientes API de OLE DB son compatibles con las características mejoradas de fecha y hora.  
  
|Función|Descripción|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Se agrega una marca de la estructura DBBINDING para habilitar las aplicaciones para diferenciar entre **datetime**, **datetime2**, y **smalldatetime** valores. Para obtener más información, consulte [Parameter and Rowset Metadata](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Para obtener más información, consulte [cambios de copia masiva para tipos mejorada de fecha y hora &#40;OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).|  
|ICommandWithParameters::GetParameterInfo|Para obtener más información, consulte[Parameter and Rowset Metadata](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Para obtener más información, consulte[Parameter and Rowset Metadata](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Para obtener más información, consulte[Parameter and Rowset Metadata](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Para obtener más información, consulte[Parameter and Rowset Metadata](../../relational-databases/native-client-ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Para obtener detalles de los conjuntos de filas de esquema afectados, consulte[fecha y hora y conjuntos de filas de esquema](../../relational-databases/native-client-ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md).|  
|IRowsetFastLoad|Esta interfaz admite los nuevos tipos de fecha y hora, pero no hay ningún cambio en su interfaz.|  
|ITableDefinition::CreateTable|Para obtener más información, consulte [compatibilidad con tipos de datos para OLE DB mejoras de fecha y hora](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Vea también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
