---
title: Probar la conexión de ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02509ddb6a986ebb7796d80aca10c6f18cde6e69
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939706"
---
# <a name="testing-the-odbc-connection"></a>Probar la conexión de ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Al solucionar problemas de acceso ODBC para Oracle 7.x y servidores de Oracle8 RDBMS, podría ser necesario comprobar que el SQL subyacente * Net y protocolo adaptadores para Oracle se han instalado correctamente. Para ello, use la utilidad suministrado por Oracle Nettest.exe en el directorio Orawin\Bin.  
  
 Nettest es una utilidad simple que intenta iniciar sesión en el servidor seleccionado usando solo el instalada de SQL * Net software que forma parte del cliente de Oracle. La utilidad le pedirá un nombre de inicio de sesión, contraseña y TNS cadena de conexión. Si el cliente de Oracle está instalado correctamente, la utilidad simplemente mostrará "Ping correcto". Si el inicio de sesión no se realizó correctamente, deberá consultar con un administrador de base de datos.
