---
title: Eliminación de grupos de archivos inactivos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], defunct filegroups
- defunct filegroups
- restoring filegroups [SQL Server]
- deferred transactions
- filegroups [SQL Server], defunct
- unrestored filegroups
ms.assetid: 055f9c6a-5c18-4942-98e7-ec918f0ff975
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d2fd69c58f9572a479e4ba95fab1d1af9e0214be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937677"
---
# <a name="remove-defunct-filegroups-sql-server"></a>Quitar grupos de archivos inactivos (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo quitar grupos de archivos inactivos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para quitar grupos de archivos inactivos, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Este tema es pertinente para las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que incluyen varios archivos o grupos de archivos y, en el modelo simple, solo para grupos de archivos de solo lectura.  
  
-   Todos los archivos de un grupo de archivos pasan a estar inactivos cuando se quita un grupo de archivos sin conexión.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Si no se va a restaurar nunca un grupo de archivos sin restaurar, se puede convertir en *inactivo* quitándolo de la base de datos. El grupo de archivos inactivo no se podrá restaurar nunca en esta base de datos, aunque los metadatos permanecen en ella. Una vez inactivo el grupo de archivos, la base de datos se puede reiniciar y la recuperación hará que la base de datos sea coherente en todos los grupos de archivos restaurados.  
  
     Por ejemplo, establecer un grupo de archivos como inactivo es una opción para resolver transacciones diferidas generadas por un grupo de archivos sin conexión que ya no es necesario en la base de datos. Las transacciones que estaban diferidas porque el grupo de archivos estaba sin conexión salen del estado diferido una vez que el grupo de archivos queda inactivo. Para obtener más información, vea [Transacciones diferidas &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la base de datos.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-remove-defunct-filegroups"></a>Para quitar grupos de archivos inactivos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, haga clic con el botón derecho en la base de datos de la que quiera eliminar el archivo y, después, haga clic en **Propiedades**.  
  
3.  Seleccione la página **Archivos** .  
  
4.  En la cuadrícula **Archivos de base de datos** , seleccione los archivos que desee eliminar, haga clic en **Quitar**y, a continuación en **Aceptar**.  
  
5.  Seleccione la página **Grupos de archivos** .  
  
6.  En la cuadrícula **Filas** , seleccione el grupo de archivos que desee eliminar, haga clic en **Quitar**y, a continuación, en **Aceptar**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-remove-defunct-filegroups"></a>Para quitar grupos de archivos inactivos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. (**Nota:** En este ejemplo se supone que ya existen los archivos y el grupo de archivos. Para crear estos objetos, vea el ejemplo B del tema [Opciones File y Filegroup de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)). En el primer ejemplo se quitan los archivos `test1dat3` y `test1dat4` del grupo de archivos inactivo utilizando la instrucción `ALTER DATABASE` con la cláusula `REMOVE FILE`. En el segundo ejemplo se quita el grupo de archivos inactivo `Test1FG1` utilizando la cláusula `REMOVE FILEGROUP`.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat3 ;  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4 ;  
GO  
  
```  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILEGROUP Test1FG1 ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [Opciones File y Filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)   
 [Transacciones diferidas &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)   
 [Restauraciones de archivos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Restauraciones de archivos &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Restauración con conexión &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
