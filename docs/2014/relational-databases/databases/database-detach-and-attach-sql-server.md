---
title: Anexión y separación de bases de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [SQL Server], detaching
- detach database [SQL Server]
- databases [SQL Server], attaching
- removing databases
- transaction logs [SQL Server], detaching
- databases [SQL Server], removing
- restoring [SQL Server], attached databases
- transaction logs [SQL Server], attaching
- differential backups, after detaching
- moving databases
- attach database [SQL Server]
- detaching databases [SQL Server]
- differential base [SQL Server]
- attaching databases [SQL Server]
- databases [SQL Server], moving
ms.assetid: d0de0639-bc54-464e-98b1-6af22a27eb86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5eae331b064d83510d657f6f09a819955e6259a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62762422"
---
# <a name="database-detach-and-attach-sql-server"></a>Adjuntar y separar bases de datos (SQL Server)
  Los archivos de registro de datos y transacciones de una base de datos se pueden desasociar y volverse a adjuntar posteriormente a la misma instancia u otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Separar y adjuntar una base de datos es útil si desea cambiar la base de datos a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el mismo equipo o si desea mover la base de datos.  
  
 El formato de almacenamiento en disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el mismo en los entornos de 64 bits y 32 bits. Por lo tanto, la operación de adjuntar funciona en entornos de 32 bits y de 64 bits.  Una base de datos desasociada de una instancia del servidor que se ejecute en un entorno puede adjuntarse a una instancia del servidor que se ejecute en otro entorno.  
  
  
  
##  <a name="Security"></a> Seguridad  
 Los permisos de acceso a archivos se establecen durante una serie de operaciones de base de datos, incluidas las operaciones de desasociar o adjuntar una base de datos.  
  
> [!IMPORTANT]  
>  Se recomienda no adjuntar ni restaurar bases de datos de orígenes desconocidos o que no sean de confianza. Es posible que dichas bases de datos contengan código malintencionado que podría ejecutar código [!INCLUDE[tsql](../../includes/tsql-md.md)] no deseado o provocar errores al modificar el esquema o la estructura de la base de datos física. Para usar una base de datos desde un origen desconocido o que no sea de confianza, ejecute [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) en la base de datos de un servidor que no sea de producción y examine también el código, como procedimientos almacenados u otro código definido por el usuario, en la base de datos.  
  
##  <a name="DetachDb"></a> Separar una base de datos  
 Al separar una base de datos, la está quitando de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pero la deja intacta en sus archivos de datos y en los archivos de registro de transacciones. Estos archivos pueden utilizarse después para adjuntar la base de datos a cualquier instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluido el servidor del que se separó.  
  
 No podrá separar una base de datos si se cumple cualquiera de las condiciones siguientes:  
  
-   La base de datos está replicada y publicada. Si está replicada, la base de datos no debe estar publicada. Antes de separarla, debe deshabilitar la publicación ejecutando [sp_replicationdboption](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql).  
  
    > [!NOTE]  
    >  Si no puede usar **sp_replicationdboption**, puede quitar la replicación ejecutando [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql).  
  
-   Existe una instantánea de base de datos en la base de datos.  
  
     Para poder separar la base de datos, debe quitar todas sus instantáneas. Para obtener más información, vea [Eliminar una instantánea de base de datos &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md).  
  
    > [!NOTE]  
    >  No puede separar ni adjuntar una instantánea de base de datos.  
  
-   Se va a reflejar la base de datos en una sesión de creación de reflejo de la base de datos.  
  
     No se puede separar la base de datos a menos que se termine la sesión. Para obtener más información, vea [Quitar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
-   La base de datos es sospechosa. Una base de datos sospechosa no puede ser separada. Antes de poder separarla, debe ponerla en modo de emergencia. Para obtener más información sobre cómo poner una base de datos en modo de emergencia, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
-   La base de datos es una base de datos del sistema.  
  
### <a name="backup-and-restore-and-detach"></a>Hacer copias de seguridad y restauración, y separar  
 Al separar una base de datos de solo lectura se pierde información acerca de las bases diferenciales de las copias de seguridad diferenciales. Para obtener más información, vea [Copias de seguridad diferenciales &#40;SQL Server&#41;](../backup-restore/differential-backups-sql-server.md).  
  
### <a name="responding-to-detach-errors"></a>Responder a errores de separación  
 Los errores generados durante la separación de una base de datos pueden impedir que la base de datos se cierre sin problemas y que se vuelva a generar el registro de transacciones. Si recibe un mensaje de error, realice las siguientes acciones correctoras:  
  
1.  Vuelva a adjuntar todos los archivos asociados a la base de datos, no solo el archivo principal.  
  
2.  Resuelva el problema que causó el mensaje de error.  
  
3.  Vuelva a separar la base de datos.  
  
##  <a name="AttachDb"></a> Adjuntar una base de datos  
 Puede adjuntar una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copiada o separada. Cuando adjunte un [!INCLUDE[ssVersion2005](../../includes/sscurrent-md.md)] instancia del servidor, el catálogo se adjuntan archivos desde su ubicación anterior junto con los demás archivos de base de datos, igual que en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obtener más información, vea [Actualizar la búsqueda de texto completo](../search/upgrade-full-text-search.md).  
  
 Al adjuntar una base de datos, todos los archivos de datos deben estar disponibles (archivos MDF y NDF). Si algún archivo de datos tiene una ruta de acceso diferente a la que tenía cuando se creó la base de datos o cuando ésta se adjuntó por última vez, debe especificar la ruta actual.  
  
> [!NOTE]  
>  Si el archivo de datos principal que se va a adjuntar es de solo lectura, [!INCLUDE[ssDE](../../includes/ssde-md.md)] considera que la base de datos es de solo lectura.  
  
 Cuando se adjunta una base de datos cifrada en primer lugar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el propietario de la base de datos debe abrir la clave maestra de la base de datos ejecutando la siguiente instrucción: OPEN MASTER KEY DESCIFRADO POR CONTRASEÑA = **' *`password`* '** . Se recomienda que habilite el descifrado automático de la clave maestra mediante la ejecución de la siguiente instrucción: ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY. Para obtener más información, vea [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql) y [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql).  
  
 Las condiciones para adjuntar archivos de registro dependen, en parte, de si la base de datos es de lectura y escritura o de solo lectura. Vea a continuación:  
  
-   Para una base de datos de lectura y escritura, normalmente, podrá adjuntar un archivo de registro a una ubicación nueva. Sin embargo, en algunos casos, para volver a adjuntar una base de datos son necesarios sus archivos de registro. Por tanto, es importante mantener siempre todos los archivos de registro separados hasta que la base de datos se haya adjuntado correctamente sin ellos.  
  
     Si una base de datos de lectura y escritura contiene solo un archivo de registro y no se especifica una ubicación nueva para el mismo, al adjuntar la base de datos se buscará el archivo en la ubicación antigua. Si se encuentra, se usará el archivo de registro antiguo, sin tener en cuenta si la base de datos se cerró correctamente. No obstante, si el archivo de registro antiguo no se encuentra, la base de datos se cerró correctamente y no hay ninguna cadena de registros activa, al adjuntar se intentará crear un archivo de registro nuevo para la base de datos.  
  
-   Si va a adjuntar el archivo de datos principal es de solo lectura, el [!INCLUDE[ssDE](../../includes/ssnoversion-md.md)] no se puede actualizar la ubicación de registro almacenada en el archivo principal.  
  
  
  
###  <a name="Metadata"></a> Cambios en los metadatos al adjuntar una base de datos  
 Cuando se separa y se vuelve a adjuntar una base de datos de solo lectura, se pierde la información de copia de seguridad acerca de la base diferencial. La *base diferencial* es la copia de seguridad más reciente de todos los datos de una base de datos o de un subconjunto de archivos o grupos de archivos de la misma. Sin la información de la copia de seguridad básica, la base de datos **maestra** deja de estar sincronizada con la base de datos de solo lectura, de modo que las copias de seguridad diferenciales tomadas después pueden proporcionar resultados inesperados. Por lo tanto, si utiliza copias de seguridad diferenciales con una base de datos de solo lectura, deberá establecer una nueva base diferencial actual realizando una copia de seguridad completa después de volver a adjuntar la base de datos. Para obtener más información sobre las copias de seguridad diferenciales, vea [Copias de seguridad diferenciales &#40;SQL Server&#41;](../backup-restore/differential-backups-sql-server.md).  
  
 Al adjuntar, la base de datos se inicia. Normalmente, al adjuntar una base de datos, esta vuelve al mismo estado en el que estaba cuando fue separada o copiada. Sin embargo, las operaciones de adjuntar y separar deshabilitan el encadenamiento de propiedades entre bases de datos para la base de datos. Para obtener más información sobre cómo habilitar el encadenamiento, vea [cross db ownership chaining (opción de configuración del servidor)](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md). Asimismo, TRUSTWORTHY se establece en OFF siempre que la base de datos se adjunta. Para obtener más información sobre cómo establecer TRUSTWORTHY en ON, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
### <a name="backup-and-restore-and-attach"></a>Hacer copias de seguridad y restauración, y adjuntar  
 Al igual que cualquier base de datos que esté total o parcialmente sin conexión, no es posible adjuntar una base de datos con archivos que se estén restaurando. Puede adjuntar la base de datos si detiene la secuencia de restauración. Posteriormente, puede reiniciar la secuencia de restauración.  
  
###  <a name="OtherServerInstance"></a> Adjuntar una base de datos a otra instancia de servidor  
  
> [!IMPORTANT]  
>  Una base de datos creada por una versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede adjuntarse en versiones anteriores.  
  
 Al adjuntar una base de datos a otra instancia de servidor, es posible que tenga que volver a crear una parte o la totalidad de los metadatos de la base de datos, por ejemplo los inicios de sesión y los trabajos, en la otra instancia de servidor; de este modo se proporciona una experiencia coherente a usuarios y aplicaciones. Para obtener más información, vea [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para separar una base de datos**  
  
-   [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
-   [Separar una base de datos](detach-a-database.md)  
  
 **Para adjuntar una base de datos**  
  
-   [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
-   [Adjuntar una base de datos](attach-a-database.md)  
  
-   [sp_attach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-db-transact-sql)  
  
-   [sp_attach_single_file_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql)  
  
 **Para actualizar una base de datos mediante el método de separar y adjuntar**  
  
-   [Actualizar una base de datos mediante Separar y Adjuntar &#40;Transact-SQL&#41;](upgrade-a-database-using-detach-and-attach-transact-sql.md)  
  
 **Para mover una base de datos mediante el método de separar y adjuntar**  
  
-   [Mover una base de datos mediante Separar y Adjuntar &#40;Transact-SQL&#41;](move-a-database-using-detach-and-attach-transact-sql.md)  
  
 **Para eliminar una instantánea de base de datos**  
  
-   [Eliminar una instantánea de base de datos &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Archivos y grupos de archivos de base de datos](database-files-and-filegroups.md)  
  
  
