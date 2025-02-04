---
title: sqlsrv_client_info | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_client_info
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_client_info
- sqlsrv_client_info
ms.assetid: 3e2d3679-436a-45d8-8bdc-7c633b65a720
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 861e686d4a64b1030224b8ec35551fade4188ca5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992830"
---
# <a name="sqlsrvclientinfo"></a>sqlsrv_client_info
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Devuelve información sobre la pila de conexión y cliente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_client_info( resource $conn)  
```  
  
#### <a name="parameters"></a>Parámetros  
*$conn*: el recurso de conexión mediante el cual está conectado el cliente.  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve una matriz asociativa con las claves descritas en la tabla siguiente, o bien **False** si el valor del recurso de conexión es Null.  
  
**Para PHP (versiones 3.2 y 3.1 de SQL Server)** :  
  
|Key|Descripción|  
|-------|---------------|  
|DriverDllName|MSODBCSQL11.DLL (ODBC Driver 11 for SQL Server)|  
|DriverODBCVer|Versión de ODBC (xx.yy)|  
|DriverVer|Versión de la DLL de ODBC Driver 11 for SQL Server:<br /><br />xx.yy.zzzz (versión 3.2 o 3.1 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)])|  
|ExtensionVer|Versión de php_sqlsrv.dll:<br /><br />3.2.xxxx.x (para la versión 3.2 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)])<br /><br />3.1.xxxx.x (para la versión 3.1 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)])|  
  
**Para PHP (versiones 3.0 y 2.0 de SQL Server)** :  
  
|Key|Descripción|  
|-------|---------------|  
|DriverDllName|SQLNCLI10.DLL (versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)])|  
|DriverODBCVer|Versión de ODBC (xx.yy)|  
|DriverVer|Versión de la DLL de SQL Server Native Client:<br /><br />10.50.xxx (versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)])|  
|ExtensionVer|Versión de php_sqlsrv.dll:<br /><br />2.0.xxxx.x (versión 2.0 de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)])|  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se crea información del cliente en la consola cuando se ejecuta dicho ejemplo en la línea de comandos. En el ejemplo se da por hecho que SQL Server está instalado en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
if( $client_info = sqlsrv_client_info( $conn))  
{  
       foreach( $client_info as $key => $value)  
      {  
              echo $key.": ".$value."\n";  
      }  
}  
else  
{  
       echo "Client info error.\n";  
}  
  
/* Close connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  
  
