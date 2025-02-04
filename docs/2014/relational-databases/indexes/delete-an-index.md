---
title: Eliminación de un índice | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- deleting indexes
- dropping indexes
- indexes [SQL Server], dropping
- index deletions [SQL Server]
ms.assetid: fd38a0ed-26c4-4c76-9ef7-e0a16147329d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 092d6e9432f22ef43a155d2a7d3ff03299bcd131
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162319"
---
# <a name="delete-an-index"></a>Eliminar un índice
  En este tema se describe cómo eliminar (quitar) un índice en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para eliminar un índice, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Los índices creados como resultado de una restricción PRIMARY KEY o UNIQUE no se pueden eliminar con este método. En su lugar, se debe eliminar la restricción. Para quitar la restricción y el índice correspondiente, use [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) con la cláusula DROP CONSTRAINT en [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obtener más información, consulte [Delete Primary Keys](../tables/delete-primary-keys.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla o la vista. Este permiso se concede de forma predeterminada al rol fijo de servidor **sysadmin** y a los roles fijos de base de datos **db_ddladmin** y **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-delete-an-index-by-using-object-explorer"></a>Para eliminar un índice mediante el Explorador de objetos  
  
1.  En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que desea eliminar un índice.  
  
2.  Expanda la carpeta **Tablas** .  
  
3.  Expanda la tabla que contiene el índice que desee eliminar.  
  
4.  Expanda la carpeta **Índices** .  
  
5.  Haga clic con el botón derecho en el índice que quiere eliminar y seleccione **Eliminar**.  
  
6.  En el cuadro de diálogo **Eliminar objeto** , compruebe que el índice correcto se encuentra en la cuadrícula **Objeto que se va a eliminar** y haga clic en **Aceptar**.  
  
#### <a name="to-delete-an-index-using-table-designer"></a>Para eliminar un índice mediante el Diseñador de tablas  
  
1.  En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que desea eliminar un índice.  
  
2.  Expanda la carpeta **Tablas** .  
  
3.  Haga clic con el botón secundario en la tabla que contiene el índice que desee eliminar y haga clic en Diseño.  
  
4.  En el menú **Diseñador de tablas** , haga clic en **Índices o claves**.  
  
5.  En el cuadro de diálogo **Índices o claves** , seleccione el índice que quiera eliminar.  
  
6.  Haga clic en **Eliminar**.  
  
7.  Haga clic en **Cerrar**.  
  
8.  En el menú **Archivo** , seleccione **Guardar**_nombre_tabla_.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-delete-an-index"></a>Para eliminar un índice  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- delete the IX_ProductVendor_BusinessEntityID index  
    -- from the Purchasing.ProductVendor table  
    DROP INDEX IX_ProductVendor_BusinessEntityID   
        ON Purchasing.ProductVendor;  
    GO  
    ```  
  
 Para obtener más información, vea [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql).  
  
  
