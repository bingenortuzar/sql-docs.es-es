---
title: Definición de un dispositivo lógico de copia de seguridad para un archivo de disco (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], defining
- backup devices [SQL Server], disks
- disk backup devices [SQL Server]
- database backups [SQL Server], disks
- backing up databases [SQL Server], disks
ms.assetid: 86331d43-c738-4523-ae3d-7d6700348ed1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0ae32391bd2f10525b89015272d11bcdb6468298
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62877871"
---
# <a name="define-a-logical-backup-device-for-a-disk-file-sql-server"></a>Definir un dispositivo lógico de copia de seguridad para un archivo de disco (SQL Server)
  En este tema se describe cómo definir un dispositivo lógico de copia de seguridad para un archivo de disco en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Un dispositivo lógico es un nombre definido por el usuario que señala un dispositivo físico de copia de seguridad específico (un archivo de disco o unidad de cinta).  La inicialización del dispositivo físico tiene lugar posteriormente, cuando se escribe una copia de seguridad en el dispositivo de copia de seguridad.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para definir un dispositivo lógico de copia de seguridad en un archivo de disco, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El nombre de dispositivo lógico debe ser único entre todos los dispositivos lógicos de copia de seguridad de la instancia de servidor. Para ver los nombres de los dispositivos lógicos existentes, consulte la vista de catálogo [sys.backup_devices](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql) .  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Se recomienda que el disco de copia de seguridad no sea el disco de datos o del registro de la base de datos. Esto es necesario para garantizar el acceso a las copias de seguridad si el disco de datos o del registro presenta errores.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Debe pertenecer al rol fijo de servidor **diskadmin** .  
  
 Requiere permiso para escribir en el disco.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-define-a-logical-backup-device-for-a-disk-file"></a>Para definir un dispositivo lógico de copia de seguridad en un archivo de disco  
  
1.  Tras conectarse a la instancia apropiada de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol correspondiente.  
  
2.  Expanda **Objetos de servidor**y, después, haga clic con el botón derecho en **Dispositivos de copia de seguridad**.  
  
3.  Haga clic en **Nuevo dispositivo de copia de seguridad**. Se abrirá el cuadro de diálogo **Dispositivo de copia de seguridad** .  
  
4.  Escriba un nombre para el dispositivo.  
  
5.  Para indicar el destino, haga clic en **Archivo** y especifique la ruta de acceso completa del archivo.  
  
6.  Para definir el nuevo dispositivo, haga clic en **Aceptar**.  
  
 Para realizar una copia de seguridad en este nuevo dispositivo, agréguelo en el campo **Copia de seguridad en:** del cuadro de diálogo **Copia de seguridad de base de datos** (**General**). Para obtener más información, vea [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-define-a-logical-backup-for-a-disk-file"></a>Para definir un dispositivo lógico de copia de seguridad para un archivo de disco  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql) para definir un dispositivo lógico de copia de seguridad para un archivo de disco. El ejemplo agrega el dispositivo de copia de seguridad de disco denominado `mydiskdump`, con el nombre físico `c:\dump\dump1.bak`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'disk', 'mydiskdump', 'c:\dump\dump1.bak' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [sp_dropdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdevice-transact-sql)   
 [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
