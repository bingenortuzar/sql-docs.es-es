---
title: Cierre el Cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de22797bdcf4ff526a8c17aee313567da3114b60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036545"
---
# <a name="closing-the-cursor"></a>Cierre el Cursor
Cuando una aplicación ha terminado de utilizar un cursor, llama a **SQLCloseCursor** para cerrar el cursor. Por ejemplo:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Hasta que la aplicación cierra el cursor, no se puede usar la instrucción en el que se abre el cursor para la mayoría otras operaciones, como ejecutar otra instrucción SQL. Para obtener una lista completa de las funciones que se puede llamar mientras está abierto un cursor, vea [Apéndice B: Las tablas de transición de estado de ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
> [!NOTE]  
>  Para cerrar un cursor, una aplicación debe llamar a **SQLCloseCursor**, no **SQLCancel**.  
  
 Los cursores permanecen abiertos hasta que se cierran explícitamente, excepto cuando se confirma o revierte una transacción, en cuyo caso algunos orígenes de datos cierra el cursor. En particular, alcanzar el final del resultado de conjunto, cuando **SQLFetch** devuelve SQL_NO_DATA, no se cierra un cursor. Incluso los cursores en los conjuntos de resultados vacío (conjuntos de resultados creados cuando una instrucción que se ha ejecutado correctamente, pero que no ha devuelto filas) deben cerrarse explícitamente.
