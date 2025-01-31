---
title: Las instrucciones SQL escrita por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 78a1653df60b21cde772cbe32a688b3fdef80a42
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086069"
---
# <a name="sql-statements-entered-by-the-user"></a>Instrucciones SQL escritas por el usuario
Las aplicaciones que realizan análisis ad hoc también suele permiten al usuario que escriba las instrucciones SQL directamente. Por ejemplo:  
  
```  
SQLCHAR *     Statement, SqlState[6], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLSMALLINT   i, MsgLen;  
SQLINTEGER    NativeError;  
SQLRETURN     rc1, rc2;  
  
// Prompt user for SQL statement.  
GetSQLStatement(Statement);  
  
// Execute the statement directly. Because it will be executed only once,  
// do not prepare it.  
rc1 = SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Process any errors or returned information.  
if ((rc1 == SQL_ERROR) || rc1 == SQL_SUCCESS_WITH_INFO) {  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
         Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState, NativeError, Msg, MsgLen);  
      i++;  
   }  
}  
```  
  
 Este enfoque simplifica la programación de aplicaciones; la aplicación se basa en el usuario para generar la instrucción SQL y en el origen de datos para comprobar la validez de la instrucción. Dado que es difícil de escribir una interfaz gráfica de usuario que expone adecuadamente los pormenores de SQL, basta con que pide al usuario que escriba el texto de la instrucción SQL puede ser una alternativa preferible. Sin embargo, esto requiere que el usuario saber no solo SQL, sino también el esquema del origen de datos que se está consultando. Algunas aplicaciones proporcionan una interfaz gráfica de usuario mediante el cual el usuario puede crear una instrucción SQL básica y también proporcionan una interfaz de texto con el que el usuario puede modificar.
