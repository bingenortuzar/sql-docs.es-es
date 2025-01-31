---
title: Configuración de la replicación de SQL Server de recursos compartidos de carpetas de instantáneas en Linux
description: En este artículo, se describe cómo configurar una replicación de SQL Server de recursos compartidos de carpetas de instantáneas en Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6959b2073871f70fb33823b50419c208a23df2dd
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68093184"
---
# <a name="configure-replication-with-non-default-ports"></a>Configurar la replicación con puertos no predeterminados

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Puede configurar la replicación con SQL Server en instancias de Linux que escuchen en cualquier puerto configurado con la opción network.tcpport mssql-conf. Si se cumplen las condiciones siguientes, es necesario anexar el puerto al nombre del servidor durante la configuración:

1. En la configuración de replicación, se usa una instancia de SQL Server en Linux.
2. Cualquier instancia (Windows o Linux) escucha en un puerto no predeterminado. 

El nombre del servidor de una instancia se puede averiguar si se ejecuta @@servername en la instancia.

## <a name="examples"></a>Ejemplos

“Servidor1” escucha en el puerto 1500 en Linux. Para configurar “Servidor1” para la distribución, ejecute `sp_adddistributor` con `@distributor`. Por ejemplo: 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

“Servidor1” escucha en el puerto 1500 en Linux. Para configurar un publicador para el distribuidor, ejecute `sp_adddistpublisher` con `@publisher`. Por ejemplo:

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

“Servidor2” escucha en el puerto 6549 en Linux. Para configurar “Servidor2” como un suscriptor, ejecute `sp_addsubscription` con `@subscriber`. Por ejemplo:

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

“Servidor3” escucha en el puerto 6549 en Windows con el nombre de servidor “Servidor3” y el nombre de instancia “MSSQL2017”. Para configurar “Servidor3” como un suscriptor, ejecute `sp_addsubscription` con `@subscriber`. Por ejemplo:

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>Pasos siguientes

[Conceptos: Replicación de SQL Server en Linux](sql-server-linux-replication.md)

[Procedimientos almacenados de replicación](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)

