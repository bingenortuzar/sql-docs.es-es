---
title: Conexión y recuperación de datos | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bd4751fe3d1acb7119c87e39ecd8694a0fa83c19
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028226"
---
# <a name="connecting-and-retrieving-data"></a>Conexión y recuperación de datos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Cuando se trabaja con el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], hay dos métodos principales para establecer una conexión con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uno de estos métodos establece las propiedades de conexión en la URL de conexión y, a continuación, llama al método getConnection de la clase DriverManager para devolver un objeto [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
> [!NOTE]  
> Para obtener una lista de las propiedades de conexión compatibles con el controlador JDBC, vea [establecer las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
El segundo método implica el establecimiento de las propiedades de conexión mediante los métodos establecedores de la clase [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) y, a continuación, la llamada al método [getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) para devolver un objeto SQLServerDataSource.  
  
En los temas de esta sección se describen los distintos modos en que puede conectarse a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se muestran las distintas técnicas para recuperar datos.  
  
## <a name="in-this-section"></a>En esta sección  
  
| Tema                                                                | Descripción                                                                                                                                                   |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Ejemplo de URL de conexión](../../connect/jdbc/connection-url-sample.md) | Describe cómo usar una URL de conexión para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y usar una instrucción SQL para recuperar datos. |
| [Ejemplo de origen de datos](../../connect/jdbc/data-source-sample.md)       | Describe cómo usar un origen de datos para conectarse a SQL y usar un procedimiento almacenado para recuperar datos.                                                 |
  
## <a name="see-also"></a>Vea también

[Aplicaciones de ejemplo del controlador JDBC](../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
