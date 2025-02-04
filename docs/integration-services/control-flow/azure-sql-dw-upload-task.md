---
title: Tarea de carga de Azure SQL DW | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPDWUPTASK.F1
- sql14.dts.designer.afpdwuptask.f1
ms.assetid: eef82c89-228a-4dc7-9bd0-ea00f57692f5
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: 584bd3a22c24dfccf8fab562202d66ce8689b55b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947196"
---
# <a name="azure-sql-dw-upload-task"></a>Tarea de carga de Azure SQL DW

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



La **tarea de carga de Azure SQL DW** permite que un paquete SSIS copie datos tabulares a Azure SQL Data Warehouse (DW) desde el sistema de archivos o Azure Blob Storage.
La tarea usa PolyBase para mejorar el rendimiento, tal como se describe en el artículo [Azure SQL Data Warehouse Loading Patterns and Strategies](https://blogs.msdn.microsoft.com/sqlcat/2017/05/17/azure-sql-data-warehouse-loading-patterns-and-strategies/) (Patrones y estrategias de carga de Azure SQL Data Warehouse).
El formato de archivo de origen de datos que se admite actualmente es texto delimitado en codificación UTF8.
Al copiar desde el sistema de archivos, los datos primeros se cargarán a Azure Blob Storage para almacenamiento provisional y luego a Azure SQL DW. Por lo tanto, se necesita una cuenta de Azure Blob Storage.

La **tarea de carga de Azure SQL DW** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para agregar una **tarea de carga de Azure SQL DW**, arrástrela desde el cuadro de herramientas de SSIS y suéltela en el lienzo de diseño. A continuación, haga doble clic o clic con el botón secundario y haga clic en **Editar** para que se muestre el cuadro de diálogo de edición.

En la página **General** , configure las propiedades siguientes.

**SourceType** especifica el tipo de almacén de datos de origen. Seleccione uno de estos tipos:

* **FileSystem:** los datos de origen residen en el sistema de archivos local.
* **BlobStorage:** los datos de origen residen en Azure Blob Storage.

Estas son las propiedades de cada tipo de origen.

### <a name="filesystem"></a>FileSystem

Campo|Descripción
-----|-----------
LocalDirectory|Especifica el directorio local que contiene los archivos de datos que se van a cargar.
Recursively|Especifica si los subdirectorios se deben buscar de forma recursiva.
FileName|Especifica un filtro de nombre para seleccionar archivos con un determinado patrón de nombre. Por ejemplo: MiHoja*.xsl\* incluirá archivos como MiHoja001.xsl y MiHojaABC.xslx.
RowDelimiter|Especifica los caracteres que marcan el final de cada fila.
ColumnDelimiter|Especifica uno o más caracteres que marcan el final de cada columna. Por ejemplo: &#124; (barra vertical), \t (tabulación), ' (comilla simple), " (comilla doble) y 0x5c (barra diagonal inversa).
IsFirstRowHeader|Especifica si la primera fila de cada archivo de datos contiene nombres de columna en lugar de datos reales.
AzureStorageConnection|Especifica un administrador de conexiones de Azure Storage.
BlobContainer|Especifica el nombre del contenedor de blob en el que se cargarán los datos locales para retransmitirlos a Azure DW mediante PolyBase. Si no existe ningún contenedor, se creará uno.
BlobDirectory|Especifica el directorio de blob (estructura jerárquica virtual) en el que se cargarán los datos locales para retransmitirlos a Azure DW mediante PolyBase.
RetainFiles|Especifica si se deben conservar los archivos cargados en Azure Storage.
CompressionType|Especifica el formato de compresión que se usará al cargar archivos en Azure Storage. El origen local no se verá afectado.
CompressionLevel|Especifica el nivel de compresión que se usará para el formato de compresión.
AzureDwConnection|Especifica un administrador de conexión de ADO.NET para Azure SQL DW.
TableName|Especifica el nombre de la tabla de destino. Elija un nombre de tabla existente o cree uno eligiendo **\<Nueva tabla ...>** .
TableDistribution|Especifica el método de distribución para la tabla nueva. Se aplica si se especifica un nuevo nombre de tabla para **TableName**.
HashColumnName|Especifica la columna usada para la distribución de la tabla hash. Se aplica si **HASH** se ha especificado para **TableDistribution**.

### <a name="blobstorage"></a>BlobStorage

Campo|Descripción
-----|-----------
AzureStorageConnection|Especifica un administrador de conexiones de Azure Storage.
BlobContainer|Especifica el nombre del contenedor de blob en el que residen los datos de origen.
BlobDirectory|Especifica el directorio de blobs (estructura jerárquica virtual) en el que residen los datos de origen.
RowDelimiter|Especifica los caracteres que marcan el final de cada fila.
ColumnDelimiter|Especifica uno o más caracteres que marcan el final de cada columna. Por ejemplo: &#124; (barra vertical), \t (tabulación), ' (comilla simple), " (comilla doble) y 0x5c (barra diagonal inversa).
CompressionType|Especifica el formato de compresión que se usa para los datos de origen.
AzureDwConnection|Especifica un administrador de conexión de ADO.NET para Azure SQL DW.
TableName|Especifica el nombre de la tabla de destino. Elija un nombre de tabla existente o cree uno eligiendo **\<Nueva tabla ...>** .
TableDistribution|Especifica el método de distribución para la tabla nueva. Se aplica si se especifica un nuevo nombre de tabla para **TableName**.
HashColumnName|Especifica la columna usada para la distribución de la tabla hash. Se aplica si **HASH** se ha especificado para **TableDistribution**.

Se mostrará otra página **Asignaciones** en función de si quiere copiar los datos en una tabla nueva o en una existente.
En el primer caso, configure las columnas de origen que se van a asignar y los nombres correspondientes en la tabla de destino que se creará.
En el segundo caso, configure las relaciones de asignación entre las columnas de origen y las de destino.

En la página **Columnas** , configure las propiedades de tipos de datos para cada columna de origen.

La página **T-SQL** muestra la instrucción T-SQL usada para cargar datos de Azure Blob Storage a Azure SQL DW.
La instrucción T-SQL se genera automáticamente a partir de configuraciones de otras páginas y se ejecuta como parte de la tarea.
Puede editar manualmente la instrucción T-SQL generada para adaptarla a sus necesidades concretas haciendo clic en el botón **Editar** .
Puede revertirla para volver a la que se genera automáticamente más tarde haciendo clic en el botón **Restablecer** .
