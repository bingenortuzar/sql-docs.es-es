---
title: Ejecutar funciones definidas por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7e9c170a187fc3ccf28301a2ee1c9ee7b626169f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68196445"
---
# <a name="execute-user-defined-functions"></a>Ejecutar funciones definidas por el usuario
  Puede ejecutar una función definida por el usuario en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para ejecutar definido por el usuario funcione, mediante:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 En Transact-SQL, los parámetros se pueden proporcionar mediante *value* o @*parameter_name*=*value.* Un parámetro no forma parte de una transacción; por tanto, si se cambia un parámetro en una transacción que se revierte posteriormente, el valor del parámetro no vuelve a su valor anterior. El valor devuelto al procedimiento llamante es siempre el valor del parámetro en el momento en que finaliza el módulo llamado.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 No se requieren permisos para ejecutar la instrucción EXECUTE. Sin embargo, se requieren permisos para los elementos protegibles a los que se hace referencia en la cadena EXECUTE. Por ejemplo, si la cadena contiene una instrucción INSERT, el autor de llamada de la instrucción EXECUTE debe tener el permiso INSERT en la tabla de destino. Los permisos se comprueban cuando se encuentra la instrucción EXECUTE, incluso si la instrucción EXECUTE está incluida en un módulo. Para obtener más información, vea [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-execute-a-user-defined-function"></a>Para ejecutar una función definida por el usuario  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Declares a variable and sets it to zero.  
    -- This variable is used to return the results of the function.  
    DECLARE @ret nvarchar(15)= NULL;   
  
    -- Executes the dbo.ufnGetSalesOrderStatusText function.  
    --The function requires a value for one parameter, @Status.   
    EXEC @ret = dbo.ufnGetSalesOrderStatusText @Status= 5;   
    --Returns the result in the message tab.  
    PRINT @ret;  
    ```  
  
 Para obtener más información, vea [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql).  
  
  
