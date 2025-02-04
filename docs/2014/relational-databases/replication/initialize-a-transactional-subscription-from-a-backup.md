---
title: Inicializar una suscripción transaccional desde una copia de seguridad (programación de replicación Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7e7fb32de254729c4173fab260e5797db5f2cc2f
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793305"
---
# <a name="initialize-a-transactional-subscription-from-a-backup-replication-transact-sql-programming"></a>Inicializar una suscripción transaccional desde una copia de seguridad (programación de la replicación con Transact-SQL)
  Aunque una suscripción a una publicación transaccional se inicializa normalmente con una instantánea, también se puede inicializar desde una copia de seguridad mediante procedimientos almacenados de replicación. Para obtener más información, consulte [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>Para inicializar una suscripción transaccional desde una copia de seguridad  
  
1.  En una publicación existente, asegúrese de que la publicación admite la capacidad de inicializarse desde la copia de seguridad ejecutando [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) en la base de datos de publicación del publicador. Tenga en cuenta el valor de **allow_initialize_from_backup** en el conjunto de resultados.  
  
    -   Si el valor es **1**, la publicación admite esta funcionalidad.  
  
    -   Si el valor es **0**, ejecute [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) en el Publicador de la base de datos de publicación. Especifique un valor de **allow_initialize_from_backup** para  **\@propiedad** y un valor de `true` para  **\@valor**.  
  
2.  Para una nueva publicación, ejecute [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) en el Publicador de la base de datos de publicación. Especifique un valor de `true` para **allow_initialize_from_backup**. Para obtener más información, vea [Crear una suscripción](publish/create-a-publication.md).  
  
    > [!WARNING]  
    >  Para evitar perder los datos del suscriptor, al utilizar **sp_addpublication** con `@allow_initialize_from_backup = N'true'`, utilice siempre `@immediate_sync = N'true'`.  
  
3.  Cree una copia de seguridad de la base de datos de publicación con la instrucción [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
4.  Restaure la copia de seguridad en el suscriptor con la instrucción [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
5.  En la base de datos de publicación del publicador, ejecute el procedimiento almacenado [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql). Especifique los parámetros siguientes:  
  
    -   **\@sync_type** -un valor de **inicializar con copia de seguridad**.  
  
    -   **\@backupdevicetype** -el tipo de dispositivo de copia de seguridad: **lógico** (valor predeterminado), **disco**, o **cinta**.  
  
    -   **\@backupdevicename** -el dispositivo de copia de seguridad físico o lógico que se usará para la restauración.  
  
         Para una unidad lógica, especifique el nombre del dispositivo de copia de seguridad especificado cuando se usó **sp_addumpdevice** para crear el dispositivo.  
  
         Para un dispositivo físico, especifique una ruta de acceso y un nombre de archivo completos, como `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\BACKUP\Mybackup.dat'` o `TAPE = '\\.\TAPE0'`.  
  
    -   (Opcional)  **\@contraseña** -una contraseña que proporcionó cuando se creó el conjunto de copia de seguridad.  
  
    -   (Opcional)  **\@mediapassword** -una contraseña que proporcionó cuando se formatea el conjunto de medios.  
  
    -   (Opcional)  **\@fileidhint** -identificador de la copia de seguridad para restaurar. Por ejemplo, **1** indica el primer conjunto de copia de seguridad del medio de copia de seguridad y **2** indica el segundo conjunto de copia de seguridad.  
  
    -   (Opcional para los dispositivos de cinta)  **\@descargar** -especifique un valor de **1** (valor predeterminado) si la cinta debe descargarse de la unidad una vez completada la restauración y **0** si no debe ser descargado .  
  
6.  (Opcional) Para una suscripción de extracción, ejecute [sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql) y [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) en el suscriptor de la base de datos de suscripción. Para obtener más información, consulte [Create a Pull Subscription](create-a-pull-subscription.md).  
  
7.  (Opcional) Inicio el Agente de distribución. Para obtener más información, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) o [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
## <a name="see-also"></a>Vea también  
 [Copiar bases de datos con Copias de seguridad y restauración](../databases/copy-databases-with-backup-and-restore.md)   
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
