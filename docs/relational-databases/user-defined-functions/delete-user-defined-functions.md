---
title: Eliminación de funciones definidas por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: db1d668a-23b7-4757-a9c5-1bd848ba7f6d
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9ec9cd60ff4197b94a91e280ad17cc349b906dc6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138500"
---
# <a name="delete-user-defined-functions"></a>Eliminar funciones definidas por el usuario
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Puede eliminar (quitar) las funciones definidas por el usuario en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para eliminar una función definida por el usuario, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   No podrá eliminar la función si hay vistas o funciones de Transact-SQL en la base de datos que hagan referencia a esta función y que fueron creadas con SCHEMABINDING; tampoco funcionará si existen columnas calculadas o restricciones CHECK o DEFAULT que hacen referencia a la función.  
  
-   No podrá eliminar la función si existen columnas calculadas que hagan referencia a esta función y que hayan sido indizadas.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en el esquema al que pertenece la función o el permiso CONTROL en la función.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-delete-a-user-defined-function"></a>Para eliminar un perfil definido por la función  
  
1.  Haga clic en el signo más junto a la base de datos que contenga la función que desea modificar.  
  
2.  Haga clic en el signo más junto a la carpeta **Programación** .  
  
3.  Haga clic en el signo más junto a la carpeta que contenga la función que desea modificar:  
  
    -   Table-valued Function  
  
    -   Función con valor escalar  
  
    -   Función de agregado  
  
4.  Haga clic con el botón derecho en la función que quiera eliminar y seleccione **Eliminar**.  
  
5.  En el cuadro de diálogo **Eliminar objeto** , haga clic en **Aceptar**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    > [!IMPORTANT]  
    >  Click **Show Dependencies** in the **Delete Object** dialog box to open the _function\_name_**Dependencies** dialog box. This will show all of the objects that depend on the function and all of the objects on which the function depends.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-delete-a-user-defined-function"></a>Para eliminar un perfil definido por la función  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- creates function called "Sales.ufn_SalesByStore"  
    USE AdventureWorks2012;  
    GO  
    CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
    RETURNS TABLE  
    AS  
    RETURN   
    (  
        SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
        FROM Production.Product AS P   
        JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
        JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
        JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
        WHERE C.StoreID = @storeid  
        GROUP BY P.ProductID, P.Name  
    );  
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- determines if function exists in database  
    IF OBJECT_ID (N'Sales.fn_SalesByStore', N'IF') IS NOT NULL  
    -- deletes function  
        DROP FUNCTION Sales.fn_SalesByStore;  
    GO  
    ```  
  
 Para obtener más información, vea [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md).  
  
  
