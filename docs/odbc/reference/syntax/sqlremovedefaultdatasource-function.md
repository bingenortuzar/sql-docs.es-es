---
title: Función SQLRemoveDefaultDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDefaultDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDefaultDataSource
helpviewer_keywords:
- SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cfefcd9f2f55e2d78c5c6e5b1bac7ce52e9033e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024599"
---
# <a name="sqlremovedefaultdatasource-function"></a>Función SQLRemoveDefaultDataSource
**Conformidad**  
 Versión de introducción: ODBC 1.0, en desuso  
  
 **Resumen**  
 En ODBC 3.0, el **SQLRemoveDefaultDataSource** función ha sido reemplazada por una llamada a [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) con un *fRequest* argumento de ODBC_REMOVE_DEFAULT_DSN. Si un ODBC 2 *.x* programa de instalación llama a esta función, el instalador ODBC asignará al siguiente **SQLConfigDataSource** llamar:  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
