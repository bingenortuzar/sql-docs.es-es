---
title: Usar claves generadas automáticamente | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 55a062c7-45ce-40e3-9a6f-4a0f4da4e2a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f93bad7ff490ee2774d10e2df940168a67d30867
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026614"
---
# <a name="using-auto-generated-keys"></a>Empleo de claves generadas automáticamente

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite las API de JDBC 3.0 opcionales para recuperar los identificadores de fila generados automáticamente. El valor principal de esta característica es proporcionar un método de modo que los valores IDENTITY estén disponibles para la aplicación que actualiza la tabla de base de datos sin necesidad de una consulta y un segundo ciclo de ida y vuelta en el servidor.

Dado que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite seudocolumnas para los identificadores, las actualizaciones en las que se debe usar la característica de clave generada automáticamente deben funcionar en una tabla que contenga una columna IDENTITY. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo permite una única columna IDENTITY por tabla. El conjunto de resultados devuelto por el método [getGeneratedKeys](../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) contiene tan solo una columna y se devuelve el nombre de columna GENERATED_KEYS. Si las claves generadas se solicitan en una tabla que no contiene la columna IDENTITY, el controlador JDBC devuelve un conjunto de resultados con valores nulos.

A modo de ejemplo, cree la siguiente tabla en la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
CREATE TABLE TestTable
   (Col1 int IDENTITY,
    Col2 varchar(50),
    Col3 int);  
```

En el siguiente ejemplo, se pasa una conexión abierta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] a la función, se genera una instrucción SQL que agregará datos a la tabla y, después, la instrucción se ejecuta y se muestra el valor de la columna IDENTITY.

[!code[JDBC#UsingAutoGeneratedKeys1](../../connect/jdbc/codesnippet/Java/using-auto-generated-keys_1.java)]

## <a name="see-also"></a>Vea también

[Empleo de instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)
