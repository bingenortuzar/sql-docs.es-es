---
title: Ver una lista de bases de datos en una instancia de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- current databases
- databases currently on server [SQL Server]
- database list [SQL Server]
- viewing database list
- displaying database list
- databases [SQL Server], viewing
- servers [SQL Server], databases listed on
- listing databases
ms.assetid: 7ee7a789-db36-4be9-8a0e-0362a1e152dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cdce1c0fc6f36bb0d58e93abba29ecab9d2dcd54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916996"
---
# <a name="view-a-list-of-databases-on-an-instance-of-sql-server"></a>Ver una lista de bases de datos en una instancia de SQL Server
  En este tema se describe cómo ver una lista de bases de datos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver una lista de bases de datos en una instancia de SQL Server, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Si el autor de la llamada de **sys.databases** no es el propietario de la base de datos y la base de datos no es **maestra** o **tempdb**, los permisos mínimos necesarios para ver la fila correspondiente son el permiso ALTER ANY DATABASE o VIEW ANY DATABASE de nivel de servidor, o el permiso CREATE DATABASE en la base de datos **maestra** . La base de datos a la que está conectado el autor de la llamada siempre se puede ver en **sys.databases**.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-view-a-list-of-databases-on-an-instance-of-sql-server"></a>Para ver una lista de bases de datos en una instancia de SQL Server  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, a continuación, expándala.  
  
2.  Para ver una lista de todas las bases de datos de la instancia, expanda **Bases de datos**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-view-a-list-of-databases-on-an-instance-of-sql-server"></a>Para ver una lista de bases de datos en una instancia de SQL Server  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se devuelve una lista de las bases de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La lista incluye los nombres de las bases de datos, los id. de base de datos y las fechas en que se crearon las bases de datos.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name, database_id, create_date  
FROM sys.databases ;  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de archivos y bases de datos &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
