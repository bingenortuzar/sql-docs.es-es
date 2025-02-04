---
title: Recuperación de bases de datos acelerada | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: kfarlee
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- accelerated database recovery [SQL Server], recovery-only
- database recovery [SQL Server]
author: mashamsft
ms.author: mathoma
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d825c7db4789ec1421cf43acd5897e932c7fa29a
ms.sourcegitcommit: 183d622fff36a22b882309378892010be3bdcd52
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/19/2019
ms.locfileid: "71130544"
---
# <a name="manage-accelerated-database-recovery"></a>Administrar la recuperación de bases de datos acelerada

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

## <a name="enabling-and-controlling-adr"></a>Habilitar y controlar la recuperación de bases de datos acelerada

La recuperación de bases de datos acelerada (ADR) está desactivada de forma predeterminada en [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] y se puede controlar mediante la sintaxis de DDL:
```sql
ALTER DATABASE [DB] SET ACCELERATED_DATABASE_RECOVERY = {ON | OFF}
[(PERSISTENT_VERSION_STORE_FILEGROUP = { filegroup name }) ];

```

Use esta sintaxis para controlar si la característica está activada o desactivada, y para designar un grupo de archivos específico para los datos del *almacén de versiones persistentes* (PVS). Si no se especifica ningún grupo de archivos, el PVS se almacenará en el grupo de archivos PRIMARY.

## <a name="managing-the-persistent-version-store-filegroup"></a>Administrar el grupo de archivos del almacén de versiones persistentes
La característica ADR consiste en tener versiones de los cambios y conservar distintas versiones de los elementos de datos en el PVS.
Hay algunas consideraciones que hay que tener en cuenta con respecto a la ubicación del PVS y cómo administrar el tamaño de los datos en el PVS.

### <a name="to-enable-adr-without-specifying-a-filegroup"></a>Para habilitar ADR sin especificar un grupo de archivos

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON;
GO
```

En este caso, cuando no se especifica el grupo de archivos del PVS, el grupo de archivos `PRIMARY` contiene los datos del PVS.

### <a name="to-enable-adr-and-specify-that-the-pvs-should-be-stored-in-the-versionstorefg-filegroup"></a>Para habilitar ADR y especificar que el PVS se almacene en el grupo de archivos [VersionStoreFG]

Antes de ejecutar este script, cree el grupo de archivos.

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON
(PERSISTENT_VERSION_STORE_FILEGROUP = [VersionStoreFG])
```

### <a name="to-disable-the-adr-feature"></a>Para deshabilitar la característica ADR

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = OFF;
GO
```

Incluso después de deshabilitar la característica ADR, habrá versiones almacenadas en el almacén de versiones persistentes que sigan siendo necesarias en el sistema para la reversión lógica.

### <a name="change-the-location-of-the-pvs-to-a-different-filegroup"></a>Cambiar la ubicación del PVS a otro grupo de archivos

Es posible que tenga que trasladar la ubicación del PVS a otro grupo de archivos por diversos motivos. Por ejemplo, el PVS puede requerir más espacio o un almacenamiento más rápido.

Cambiar la ubicación del PVS es un proceso de tres pasos.

1. Desactive la característica ADR.

   ```sql
   ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = OFF;
   GO
   ```

2. Espere a que se liberen todas las versiones almacenadas en el PVS.

   Para poder activar ADR con una nueva ubicación para el almacén de versiones persistentes, asegúrese primero de que toda la información de versiones se ha purgado de la ubicación anterior del PVS. Para forzar que se produzca la limpieza, ejecute el comando:

   ```sql
   EXEC sys.sp_persistent_version_store_cleanup [database name]
   ```

   El procedimiento almacenado `sys.sp_persistent_version_store_cleanup` es sincrónico, lo que significa que no se completará hasta que se haya limpiado toda la información de versiones del PVS actual.  Una vez que se haya completado, compruebe que se ha quitado la información de la versión; para ello, haga una consulta a `sys.dm_persistent_version_store_stats` de DMV y examine el valor de `persistent_version_store_size_kb`.

   ```sql
   SELECT DB_Name(database_id), persistent_version_store_size_kb 
   FROM sys.dm_tran_persistent_version_store_stats where database_id = [MyDatabaseID]
   ```

   Cuando el valor de persistent_version_store_size_kb es 0, puede volver a habilitar la característica ADR; para ello, configure que el PVS se encuentre en el nuevo grupo de archivos.

1. Active la característica ADR mediante la especificación de la nueva ubicación para el PVS.

   ```sql
   ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON
   (PERSISTENT_VERSION_STORE_FILEGROUP = [VersionStoreFG])
   ```

## <a name="troubleshooting"></a>Solucionar problemas

Consulte `sys.dm_tran_persistent_version_store_stats` para comprobar los tamaños de PVS.

Comprobar tamaño de `% of DB`. Tenga en cuenta también la diferencia respecto al tamaño normal.

El PVS se considera grande si es considerablemente mayor que la línea de base o si está cerca del 50 % del tamaño de la base de datos. 

1. Recupere `oldest_active_transaction_id` y compruebe si esta transacción ha estado activa durante un tiempo muy prolongado mediante una consulta a `sys.dm_tran_database_transactions` en función del identificador de la transacción.

   Las transacciones activas impiden la limpieza del PVS.

1. Si la base de datos forma parte de un grupo de disponibilidad, compruebe `secondary_low_water_mark`. Es el mismo que el `low_water_mark_for_ghosts` indicado por `sys.dm_hadr_database_replica_states`. Consulte `sys.dm_hadr_database_replica_states` para ver si una de las réplicas está reteniendo este valor atrás, ya que esto también evitará la limpieza del PVS.
1. Compruebe `min_transaction_timestamp` (o `online_index_min_transaction_timestamp` si el PVS en línea está en mantenimiento) y, en función de eso, compruebe `sys.dm_tran_active_snapshot_database_transactions` para que la columna `transaction_sequence_num` encuentre la sesión que tiene la transacción de instantáneas antigua que mantiene la limpieza del PVS.
1. Si no se aplica ninguno de los anteriores, significa que la limpieza se mantiene mediante transacciones anuladas. Compruebe por última vez `aborted_version_cleaner_last_start_time` y `aborted_version_cleaner_last_end_time` para ver si se ha completado la limpieza de la transacción anulada. `oldest_aborted_transaction_id` debería moverse más arriba después de completarse la limpieza de la transacción anulada.
1. Si la transacción anulada no se ha completado correctamente, consulte en el registro de errores si hay mensajes que notifican problemas de `VersionCleaner`.
