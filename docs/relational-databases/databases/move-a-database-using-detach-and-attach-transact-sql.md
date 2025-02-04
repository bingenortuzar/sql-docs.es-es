---
title: Movimiento de una base de datos mediante Separar y Adjuntar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database attaching [SQL Server]
- moving databases [SQL Server]
- database detaching [SQL Server]
- relocating databases [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 6732a431-cdef-4f1e-9262-4ac3b77c275e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 54e2ce24f4fd0b0d94344029cd2f56e378e579dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067355"
---
# <a name="move-a-database-using-detach-and-attach-transact-sql"></a>Mover una base de datos mediante Separar y Adjuntar (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo mover una base de datos separada a otra ubicación y volver a adjuntarla a la misma instancia de servidor o a otra en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. No obstante, se recomienda mover las bases de datos mediante el procedimiento de reubicación programada ALTER DATABASE, en lugar usar las operaciones de separar y adjuntar. Para más información, consulte [Move User Databases](../../relational-databases/databases/move-user-databases.md).  
  
> [!IMPORTANT]  
>  Se recomienda no adjuntar ni restaurar bases de datos de orígenes desconocidos o que no sean de confianza. Es posible que dichas bases de datos contengan código malintencionado que podría ejecutar código [!INCLUDE[tsql](../../includes/tsql-md.md)] no deseado o provocar errores al modificar el esquema o la estructura de la base de datos física. Para usar una base de datos desde un origen desconocido o que no sea de confianza, ejecute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) en la base de datos de un servidor que no sea de producción y examine también el código, como procedimientos almacenados u otro código definido por el usuario, en la base de datos.  
  
## <a name="procedure"></a>Procedimiento  
  
#### <a name="to-move-a-database-by-using-detach-and-attach"></a>Para mover una base de datos mediante la operación de separar y adjuntar  
  
1.  Separe la base de datos. Para obtener más información, vea [Separar una base de datos](../../relational-databases/databases/detach-a-database.md)  
  
2.  En el Explorador de Windows o en una ventana del símbolo del sistema de Windows, mueva el archivo o archivos de la base de datos separada y el archivo o archivos de registro a la nueva ubicación.  
  
     Debe mover los archivos de registro, incluso si piensa crear nuevos archivos de registro. En algunos casos, para volver a adjuntar una base de datos son necesarios sus archivos de registro. Por tanto, mantenga siempre todos los archivos de registro separados hasta que la base de datos se haya adjuntado correctamente sin ellos.  
  
    > [!NOTE]  
    >  Si intenta adjuntar la base de datos sin especificar el archivo de registro, la operación de adjuntar buscará el archivo de registro en su ubicación original. Si aún hay una copia del registro en la ubicación original, se adjunta esa copia. Para evitar que se utilice el archivo de registro original, especifique la ruta de acceso del nuevo archivo de registro o elimine la copia original del archivo de registro (después de copiarlo en la nueva ubicación).  
  
3.  Adjunte los archivos copiados. Para más información, consulte [Attach a Database](../../relational-databases/databases/attach-a-database.md).  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se crea una copia de la base de datos de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] denominada `MyAdventureWorks`. Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] se ejecutan en una ventana del Editor de consultas que esté conectada a la instancia del servidor a la que se ha adjuntado.  
  
1.  Separe la base de datos de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] ejecutando las siguientes instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'AdventureWorks2012';  
    GO  
    ```  
  
2.  Con el método que prefiera, copie los archivos de base de datos (AdventureWorks208R2_Data.mdf y AdventureWorks208R2_log) en: C:\MySQLServer\AdventureWorks208R2_Data.mdf y C:\MySQLServer\AdventureWorks208R2_Log.ldf, respectivamente.  
  
    > [!IMPORTANT]  
    >  En el caso de una base de datos de producción, coloque la base de datos y el registro de transacciones en discos independientes.  
  
     Para copiar archivos a través de la red en un disco de un equipo remoto, use el nombre UNC (Convención de nomenclatura universal) de la ubicación remota. Un nombre UNC toma la forma **\\\\** _nombreDeServidor_ **\\** _nombreDelRecursoCompartido_ **\\** _rutaDeAcceso_ **\\** _nombreDeArchivo_. De la misma forma que al escribir archivos en el disco duro local, se debe conceder a la cuenta de usuario que usa la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]los permisos necesarios para leer o escribir en archivos del disco remoto.  
  
3.  Adjunte la base de datos movida y, opcionalmente, su registro ejecutando las siguientes instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
    ```  
    USE master;  
    GO  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks2012_Data.mdf'),  
        (FILENAME = 'C:\MySQLServer\AdventureWorks2012_Log.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
     En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], una base de datos recién adjuntada no es inmediatamente visible en el Explorador de objetos. Para ver la base de datos, en el Explorador de objetos, haga clic en **Ver** y, a continuación, en **Actualizar**. Cuando se expande el nodo **Bases de datos** en el Explorador de objetos, la base de datos recién adjuntada aparecerá en la lista de bases de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
