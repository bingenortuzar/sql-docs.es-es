---
title: Eliminación de archivos de datos o de registro de una base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], files
- deleting files
- removing files
- removing data
- data deletions [SQL Server]
- file deletion [SQL Server]
- deleting data
ms.assetid: 0db4018c-ce2c-4ba1-bb29-1e4f3791c925
author: stevestein
ms.author: sstein
ms.openlocfilehash: be0f5865965ab419d1807783196e18a4e873c6a0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073764"
---
# <a name="delete-data-or-log-files-from-a-database"></a>Eliminar archivos de datos o de registro de una base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo eliminar archivos de datos o de registro en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Para eliminar archivos de datos o de registro de una base de datos, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Para poder eliminar un archivo debe estar vacío. Para obtener más información, vea [Reducir un archivo](../../relational-databases/databases/shrink-a-file.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la base de datos.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-delete-data-or-log-files-from-a-database"></a>Para eliminar archivos de datos o de registro de una base de datos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, haga clic con el botón derecho en la base de datos de la que quiera eliminar el archivo y, después, haga clic en **Propiedades**.  
  
3.  Seleccione la página **Archivos** .  
  
4.  En la cuadrícula **Archivos de base de datos** , seleccione el archivo que desee eliminar y haga clic en **Quitar**.  
  
5.  Haga clic en **Aceptar**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-delete-data-or-log-files-from-a-database"></a>Para eliminar archivos de datos o de registro de una base de datos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. Este ejemplo quita el archivo `test1dat4`.  
  
 [!code-sql[DatabaseDDL#AlterDatabase4](../../relational-databases/databases/codesnippet/tsql/delete-data-or-log-files_1.sql)]  
  
 Para obtener más ejemplos, vea [Opciones File y Filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
## <a name="see-also"></a>Consulte también  
 [Reducir una base de datos](../../relational-databases/databases/shrink-a-database.md)   
 [Agregar archivos de datos o de registro a una base de datos](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
  
  
