---
title: 'Ejemplo: restauración por etapas de la base de datos (modelo de recuperación simple) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 9834b14a-4e56-4654-b190-c2a38624b6b4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 01a51e073fc8b4f135beac1a7c98a12549093df4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68089675"
---
# <a name="example-piecemeal-restore-of-database-simple-recovery-model"></a>Ejemplo: Restauración por etapas de base de datos (modelo de recuperación simple)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En una secuencia de restauración por etapas restaura y recupera una base de datos en fases en el nivel del grupo de archivos, empezando con los grupos de archivos principales y todos los secundarios de lectura/escritura.  
  
 En este ejemplo, la base de datos `adb` se restaura en un nuevo equipo después de un desastre. La base de datos utiliza el modelo de recuperación simple. Antes del desastre, todos los grupos de archivos están en línea. Los grupos de archivos `A` y `C` son de lectura/escritura, y el grupo de archivos `B` es de solo lectura. El grupo de archivos `B` pasó a ser de solo lectura antes de la copia de seguridad parcial más reciente, que contiene el grupo de archivos principal y los grupos de archivos secundarios de lectura/escritura, `A` y `C`. Después de que el grupo de archivos `B` pasara a ser de solo lectura, se realizó una copia de seguridad de archivos independiente del grupo de archivos `B` .  
  
## <a name="restore-sequences"></a>Secuencias de restauración  
  
1.  Restauración parcial del grupo de archivos principal y los grupos de archivos `A` y `C`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A',FILEGROUP='C'   
       FROM partial_backup   
       WITH PARTIAL, RECOVERY;  
  
    ```  
  
     En este momento, los grupos de archivos principal, `A` y `C` están en línea. Todos los archivos del grupo de archivos `B` están pendientes de recuperación y el grupo de archivos está sin conexión.  
  
2.  Restauración con conexión del grupo de archivos `B`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY;  
  
    ```  
  
     Todos los grupos de archivos están ahora en línea.  
  
## <a name="additional-examples"></a>Otros ejemplos  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas de la base de datos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de lectura/escritura &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Consulte también  
 [Restauración con conexión &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
