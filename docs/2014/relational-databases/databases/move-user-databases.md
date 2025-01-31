---
title: Movimiento de bases de datos de usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- database files [SQL Server], moving
- data files [SQL Server], moving
- editions [SQL Server], moving databases between
- moving full-text catalogs
- scheduled disk maintenace [SQL Server]
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- moving user databases
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: ad9a4e92-13fb-457d-996a-66ffc2d55b79
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 602ac6de5a2b623e33b1b85b46a9f8cf31e0b225
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871729"
---
# <a name="move-user-databases"></a>Mover bases de datos de usuario
  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede mover los archivos de datos, del registro y del catálogo de texto completo de una base de datos de usuario a una nueva ubicación, especificando la nueva ubicación en la cláusula FILENAME de la instrucción [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) . Este método se aplica para mover archivos de la base de datos dentro de la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para mover una base de datos a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o a otro servidor, use las operaciones de [copias de seguridad y restauración](../backup-restore/back-up-and-restore-of-sql-server-databases.md) o [separar y adjuntar](move-a-database-using-detach-and-attach-transact-sql.md).  
  
## <a name="considerations"></a>Consideraciones  
 Al mover una base de datos a otra instancia de servidor, para proporcionar una experiencia coherente a usuarios y aplicaciones, puede que tenga que volver a crear algunos o todos los metadatos de la base de datos. Para obtener más información, vea [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md).  
  
 Algunas características de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] cambian la manera en que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] almacena información en los archivos de base de datos. Estas características están restringidas a ediciones concretas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una base de datos que contiene estas características no se puede mover a una edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no los admita. Utilice la vista de administración dinámica sys.dm_db_persisted_sku_features para enumerar todas las características específicas de la edición que estén habilitadas en la base de datos actual.  
  
 Los procedimientos descritos en este tema requieren el nombre lógico de los archivos de la base de datos. Para obtener el nombre, consulte la columna de nombre de la vista de catálogo [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql) .  
  
 A partir de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], los catálogos de texto completo se integran en la base de datos, en lugar de almacenarse en el sistema de archivos. Los catálogos de texto completo se mueven ahora automáticamente al mover una base de datos.  
  
## <a name="planned-relocation-procedure"></a>Procedimiento de reubicación planeada  
 Para mover un archivo de datos o de registros como parte de una reubicación planeada, siga estos pasos:  
  
1.  Ejecute la instrucción siguiente:  
  
    ```  
    ALTER DATABASE database_name SET OFFLINE;  
    ```  
  
2.  Mueva el archivo o los archivos a la nueva ubicación.  
  
3.  Con cada archivo que mueva, ejecute la instrucción siguiente:  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name, FILENAME = 'new_path\os_file_name' );  
    ```  
  
4.  Ejecute la instrucción siguiente:  
  
    ```  
    ALTER DATABASE database_name SET ONLINE;  
    ```  
  
5.  Compruebe el cambio de los archivos ejecutando la consulta siguiente.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="relocation-for-scheduled-disk-maintenance"></a>Reubicación para el mantenimiento planeado del disco  
 Para reubicar un archivo como parte de un proceso de mantenimiento planeado del disco, siga estos pasos:  
  
1.  Para cada archivo que se va a mover, ejecute la siguiente instrucción.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE ( NAME = logical_name , FILENAME = 'new_path\os_file_name' );  
    ```  
  
2.  Detenga la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o cierre el sistema para realizar el mantenimiento. Para más información, consulte [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
3.  Mueva el archivo o los archivos a la nueva ubicación.  
  
4.  Reinicie la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el servidor. Para obtener más información, consulte [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
5.  Compruebe el cambio de los archivos ejecutando la consulta siguiente.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="failure-recovery-procedure"></a>Procedimiento de recuperación de errores  
 Si se debe mover un archivo a causa de un error de hardware, siga los pasos que se indican a continuación para reubicar el archivo.  
  
> [!IMPORTANT]  
>  Si no se puede iniciar la base de datos, es decir, si se encuentra en modo sospechoso o en un estado no recuperado, solo los miembros del rol fijo sysadmin podrán mover el archivo.  
  
1.  Detenga la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se inició.  
  
2.  Inicie la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de recuperación solo de master especificando uno de los siguientes comandos en el símbolo del sistema.  
  
    -   Para una instancia predeterminada (MSSQLSERVER), ejecute el siguiente comando:  
  
        ```  
        NET START MSSQLSERVER /f /T3608  
        ```  
  
    -   Para una instancia con nombre, ejecute el siguiente comando:  
  
        ```  
        NET START MSSQL$instancename /f /T3608  
        ```  
  
     Para más información, consulte [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
3.  En cada uno de los archivos que se van a mover, use los comandos **sqlcmd** o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] para ejecutar la siguiente instrucción.  
  
    ```  
    ALTER DATABASE database_name MODIFY FILE( NAME = logical_name , FILENAME = 'new_path\os_file_name' );  
    ```  
  
     Para obtener más información sobre cómo usar la utilidad **sqlcmd** , vea [Usar la utilidad sqlcmd](../scripting/sqlcmd-use-the-utility.md).  
  
4.  Salga de la utilidad **sqlcmd** o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
5.  Detenga la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
6.  Mueva el archivo o los archivos a la nueva ubicación.  
  
7.  Inicie la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por ejemplo, ejecute: `NET START MSSQLSERVER`.  
  
8.  Compruebe el cambio de los archivos ejecutando la consulta siguiente.  
  
    ```  
    SELECT name, physical_name AS CurrentLocation, state_desc  
    FROM sys.master_files  
    WHERE database_id = DB_ID(N'<database_name>');  
    ```  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se mueve el archivo de registro [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] a la nueva ubicación como parte de una reubicación planeada.  
  
```  
USE master;  
GO  
-- Return the logical file name.  
SELECT name, physical_name AS CurrentLocation, state_desc  
FROM sys.master_files  
WHERE database_id = DB_ID(N'AdventureWorks2012')  
    AND type_desc = N'LOG';  
GO  
ALTER DATABASE AdventureWorks2012 SET OFFLINE;  
GO  
-- Physically move the file to a new location.  
-- In the following statement, modify the path specified in FILENAME to  
-- the new location of the file on your server.  
ALTER DATABASE AdventureWorks2012   
    MODIFY FILE ( NAME = AdventureWorks2012_Log,   
                  FILENAME = 'C:\NewLoc\AdventureWorks2012_Log.ldf');  
GO  
ALTER DATABASE AdventureWorks2012 SET ONLINE;  
GO  
--Verify the new location.  
SELECT name, physical_name AS CurrentLocation, state_desc  
FROM sys.master_files  
WHERE database_id = DB_ID(N'AdventureWorks2012')  
    AND type_desc = N'LOG';  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [Mover bases de datos del sistema](system-databases.md)   
 [Mover archivos de base de datos](move-database-files.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
