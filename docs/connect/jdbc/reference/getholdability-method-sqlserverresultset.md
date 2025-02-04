---
title: Método getHoldability (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57bf0cfc206319bf6afcb09435e8787499266c0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982923"
---
# <a name="getholdability-method-sqlserverresultset"></a>Método getHoldability (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la capacidad de alojamiento de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que contiene uno de los siguientes niveles capacidad de alojamiento:  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getHoldability se especifica mediante el método getHoldability de la interfaz java. SQL. ResultSet.  
  
 Para establecer la capacidad de alojamiento del conjunto de resultados, las aplicaciones pueden utilizar el método [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md). Una vez se haya llamado al método [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md), se hayan creado el objeto de instrucciones y el conjunto de resultados, y se haya ejecutado la instrucción, es posible que la aplicación deba cambiar de nuevo la capacidad de alojamiento.  
  
 Para los cursores de servidor, cuando están conectados a SQL Server 2005 o posteriores, la configuración de la capacidad de alojamiento solamente afecta a la de los nuevos conjuntos de resultados que todavía han de ser creados en esa conexión. Con SQL Server 2000, sin embargo, configurar la capacidad de alojamiento afecta a la capacidad de alojamiento de los resultados existentes como a la de los nuevos conjuntos de resultados que todavía han de ser creados en esa conexión.  
  
 Cuando se restablece la función de alojamiento y se llama al método getHoldability en el objeto de conjunto de resultados creado anteriormente, el valor devuelto por este método puede ser diferente del valor de alojamiento devuelto por los métodos siguientes: Statement. getResultSetHoldability , Connection. getHoldability o DatabaseMetaData. getResultSetHoldability.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
