---
title: Desarrollo e implementación de bases de datos de SQL Server para Linux | Microsoft Docs
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.openlocfilehash: b98980837f6dce2ebd9f39be142b816f37f16cd8
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077404"
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Uso de Visual Studio para crear bases de datos para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Data Tools (SSDT) convierte Visual Studio en un eficaz entorno de desarrollo y administración del ciclo de vida de bases de datos (DLM) para SQL Server en Linux. Puede desarrollar, compilar, probar y publicar la base de datos desde un proyecto controlado por código fuente, igual que desarrolla el código de la aplicación.

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Instalación de Visual Studio y SQL Server Data Tools

1. Si aún no ha instalado Visual Studio en el equipo Windows, [Descarga e instalación de Visual Studio]. Si no tiene una licencia de Visual Studio, Visual Studio Community Edition es un IDE gratuito con todas las características para estudiantes, código abierto y desarrolladores individuales.

2. Durante la instalación de Visual Studio, seleccione **Personalizada** en la opción **Elija el tipo de instalación**. Haga clic en **Siguiente**.

3. Seleccione **Microsoft SQL Server Data Tools**, **Git para Windows** y **Extensión de GitHub para Visual Studio** en la lista de selección de características.

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. Continúe y finalice la instalación de Visual Studio. Puede tardar unos minutos.

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>Actualización de SQL Server Data Tools a la versión SSDT 17.0 RC

SQL Server en Linux es compatible con la versión SSDT 17.0 RC o posterior.

* [Descarga e instalación de SSDT 17.0 RC2](https://go.microsoft.com/fwlink/?linkid=837939).

## <a name="create-a-new-database-project-in-source-control"></a>Creación de un nuevo proyecto de base de datos en el control de código fuente

1. Inicie Visual Studio.

2. Seleccione **Team Explorer** en el menú **Ver**. 

3. Haga clic en **Nuevo** en la sección **Repositorio de Git local** de la página **Conectar**.

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. Haga clic en **Crear**. Una vez creado el repositorio de Git local, haga doble clic en **SSDTRepo**.

4. Haga clic en **Nuevo** en la sección **Soluciones**. Seleccione **SQL Server** en el nodo **Otros lenguajes** del cuadro de diálogo **Nuevo proyecto**.

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. Escriba **TutorialDB** como nombre y haga clic en **Aceptar** para crear un nuevo proyecto de base de datos.

## <a name="create-a-new-table-in-the-database-project"></a>Creación de una nueva tabla en el proyecto de base de datos

1. Seleccione **Explorador de soluciones** en el menú **Ver**.

2. Abra el menú Proyecto de base de datos al hacer clic con el botón derecho en **TutorialDB** en el Explorador de soluciones.

3. Seleccione **Tabla** en **Agregar**.

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. Con el diseñador de tablas, agregue dos columnas, Nombre `nvarchar(50)` y Ubicación `nvarchar(50)`, como se muestra en la imagen. SSDT genera el script `CREATE TABLE` a medida que se agregan las columnas en el diseñador.

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. Guarde el archivo **Table1.sql**.

## <a name="build-and-validate-the-database"></a>Compilación y validación de la base de datos

1. Abra el menú Proyecto de base de datos en **TutorialDB** y seleccione **Compilar**. SSDT compila archivos de código fuente .sql del proyecto y un archivo de paquete de aplicación de capa de datos (dacpac). Este se puede usar para publicar una base de datos en la instancia de SQL Server en Linux. 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. Compruebe el mensaje de compilación correcta de la ventana **Salida** de Visual Studio. 

## <a name="publish-the-database-to-sql-server-instance-on-linux"></a>Publicación de la base de datos en la instancia de SQL Server en Linux

1. Abra el menú Proyecto de base de datos en **TutorialDB** y seleccione **Publicar**.

2. Haga clic en **Editar** para seleccionar la instancia de SQL Server en Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. En el cuadro de diálogo de conexión, escriba la dirección IP o el nombre de host de la instancia de SQL Server en Linux, el nombre de usuario y la contraseña.

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. Haga clic en el botón **Publicar** del cuadro de diálogo.

5. Compruebe el estado de publicación en la ventana **Operaciones de herramientas de datos**.

6. Haga clic en **Ver resultados** o **Ver script** para ver los detalles del resultado de la publicación de la base de datos en SQL Server en Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

Ha creado correctamente una base de datos nueva en la instancia de SQL Server en Linux y ha aprendido los aspectos básicos del desarrollo de una base de datos con un proyecto de base de datos controlado por código fuente.

## <a name="next-steps"></a>Pasos siguientes

Si no está familiarizado con T-SQL, vea [Tutorial: Escribir instrucciones Transact-SQL] y [Referencia de Transact-SQL (motor de base de datos)].

Para obtener más información sobre el desarrollo de una base de datos con SQL Data Tools, vea los [documentos de MSDN sobre SSDT]

[Descarga e instalación de Visual Studio]: https://www.visualstudio.com/downloads/
[Download and Install SSDT]:https://aka.ms/ssdt-download
[Documentos de MSDN sobre SSDT]: https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx
[Tutorial: Escribir instrucciones Transact-SQL]: https://msdn.microsoft.com/library/ms365303.aspx
[Referencia de Transact-SQL (motor de base de datos)]: https://msdn.microsoft.com/library/bb510741.aspx
