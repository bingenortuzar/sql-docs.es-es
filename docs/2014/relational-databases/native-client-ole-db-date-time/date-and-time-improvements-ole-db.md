---
title: Mejoras de fecha y hora (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1dec9e1281d2ff61dcab9312cdf5a7ad1ecb8da3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62866842"
---
# <a name="date-and-time-improvements-ole-db"></a>Mejoras en la fecha y la hora (OLE DB)
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduce nuevos tipos de datos de fecha y hora. En esta sección se describe la forma en que estos nuevos tipos se exponen como extensiones en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para obtener información general de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client con la nueva fecha y tipos de datos de hora, vea [mejoras de fecha y hora](../native-client/features/date-and-time-improvements.md). Para obtener un ejemplo, vea [mejoradas de fecha de uso y las características en tiempo &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md).  
  
 Para obtener información general acerca de los tipos de datos de fecha y hora, vea [datetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql).  
  
## <a name="in-this-section"></a>En esta sección  
 [Compatibilidad con tipos de datos para mejoras de fecha y hora de OLE DB](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 Proporciona información acerca de OLE DB ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) que admiten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos de fecha y hora.  
  
 [Metadatos &#40;OLE DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
 Contiene información sobre la estructura DBBINDING, `ICommandWithParameters::GetParameterInfo`, `ICommandWithParameters::SetParameterInfo`, `IColumnsRowset::GetColumnsRowset`y me`ColumnsInfo::GetColumnInfo`. También proporciona información sobre actualizaciones a conjuntos de filas de esquema de OLE DB.  
  
 [Enlaces y conversiones &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 Describe las reglas para realizar conversiones entre el servidor y el cliente tanto para tipos de datos existentes como nuevos.  
  
 [Cambios en la copia de forma masiva para tipos mejorada fecha y hora &#40;de OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Describe las mejoras de fecha y hora para admitir operaciones de copia masiva.  
  
 [Compatibilidad de API de OLE DB con las mejoras de fecha y hora](ole-db-api-support-for-date-and-time-enhancements.md)  
 Describe las API de OLE DB que admiten las características mejoradas de fecha y hora.  
  
 [Comparaciones en IRowsetFind](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 Describe los tipos de fecha y hora e `IRowsetFind`.  
  
 [Nuevas características fecha y hora con versiones anteriores de SQL Server &#40;OLE DB&#41;](new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 Describe el comportamiento que se espera cuando una aplicación cliente que utiliza características mejoradas de fecha y hora se comunica con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cuando un cliente compilado con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client envía comandos a un servidor que admite características mejoradas de fecha y hora.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
