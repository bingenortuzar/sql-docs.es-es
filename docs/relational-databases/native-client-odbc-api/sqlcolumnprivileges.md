---
title: SQLColumnPrivileges | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1f4ec3c0837f282193c937a4b0e8800b7456b57f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113590"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLColumnPrivileges** devuelve SQL_SUCCESS si existen o no valores para el*CatalogName*, *SchemaName*, *TableName*, o  *ColumnName* parámetros. **SQLFetch** devuelve SQL_NO_DATA si se usan valores no válidos en estos parámetros.  
  
 **SQLColumnPrivileges** se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar **SQLColumnPrivileges** en un cursor actualizable (dinámico o conjunto de claves) devolverá SQL_SUCCESS_WITH_INFO, que indica que se ha cambiado el tipo de cursor.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el *CatalogName* parámetro: *Nombre_servidor_vinculado.nombre_catálogo*.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLColumnPrivileges](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
