---
title: Ejecutar consultas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, executing queries
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
- SQL Server Native Client ODBC driver, queries
- queries [ODBC]
ms.assetid: d935bcba-8ce6-4159-8395-6c86431602ad
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cb9caaa95c24a9d442f53f6ed78eda12eec667c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937288"
---
# <a name="executing-queries-odbc"></a>Ejecutar consultas (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Después de que una aplicación ODBC inicializa un identificador de conexión y conecta con un origen de datos, asigna uno o más identificadores de instrucciones en el identificador de conexión. A continuación, puede ejecutar la aplicación [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instrucciones en el identificador de instrucción. La secuencia general de eventos para ejecutar una instrucción SQL es:  
  
1.  Establezca los atributos de instrucción necesarios.  
  
2.  Construya la instrucción.  
  
3.  Ejecute la instrucción.  
  
4.  Recupere los conjuntos de resultados.  
  
 Después de que una aplicación recupera todas las filas en todos los conjuntos de resultados devueltos por la instrucción SQL, puede ejecutar otra consulta en el mismo identificador de instrucciones. Si una aplicación determina que no es necesario para recuperar todas las filas de un conjunto de resultados determinado, puede cancelar el resto del conjunto de resultados por una llamada a [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) o [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md).  
  
 Si, en una aplicación ODBC, debe ejecutar varias veces la misma instrucción SQL con datos diferentes, utilice en la construcción de la instrucción SQL un marcador de parámetros denotado por un signo de interrogación (?)  
  
```  
INSERT INTO MyTable VALUES (?, ?, ?)  
```  
  
 Cada marcador de parámetro, a continuación, se puede enlazar a una variable de programa mediante una llamada a [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md).  
  
 Una vez ejecutadas todas las instrucciones SQL y procesados sus conjuntos de resultados, la aplicación libera el identificador de instrucción.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client es compatible con varios identificadores de instrucciones por identificador de conexión. Las transacciones se administran en el nivel de conexión, para que todo el trabajo realizado en todos los identificadores de instrucciones de una única conexión se administre como parte de la misma transacción.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Asignar un identificador de instrucción](../../relational-databases/native-client-odbc-queries/allocating-a-statement-handle.md)  
  
-   [Crear una instrucción SQL &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/constructing-an-sql-statement-odbc.md)  
  
-   [Crear instrucciones SQL para cursores](../../relational-databases/native-client-odbc-queries/constructing-sql-statements-for-cursors.md)  
  
-   [Usar parámetros de instrucciones](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
-   [Ejecución de instrucciones &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
-   [Liberar un identificador de instrucción](../../relational-databases/native-client-odbc-queries/freeing-a-statement-handle.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
