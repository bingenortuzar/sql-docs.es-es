---
title: Método getSQLXML (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: faa35676-573d-48d5-afd9-850134735728
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5bed4b5c0b25566527654111c03808e421eea895
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979725"
---
# <a name="getsqlxml-method-int-sqlserverresultset"></a>Método getSQLXML (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor de la columna designada en la fila actual del objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un objeto SQLXML.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final java.sql.SQLXML getSQLXML(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Valor **int** que indica el índice de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 ASQLXMLobject.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getSQLXML especifica este método getSQLXML en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte también  
 [Método getSQLXML &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
