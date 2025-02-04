---
title: Método setAutoCommit (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dbf9b18fdc6b590f085b5be6babd64100006163a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975262"
---
# <a name="setautocommit-method-sqlserverconnection"></a>Método setAutoCommit (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el modo de confirmación automática para este objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) en el estado determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *value*  
  
 Es **true** cuando se habilita el modo de confirmación automática para la conexión; es **false** cuando se deshabilita.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método setAutoCommit se especifica mediante el método setAutoCommit en la interfaz java. SQL. Connection.  
  
 Si una conexión está en modo de confirmación automática, todas sus instrucciones SQL se ejecutan y confirman como transacciones individuales. De lo contrario, sus instrucciones SQL se agrupan en transacciones que finalizan con una llamada al método [commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) o al método [rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md). De forma predeterminada, las nuevas conexiones están en modo de confirmación automática.  
  
 La confirmación se produce cuando la instrucción se completa o se produce la siguiente ejecución, lo que antes ocurra. En el caso de las instrucciones que devuelven un objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md), la instrucción se completa cuando se haya recuperado la última fila del conjunto de resultados, o bien cuando se haya cerrado el conjunto de resultados. En casos avanzados, una instrucción única podría devolver varios resultados además de los valores de parámetros de salida. En estos casos, la confirmación se produce cuando se hayan recuperado todos los resultados y valores de parámetros de salida.  
  
 Cuando el modo de confirmación automática es **false**, el controlador JDBC iniciará implícitamente una nueva transacción después de cada confirmación.  
  
> [!NOTE]  
>  Si se llama a este método durante una transacción, esta se confirma.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
