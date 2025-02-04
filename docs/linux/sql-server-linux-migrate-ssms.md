---
title: Exportación e importación de una base de datos en Linux
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.openlocfilehash: f99ff799ec91ea455cc37bd994c8555330a8ff0f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68105552"
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>Exportación e importación de una base de datos en Linux con SSMS o SqlPackage.exe en Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se muestra cómo usar [SQL Server Management Studio (SSMS )](../ssms/download-sql-server-management-studio-ssms.md) y [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx) para exportar e importar una base de datos en SQL Server en Linux. SSMS y SqlPackage.exe son aplicaciones Windows, así que use esta técnica cuando tenga un equipo Windows que pueda conectarse a una instancia remota de SQL Server en Linux.

Siempre debe instalar y usar la versión más reciente de SQL Server Management Studio (SSMS), tal como se describe en [Usar SSMS en Windows para conectarse a SQL Server en Linux](sql-server-linux-manage-ssms.md).

> [!NOTE]
> Si va a migrar una base de datos de una instancia de SQL Server a otra, se recomienda que use [Copia de seguridad y restauración](sql-server-linux-migrate-restore-database.md).

## <a name="export-a-database-with-ssms"></a>Exportación de una base de datos con SSMS

1. Escriba **Microsoft SQL Server Management Studio** en el cuadro de búsqueda de Windows para iniciar SSMS y, luego, haga clic en la aplicación de escritorio.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. Conéctese a la base de datos de origen en el Explorador de objetos. La base de datos de origen puede estar en la instancia de Microsoft SQL Server que se ejecuta de forma local o en la nube, en Linux, en Windows o en Docker, y en Azure SQL Database o en Azure SQL Data Warehouse.

3. Haga clic con el botón derecho en el Explorador de objetos, seleccione **Tareas** y haga clic en **Exportar aplicación de capa de datos**.

4. En el Asistente para exportar, haga clic en **Siguiente** y, en la pestaña **Configuración**, configure la exportación para guardar el archivo BACPAC en una ubicación de disco local o en un blob de Azure.

5. De forma predeterminada, se exportan todos los objetos de la base de datos. Haga clic en la pestaña **Opciones avanzadas** y elija los objetos de base de datos que quiere exportar.

6. Haga clic en **Siguiente** y, a continuación, en **Finalizar**.

El archivo *.BACPAC se crea correctamente en la ubicación elegida y ya puede importarlo en una base de datos de destino.

## <a name="import-a-database-with-ssms"></a>Importación de una base de datos con SSMS

1. Escriba **Microsoft SQL Server Management Studio** en el cuadro de búsqueda de Windows para iniciar SSMS y, luego, haga clic en la aplicación de escritorio.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. Conéctese al servidor de destino en el Explorador de objetos. El servidor de destino puede estar en la instancia de Microsoft SQL Server que se ejecuta de forma local o en la nube, en Linux, en Windows o en Docker, y en Azure SQL Database o en Azure SQL Data Warehouse.

3. Haga clic con el botón derecho en la carpeta **Bases de datos** del Explorador de objetos y haga clic en **Importar la aplicación de capa de datos**.

4. Para crear la base de datos en el servidor de destino, especifique un archivo BACPAC del disco local o seleccione la cuenta de Azure Storage y el contenedor en el que ha cargado el archivo BACPAC.

5. Proporcione un nombre para la nueva base de datos. Si va a importar una base de datos en Azure SQL Database, establezca la edición de Microsoft Azure SQL Database (nivel de servicio), el tamaño máximo de la base de datos y el objetivo del servicio (nivel de rendimiento).

6. Haga clic en **Siguiente** y en **Finalizar** para importar el archivo BACPAC a una base de datos nueva en el servidor de destino.

El archivo *.BACPAC se importa para crear una base de datos en el servidor de destino especificado.

## <a id="sqlpackage"></a> Opción de línea de comandos SqlPackage

También es posible usar la herramienta de línea de comandos SQL Server Data Tools (SSDT), [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx), para exportar e importar archivos BACPAC.

El siguiente comando de ejemplo exporta un archivo BACPAC:

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

Use el comando siguiente para importar el esquema de la base de datos y los datos de usuario de un archivo .BACPAC:

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>Vea también
Para obtener más información sobre el uso de SSMS, consulte [Uso de SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx). Para obtener más información sobre SqlPackage.exe, consulte la [documentación de referencia de SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx).
