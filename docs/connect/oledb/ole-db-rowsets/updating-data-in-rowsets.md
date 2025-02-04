---
title: Actualizar datos en conjuntos de filas | Microsoft Docs
description: Actualizar datos en conjuntos de filas con OLE DB controlador para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, updating data
- OLE DB Driver for SQL Server, data updates
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: pelopes
ms.openlocfilehash: e19128d6defa2c154cc8bddbcc4bcaa761b58a2b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015338"
---
# <a name="updating-data-in-rowsets"></a>Actualizar datos en conjuntos de filas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server actualiza los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando un consumidor actualiza un conjunto de filas modificable que contiene esos datos. Se crea un conjunto de filas modificable cuando el consumidor solicita compatibilidad para las interfaces **IRowsetUpdate** o **IRowsetChange**.  
  
 Todos los OLE DB controlador para los conjuntos de filas modificables [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQL Server usan cursores para admitir el conjunto de filas. La propiedad de conjunto de filas DBPROP_LOCKMODE modifica el comportamiento de control de simultaneidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en cursores y determina el comportamiento de la captura de filas del conjunto de filas y la generación de errores de integridad de datos en los conjuntos de filas actualizables.  
  
 El controlador de OLE DB para SQL Server admite la sincronización de filas antes o después de una actualización.  
  
> [!NOTE]  
>  IRowChange::SetColumns está disponible para establecer los valores de una o más columnas con nombre de un objeto de fila.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Actualizar datos en cursores de SQL Server](../../oledb/ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [Volver a sincronizar filas](../../oledb/ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
