---
title: Conectar directamente a los controladores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44b9de304069849e965fc335e130ae57d9ec8bad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083164"
---
# <a name="connecting-directly-to-drivers"></a>Conectar directamente a los controladores
Como se explicó en [elegir un origen de datos o controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md), anteriormente en esta sección, algunas aplicaciones no desean usar un origen de datos en absoluto. En su lugar, desean conectarse directamente a un controlador. **SQLDriverConnect** proporciona una forma de la aplicación para conectarse directamente a un controlador sin especificar un origen de datos. Conceptualmente, un origen de datos temporal se crea en tiempo de ejecución.  
  
 Para conectarse directamente a un controlador, la aplicación especifica la **controlador** palabra clave en la cadena de conexión en lugar de la **DSN** palabra clave. El valor de la **controlador** palabra clave es la descripción del controlador, tal como lo devuelve **SQLDrivers**. Por ejemplo, suponga que un controlador con la descripción del controlador de Paradox y requiere que el nombre de un directorio que contiene los archivos de datos. Para conectarse a este controlador, la aplicación puede usar cualquiera de las cadenas de conexión siguientes:  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 Con la primera cadena, el controlador no necesitaría la información adicional. La segunda cadena, el controlador deberá solicitar el nombre del directorio que contiene los archivos de datos.
