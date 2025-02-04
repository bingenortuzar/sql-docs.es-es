---
title: Compresión de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- page compression [Database Engine]
- indexes [SQL Server], compressed
- compressed indexes [SQL Server]
- storage compression [Database Engine]
- tables [SQL Server], compressed
- storage [SQL Server], compressed
- compression [SQL Server]
- row compression [Database Engine]
- compression [SQL Server], about compressed tables and indexes
- data compression [Database Engine]
- compressed tables [SQL Server]
ms.assetid: 5f33e686-e115-4687-bd39-a00c48646513
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c52fa04c46ff41ce67094599a6a2f3f5074e8f03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62873555"
---
# <a name="data-compression"></a>Data Compression
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite la compresión de fila y de página para las tablas e índices de almacén de filas, y admite la compresión de almacén de columnas y de archivo de almacén de columnas para las tablas e índices de almacén de columnas.  
  
 Para las tablas e índices de almacén de filas, use la característica de compresión de datos como ayuda para reducir el tamaño de la base de datos. Además de ahorrar espacio, la compresión de datos puede contribuir a mejorar el rendimiento de las cargas de trabajo que hacen un uso intensivo de las operaciones de E/S porque los datos se almacenan en menos páginas y las consultas deben leer menos páginas del disco. No obstante, se requieren recursos de CPU adicionales en el servidor de base de datos para comprimir y descomprimir los datos, mientras los datos se intercambian con la aplicación. La compresión de fila y de página se puede configurar en los objetos de base de datos siguientes:  
  
-   Una tabla entera que está almacenada como un montón.  
  
-   Una tabla entera que está almacenada como un índice clúster.  
  
-   Un índice no clúster entero.  
  
-   Una vista indizada entera.  
  
-   Para las tablas e índices con particiones, la opción de compresión se puede configurar para cada partición y las diferentes particiones de un objeto no tienen por qué tener la misma configuración de compresión.  
  
 Para las tablas e índices de almacén de columnas, todos los índices y tablas de almacén de columnas usan siempre la compresión de almacén de columnas, que no es configurable por el usuario. Use la compresión de archivo de almacén de columnas para reducir más el tamaño de datos en los casos en que pueda permitirse emplear tiempo y recursos de CPU adicionales para almacenar y recuperar los datos.  La compresión de archivo de almacén de columnas se puede configurar en los objetos de base de datos siguientes:  
  
-   Una tabla entera de almacén de columnas o un índice entero de almacén de columnas en clúster.  Puesto que una tabla de almacén de columnas se almacena como índice de almacén de columnas en clúster, ambos métodos tienen los mismos resultados.  
  
-   Un índice entero de almacén de columnas no clúster.  
  
-   Para las tablas de almacén de columnas y los índices de almacén de columnas con particiones, la opción de compresión de archivo se puede configurar para cada partición y las diferentes particiones no tienen por qué tener la misma configuración de compresión de archivo.  
  
## <a name="considerations-for-when-you-use-row-and-page-compression"></a>Consideraciones sobre el uso de la compresión de filas y páginas  
 Cuando utilice la compresión de filas y páginas, tenga en cuenta las consideraciones siguientes:  
  
-   Los detalles de la compresión de datos se pueden cambiar sin previo aviso en los Service Pack o versiones posteriores.  
  
-   La compresión no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   La compresión no está disponible para las tablas del sistema.  
  
-   La compresión puede permitir que se almacenen más filas en una página, pero no cambia el tamaño máximo de filas de una tabla o índice.  
  
-   Una tabla no se puede habilitar para su compresión cuando el tamaño máximo de filas más la sobrecarga de compresión supera el tamaño máximo de filas de 8060 bytes. Por ejemplo, una tabla que tiene las columnas c1`char(8000)` y c2`char(53)` no se puede comprimir debido a la sobrecarga de compresión adicional. Cuando se utiliza el formato de almacenamiento vardecimal, la comprobación del tamaño de filas se realiza cuando se habilita el formato. Para la compresión de filas y páginas, la comprobación del tamaño de filas se realiza cuando el objeto se comprime inicialmente, y después se comprueba cuando se inserta o modifica cada fila. La compresión exige las dos reglas siguientes:  
  
    -   Una actualización a un tipo de longitud fija siempre debe tener éxito.  
  
    -   La deshabilitación de la compresión de datos siempre debe tener éxito. Aunque la fila comprimida quepa en la página, lo que significa que tiene menos de 8060 bytes, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] evita actualizaciones que no cabrían en la fila al descomprimirla.  
  
-   Cuando se especifica una lista de particiones, el tipo de compresión se puede establecer en ROW, PAGE o NONE en particiones individuales. Si no se especifica la lista de particiones, todas las particiones se establecen con la propiedad de compresión de datos que se especifica en la instrucción. Cuando se crea una tabla o índice, la compresión de datos se establece en NONE, a menos que se especifique lo contrario. Cuando se modifica una tabla, se conserva la compresión existente, a menos que se especifique lo contrario.  
  
-   Si se especifica una lista de particiones o una partición que están fuera del intervalo, se generará un error.  
  
-   Los índices no clúster no heredan la propiedad de compresión de la tabla. Para comprimir índices, se debe establecer explícitamente la propiedad de compresión de los índices. De forma predeterminada, el valor de compresión de índices se establecerá en NONE cuando se crea el índice.  
  
-   Cuando se crea un índice clúster en un montón, el índice clúster hereda el estado de compresión del montón, a menos que se especifique otro estado de compresión.  
  
-   Cuando un montón se configura para la compresión de nivel de página, las páginas solo reciben la compresión de nivel de página de las formas siguientes:  
  
    -   Los datos se importan de forma masiva con las optimizaciones masivas habilitadas.  
  
    -   Los datos se insertan utilizando la sintaxis INSERT INTO ... La sintaxis WITH (TABLOCK) y la tabla no tienen ningún índice no agrupado.  
  
    -   Una tabla se vuelve a generar ejecutando la instrucción ALTER TABLE... REBUILD con la opción de compresión PAGE.  
  
-   Las nuevas páginas asignadas en un montón como parte de las operaciones DML no usarán la compresión PAGE hasta que se vuelva a generar el montón. Para volver a generar el montón, quite y vuelva a aplicar la compresión, o cree y quite un índice clúster.  
  
-   El cambio del valor de compresión de un montón requiere que todos los índices no clúster de la tabla se vuelvan a generar de modo que tengan punteros a las nuevas ubicaciones de fila en el montón.  
  
-   Puede habilitar o deshabilitar la compresión ROW o PAGE conectado o sin conexión. La habilitación de la compresión en un montón es de un solo subproceso para una operación en línea.  
  
-   Los requisitos de espacio en disco para habilitar o deshabilitar la compresión de filas o páginas son los mismos que los necesarios para crear o volver a generar un índice. Para los datos con particiones, puede reducir el espacio que se requiere habilitando o deshabilitando la compresión para una partición cada vez.  
  
-   Para determinar el estado de compresión de particiones en una tabla con particiones, consulte la columna data_compression de la vista de catálogo sys.partitions.  
  
-   Cuando se comprimen índices, las páginas de nivel de hoja se pueden comprimir tanto con la compresión de filas como con la compresión de páginas. Las páginas que no están en el nivel hoja no reciben la compresión de páginas.  
  
-   Debido a su tamaño, los tipos de datos de valores grandes suelen almacenarse independientemente de los datos de fila normales en páginas con un fin específico. La compresión de datos no está disponible para los datos que se almacenan independientemente.  
  
-   Las tablas que implementaron el formato de almacenamiento vardecimal en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] conservarán ese valor cuando se actualicen. Puede aplicar la compresión de filas a una tabla que tenga el formato de almacenamiento vardecimal. Sin embargo, como la compresión de filas es un superconjunto del formato de almacenamiento vardecimal, no hay ninguna razón para conservar el formato de almacenamiento vardecimal. Los valores decimales no obtienen una compresión adicional cuando se combina el formato de almacenamiento vardecimal con la compresión de filas. Puede aplicar la compresión de páginas a una tabla que tenga el formato de almacenamiento vardecimal; sin embargo, es probable que las columnas con formato de almacenamiento vardecimal no consigan una compresión adicional.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite el formato de almacenamiento vardecimal; sin embargo, como la compresión de nivel de fila consigue los mismos objetivos, el formato de almacenamiento vardecimal ha quedado desusado. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="using-columnstore-and-columnstore-archive-compression"></a>Usar la compresión de almacén de columnas y de archivo de almacén de columnas  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de la [versión actual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
### <a name="basics"></a>Conceptos básicos  
 Las tablas y los índices de almacén de columnas siempre se almacenan con compresión de almacén de columnas. El tamaño de los datos de almacén de columnas se puede reducir más configurando una compresión adicional denominada compresión de archivo.  Para realizar la compresión de archivo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta el algoritmo de compresión de Microsoft XPRESS en los datos. La compresión de archivo se agrega o se quita mediante los tipos de compresión de datos siguientes:  
  
-   Use la compresión de datos de `COLUMNSTORE_ARCHIVE` para comprimir los datos de almacén de columnas con la compresión de archivo.  
  
-   Use la compresión de datos de **COLUMNSTORE** para descomprimir la compresión de archivo. Estos datos resultantes seguirán comprimiéndose con la compresión de almacén de columnas.  
  
 Para agregar la compresión de archivo, use [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql) o [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql) con la opción REBUILD y DATA COMPRESSION = COLUMNSTORE.  
  
 Ejemplos:  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE ON PARTITIONS (2,4)) ;  
  
```  
  
 Para quitar la compresión de archivo y restaurar los datos a la compresión de almacén de columnas, use [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql) o [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql) con la opción REBUILD y DATA COMPRESSION = COLUMNSTORE.  
  
 Ejemplos:  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (2,4) ) ;  
  
```  
  
 En el ejemplo siguiente se establece la compresión de datos a almacén de columnas en algunas particiones y a archivo de almacén de columnas en otras particiones.  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (  
    DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (4,5),  
    DATA COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (1,2,3)  
) ;  
```  
  
### <a name="performance"></a>Rendimiento  
 Al comprimir los índices de almacén de columnas con la compresión de archivo, el índice se ejecutará más lentamente que los índices de almacén de columnas que no tienen la compresión de archivo.  Use la compresión de archivo solo cuando se puede permitirse emplear tiempo y recursos de CPU adicionales para comprimir y recuperar los datos.  
  
 La contrapartida del rendimiento más lento es el almacenamiento reducido, que sirve para los datos que no son de acceso frecuente. Por ejemplo, si tiene una partición para cada mes de datos y la mayor parte de la actividad tiene lugar en los meses más recientes, podría archivar los meses más antiguos para reducir los requisitos de almacenamiento.  
  
### <a name="metadata"></a>Metadatos  
 Las vistas del sistema siguientes contienen información sobre la compresión de datos para los índices clúster:  
  
-   [Sys.Indexes &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql) : la `type` y `type_desc` columnas incluyen CLUSTERED COLUMNSTORE y NONCLUSTERED COLUMNSTORE.  
  
-   [Sys.Partitions &#40;Transact-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-partitions-transact-sql) : la `data_compression` y `data_compression_desc` columnas incluyen COLUMNSTORE y COLUMNSTORE_ARCHIVE.  
  
 El procedimiento [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql) no se aplica a los índices de almacén de columnas.  
  
## <a name="how-compression-affects-partitioned-tables-and-indexes"></a>Cómo afecta la compresión a tablas e índices con particiones  
 Cuando use la compresión de datos con tablas e índices con particiones, tenga en cuenta las consideraciones siguientes:  
  
-   Cuando se divide una partición utilizando la instrucción ALTER PARTITION, ambas particiones heredan el atributo de compresión de datos de la partición original.  
  
-   Cuando se combinan dos particiones, la partición resultante hereda el atributo de compresión de datos de la partición de destino.  
  
-   Para cambiar una partición, la propiedad de compresión de datos de la partición debe coincidir con la propiedad de compresión de la tabla.  
  
-   Hay dos variaciones de sintaxis que se pueden utilizar para modificar la compresión de una tabla o índice con particiones:  
  
    -   La sintaxis siguiente vuelve a generar solo la partición a la que se hace referencia:  
  
        ```  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  <option>)  
        ```  
  
    -   La sintaxis siguiente vuelve a generar la tabla completa utilizando el valor de compresión existente para las particiones a las que no se haga referencia:  
  
        ```  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = ALL   
        WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(<range>),  
        ... )  
        ```  
  
     Los índices con particiones siguen el mismo principio mediante el uso de ALTER INDEX.  
  
-   Cuando se quita un índice clúster, las particiones del montón correspondientes retienen su valor de compresión de datos, a menos que se modifique el esquema de partición. Si se cambia el esquema de partición, todas las particiones se vuelven a generar en un estado sin comprimir. Para quitar un índice clúster y cambiar el esquema de partición es necesario realizar los pasos siguientes:  
  
     1. Quitar el índice clúster.  
  
     2. Modificar la tabla utilizando la opción ALTER TABLE ... REBUILD ... que especifica la opción de compresión.  
  
     La operación de quitar un índice clúster OFFLINE es muy rápida porque solo se quitan los niveles superiores de índices clústeres. Cuando se quita un índice clúster ONLINE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe volver a generar el montón dos veces, una vez para el paso 1 y otra para el paso 2.  
  
## <a name="how-compression-affects-replication"></a>Cómo afecta la compresión a la replicación  
 Cuando utilice la compresión de datos con replicación, tenga en cuenta las consideraciones siguientes:  
  
-   Cuando el Agente de instantáneas genera el script de esquema inicial, el nuevo esquema utilizará los mismos valores de compresión para la tabla y sus índices. La compresión no se puede habilitar solo en la tabla y no en el índice.  
  
-   Para la replicación transaccional, la opción de esquema de artículo determina para qué propiedades y objetos dependientes se van a generar scripts. Para obtener más información, vea [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql).  
  
     El Agente de distribución no comprueba los suscriptores de nivel inferior cuando aplica scripts. Si se selecciona la replicación de compresión, se producirá un error en la creación de la tabla en los suscriptores de nivel inferior. En el caso de una topología mixta, no se debe habilitar la replicación de compresión.  
  
-   Para la replicación de mezcla, el nivel de compatibilidad de la publicación invalida las opciones de esquema y determina los objetos de esquema para los que se crearán scripts.  
  
     En el caso de una topología mixta, si no se requiere la admisión de las nuevas opciones de compresión, el nivel de compatibilidad de la publicación debe establecerse en la versión de suscriptor de nivel inferior. En caso de que se requiera, se deben comprimir las tablas en el suscriptor una vez creadas.  
  
 La tabla siguiente muestra los valores de replicación que controlan la compresión durante la replicación.  
  
|Intento del usuario|Replicar el esquema de partición para una tabla o índice|Replicar los valores de compresión|Comportamiento de creación de script|  
|-----------------|-----------------------------------------------------|------------------------------------|------------------------|  
|Replicar el esquema de partición y habilitar la compresión en el suscriptor en la partición.|True|True|Se crean scripts tanto para el esquema de partición como para los valores de compresión.|  
|Replicar el esquema de partición pero no comprimir los datos en el suscriptor.|True|False|Se crean scripts para el esquema de partición pero no para los valores de compresión para la partición.|  
|No replicar el esquema de partición y no comprimir los datos en el suscriptor.|False|False|No se crean scripts para la partición o para los valores de compresión.|  
|Comprimir la tabla en el suscriptor si todas las particiones se comprimen en el publicador, pero no replicar el esquema de partición.|False|True|Comprueba si todas las particiones están habilitadas para la compresión.<br /><br /> Se crean scripts para la compresión en el nivel de tabla.|  
  
## <a name="how-compression-affects-other-sql-server-components"></a>Cómo afecta la compresión a los demás componentes de SQL Server  
 La compresión se produce en el motor de almacenamiento y los datos se presentan a la mayoría de los demás componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un estado sin comprimir. Esto limita los efectos de la compresión en los demás componentes para lo siguiente:  
  
-   Operaciones de exportación e importación masivas  
  
     Cuando se exportan datos, incluso en formato nativo, los datos se envían en formato de fila sin comprimir. Esto puede hacer que el tamaño del archivo de datos exportados sea significativamente mayor que el de los datos de origen.  
  
     Cuando se importan datos, si la tabla de destino se ha habilitado para la compresión, el motor de almacenamiento convierte los datos a formato de fila comprimida. Esto puede implicar un mayor uso de la CPU si se compara con la importación de datos en una tabla sin comprimir.  
  
     Cuando los datos se importan de forma masiva a un montón con compresión de página, la operación de importación masiva intentará comprimir los datos con compresión de página cuando se inserten los datos.  
  
-   La compresión no afecta a las acciones de copias de seguridad y restauración.  
  
-   La compresión no afecta al trasvase de registros.  
  
-   La compresión de datos es incompatible con las columnas dispersas. Por consiguiente, las tablas que contienen columnas dispersas no pueden comprimirse y las columnas dispersas no se pueden agregar a una tabla comprimida.  
  
-   Al habilitar la compresión, se puede hacer que los planes de consulta cambien porque los datos se almacenan utilizando un número diferente de páginas y de filas por cada página.  
  
## <a name="see-also"></a>Vea también  
 [Implementación de la compresión de fila](row-compression-implementation.md)   
 [Implementación de la compresión de página](page-compression-implementation.md)   
 [Implementación de la compresión Unicode](unicode-compression-implementation.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-partition-scheme-transact-sql)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-partition-function-transact-sql)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
  
