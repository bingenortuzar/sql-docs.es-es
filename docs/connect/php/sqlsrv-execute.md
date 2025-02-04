---
title: sqlsrv_execute | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_execute
apitype: NA
helpviewer_keywords:
- sqlsrv_exclude
- executing queries
- API Reference, sqlsrv_execute
ms.assetid: 38331bc2-4391-4f9f-aa83-9873dad605a0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba15ea2e756e6c83b2fcdb6cf56c39511bd95296
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992754"
---
# <a name="sqlsrvexecute"></a>sqlsrv_execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ejecuta una instrucción preparada previamente. Consulte [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) para obtener información sobre cómo preparar una instrucción para ejecutarla.  
  
> [!NOTE]  
> Esta función es perfecta para ejecutar una instrucción preparada varias veces con distintos valores de parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sqlsrv_execute( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parámetros  
*$stmt*: recurso que especifica la instrucción que se ejecutará. Para obtener más información sobre cómo crear un recurso de instrucción, consulte [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
## <a name="return-value"></a>Valor devuelto  
Se devuelve un valor booleano **True** si la instrucción se ha ejecutado correctamente. De lo contrario, se devuelve el valor **False**.  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se ejecuta una instrucción que actualiza un campo de la tabla *Sales.SalesOrderDetail* de la base de datos de [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) . En el ejemplo se da por hecho que SQL Server y la base de datos de AdventureWorks están instalados en el equipo local. Los resultados se agregan a la consola cuando se ejecuta el ejemplo en la línea de comandos.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up the Transact-SQL query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = ( ?)   
         WHERE SalesOrderDetailID = ( ?)";  
  
/* Set up the parameters array. Parameters correspond, in order, to  
question marks in $tsql. */  
$params = array( 5, 10);  
  
/* Create the statement. */  
$stmt = sqlsrv_prepare( $conn, $tsql, $params);  
if( $stmt )  
{  
     echo "Statement prepared.\n";  
}  
else  
{  
     echo "Error in preparing statement.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Execute the statement. Display any errors that occur. */  
if( sqlsrv_execute( $stmt))  
{  
      echo "Statement executed.\n";  
}  
else  
{  
     echo "Error in executing statement.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte también  
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Sobre los ejemplos de código de la documentación](../../connect/php/about-code-examples-in-the-documentation.md)  

[sqlsrv_query](../../connect/php/sqlsrv-query.md)  
  
