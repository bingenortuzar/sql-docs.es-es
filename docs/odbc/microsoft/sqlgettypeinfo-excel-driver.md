---
title: SQLGetTypeInfo (Excel Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Excel Driver
- Excel driver [ODBC], SQLGetTypeInfo
ms.assetid: 708845be-e6a1-4677-8113-c52819a43fa4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 227fef1ecd28e5099b599e86c82c3cc42fbacd0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898708"
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Devuelve el nombre del tipo (TYPE_NAME) en la tabla generada por **SQLGetTypeInfo** será el nombre más utilizado por el origen de datos.  
  
 SQL_ALL_EXCEPT_LIKE se devolverá en la columna de búsqueda para el Byte, contador, Double, tipos de datos único, larga y corta. (La capacidad similar puede lograrse mediante la conversión del valor en un carácter mediante las funciones de conversión canónica de ODBC, a continuación, realizar la comparación).  
  
 Cuando se usa el controlador de Microsoft Excel, los nombres de tipo ODBC se devuelven en la columna TYPE_NAME devuelto por **SQLGetTypeInfo**.
