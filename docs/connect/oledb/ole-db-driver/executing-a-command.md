---
title: Ejecutar un comando | Microsoft Docs
description: Ejecutar un comando
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- commands [OLE DB Driver for SQL Server]
- OLE DB, executing commands
- sessions [OLE DB Driver for SQL Server]
- OLE DB extensions for XML
- OLE DB Driver for SQL Server, command execution
author: pmasl
ms.author: pelopes
ms.openlocfilehash: f13c9177a74212b849572881f114e503a9530286
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994991"
---
# <a name="executing-a-command"></a>Ejecutar un comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Una vez establecida la conexión a un origen de datos, el consumidor llama al método **IDBCreateSession:: createSession** para crear una sesión. La sesión actúa como un comando, conjunto de filas o fábrica de transacciones.  
  
 Para trabajar directamente con índices o tablas individuales, el consumidor solicita la interfaz **IOpenRowset**. El método **IOpenRowset::OpenRowset** se abre y devuelve un conjunto de filas que incluye todas las filas de un índice o tabla base única.  
  
 Para ejecutar un comando (como SELECT \* FROM Authors), el consumidor solicita la interfaz **IDBCreateCommand**. El consumidor puede ejecutar el método **IDBCreateCommand:: CreateCommand** para crear un objeto de comando y solicitar la interfaz **ICommandText** . El método **ICommandText:: SetCommandText** se usa para especificar el comando que se va a ejecutar.  
  
 El comando **Execute** se utiliza para ejecutar el comando. El comando puede ser cualquier instrucción SQL o nombre de procedimiento. No todos los comandos generan un objeto de conjunto de resultados (conjunto de filas). Comandos como SELECT * FROM Autores generan un conjunto de resultados.  
  
## <a name="see-also"></a>Consulte también  
 [Creación de un controlador OLE DB para la aplicación de SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
