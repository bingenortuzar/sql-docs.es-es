---
title: Compatibilidad de FILESTREAM con otras características de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], other SQL Server features and
- FILESTREAM [SQL Server], limitations
ms.assetid: d2c145dc-d49a-4f5b-91e6-89a2b0adb4f3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: aba8bdc3182cd0e3784908a8af32b6f2fbebd6e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010194"
---
# <a name="filestream-compatibility-with-other-sql-server-features"></a>Compatibilidad de FILESTREAM con otras características de SQL Server
  Dado que los datos FILESTREAM están en el sistema de archivos, este tema proporciona algunas consideraciones, directrices y limitaciones para usar FILESTREAM con las siguientes características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [SQL Server Integration Services (SSIS)](#ssis)  
  
-   [Consultas distribuidas y servidores vinculados](#distqueries)  
  
-   [Cifrado](#encryption)  
  
-   [Instantáneas de base de datos](#DatabaseSnapshot)  
  
-   [Replicación](#Replication)  
  
-   [Trasvase de registros](#LogShipping)  
  
-   [Creación de reflejo de base de datos](#DatabaseMirroring)  
  
-   [Indización de texto completo](#FullText)  
  
-   [Agrupación en clústeres de conmutación por error](#FailoverClustering)  
  
-   [SQL Server Express](#SQLServerExpress)  
  
-   [Bases de datos independientes](#contained)  
  
##  <a name="ssis"></a> SQL Server Integration Services (SSIS)  
 SQL Server Integration Services (SSIS) administra los datos FILESTREAM en el flujo de datos como otros datos BLOB utilizando el tipo de datos DT_IMAGE de SSIS.  
  
 Puede utilizar la transformación Importar columna para cargar archivos del sistema de archivos en una columna FILESTREAM. También puede usar la transformación Exportar columna para extraer archivos de una columna FILESTREAM a otra ubicación en el sistema de archivos.  
  
##  <a name="distqueries"></a> Consultas distribuidas y servidores vinculados  
 Puede trabajar con datos FILESTREAM a través de las consultas distribuidas y servidores vinculados si los trata como `varbinary(max)` datos. La función FILESTREAM **PathName()** no puede usar en consultas distribuidas en las que se usa un nombre de cuatro partes, aunque el nombre haga referencia al servidor local. Pero puede usar **PathName()** en una consulta interna de una consulta de paso a través que use **OPENQUERY()** .  
  
##  <a name="encryption"></a> Cifrado  
 Los datos FILESTREAM no se cifran ni siquiera cuando está habilitado el cifrado de datos transparente.  
  
##  <a name="DatabaseSnapshot"></a> Instantáneas de base de datos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite [instantáneas de base de datos](../databases/database-snapshots-sql-server.md) para grupos de archivos FILESTREAM. Si se incluye un grupo de archivos FILESTREAM en una cláusula CREATE DATABASE ON, se producirá un error en la instrucción y se generará el mensaje correspondiente.  
  
 Cuando se utiliza FILESTREAM, pueden crearse instantáneas de la base de datos de grupos de archivos estándar (no FILESTREAM). Los grupos de archivos FILESTREAM se marcan como sin conexión para esas instantáneas de la base de datos.  
  
 Una instrucción SELECT que se ejecuta en una tabla FILESTREAM de una instantánea de base de datos no debe incluir una columna FILESTREAM; de lo contrario, se devolverá el mensaje de error siguiente:  
  
 `Could not continue scan with NOLOCK due to data movement.`  
  
##  <a name="Replication"></a> Replication  
 Una columna `varbinary(max)` que tiene el atributo FILESTREAM habilitado en el publicador puede replicarse en un suscriptor con o sin el atributo FILESTREAM. Para especificar cómo se replica la columna, utilice el cuadro de diálogo **Propiedades del artículo - \<Artículo>** o el parámetro @schema_option de [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) o [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Los datos que se replican en una columna `varbinary(max)` que no tiene el atributo FILESTREAM no deben superar el límite de 2 GB para ese tipo de datos; de lo contrario, se genera un error en tiempo de ejecución. Se recomienda que replique el atributo FILESTREAM, a menos que se va a replicar datos a [!INCLUDE[ssVersion2005](../../includes/ssversion2000-md.md)] no es compatible con suscriptores, independientemente de la opción de esquema que se ha especificado.  
  
> [!NOTE]  
>  La replicación de valores de datos de gran tamaño de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a suscriptores de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] está limitada a un máximo de 256 MB de valores de datos. Para obtener más información, vea [Especificaciones de capacidad máxima](https://go.microsoft.com/fwlink/?LinkId=103810).  
  
### <a name="considerations-for-transactional-replication"></a>Consideraciones acerca de la replicación transaccional  
 Si utiliza columnas FILESTREAM en tablas que se publican para la replicación transaccional, tenga en cuenta las consideraciones siguientes:  
  
-   Si alguna de las tablas incluye columnas que tienen el atributo FILESTREAM, no puede usar valores de *database snapshot* ni *database snapshot character* para la propiedad @sync_method de [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql).  
  
-   La opción max text repl size especifica la cantidad máxima de datos que se pueden insertar en una columna que se publica para la replicación. Esta opción se puede utilizar para controlar el tamaño de los datos FILESTREAM que se replican.  
  
-   Si especifica la opción de esquema para replicar el atributo FILESTREAM, pero filtra la columna `uniqueidentifier` que FILESTREAM necesita o especifica que no se replique la restricción UNIQUE para la columna, la replicación no replica el atributo FILESTREAM. La columna solo se replica como una columna `varbinary(max)`.  
  
### <a name="considerations-for-merge-replication"></a>Consideraciones acerca de la replicación de mezcla  
 Si utiliza columnas FILESTREAM en tablas que se publican para la replicación de mezcla, tenga en cuenta las consideraciones siguientes:  
  
-   Tanto la replicación de mezcla como FILESTREAM requieren una columna del tipo de datos `uniqueidentifier` para identificar cada fila de una tabla. La replicación de mezcla agrega una columna automáticamente si la tabla no la tiene. La replicación de mezcla requiere que la columna tenga establecida la propiedad ROWGUIDCOL y su valor predeterminado sea NEWID() o NEWSEQUENTIALID(). Además de estos requisitos, FILESTREAM requiere que se defina una restricción UNIQUE para la columna. Estos requisitos tienen las consecuencias siguientes:  
  
    -   Si agrega una columna FILESTREAM a una tabla que ya está publicada para la replicación de mezcla, asegúrese de que la columna `uniqueidentifier` tiene una restricción UNIQUE. Si no tiene una restricción UNIQUE, agregue una restricción con nombre a la tabla en la base de datos de publicación. De forma predeterminada, la replicación de mezcla publicará este cambio del esquema y se aplicará a cada base de datos de suscripciones.  
  
         Si agrega manualmente una restricción UNIQUE tal como se ha descrito y desea quitar la replicación de mezcla, primero debe quitar la restricción UNIQUE; de lo contrario, se producirá un error en la eliminación de la replicación.  
  
    -   De forma predeterminada, la replicación de mezcla utiliza NEWSEQUENTIALID() porque puede proporcionar un mejor rendimiento que NEWID(). Si agrega una columna `uniqueidentifier` a una tabla que se publicará para la replicación de mezcla, especifique NEWSEQUENTIALID() como valor predeterminado.  
  
-   La replicación de mezcla incluye una optimización para replicar tipos de objetos grandes. Esta optimización la controla el parámetro @stream_blob_columns de [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Si establece la opción de esquema para replicar el atributo FILESTREAM, el valor del parámetro @stream_blob_columns se establece en `true`. Esta optimización se puede invalidar con [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Este procedimiento almacenado le permite establecer @stream_blob_columns en `false`. Si agrega una columna FILESTREAM a una tabla que ya está publicada para la replicación de mezcla, se recomienda establecer la opción en `true` mediante el uso de sp_changemergearticle.  
  
-   Si se habilita la opción de esquema para FILESTREAM una vez creado un artículo, puede producirse un error en la replicación si los datos de una columna FILESTREAM superan los 2 GB y hay un conflicto durante la replicación. Si espera que se produzca esta situación, se recomienda que quite y vuelva a crear el artículo de la tabla con la opción de esquema FILESTREAM adecuada habilitada durante la creación.  
  
-   La replicación de mezcla puede sincronizar datos FILESTREAM a través de una conexión HTTPS mediante la [Sincronización web](../replication/merge/merge-replication.md). Estos datos no pueden superar el límite de 50 MB para la Sincronización web; de lo contrario, se generará un error en tiempo de ejecución.  
  
##  <a name="LogShipping"></a> Trasvase de registros  
 [El trasvase de registros](../../database-engine/log-shipping/about-log-shipping-sql-server.md) es compatible con FILESTREAM. Los servidores principal y secundario deben estar ejecutando [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]o una versión posterior y deben tener FILESTREAM habilitado.  
  
##  <a name="DatabaseMirroring"></a> Creación de reflejo de base de datos  
 La creación de reflejo de la base de datos no es compatible con FILESTREAM. No se puede crear un grupo de archivos FILESTREAM en el servidor principal. La creación de reflejo de la base de datos no puede configurarse para una base de datos que contiene grupos de archivos FILESTREAM.  
  
##  <a name="FullText"></a> Indización de texto completo  
 [Indización de texto completo](../indexes/indexes.md) funciona con una columna FILESTREAM de la misma manera que lo hace con un `varbinary(max)` columna. La tabla FILESTREAM debe tener una columna con la extensión de nombre de archivo para cada BLOB FILESTREAM. Para obtener más información, vea [Consultar con búsqueda de texto completo](../search/query-with-full-text-search.md), [Configurar y administrar filtros para búsquedas](../search/configure-and-manage-filters-for-search.md) y [sys.fulltext_document_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).  
  
 El motor de texto completo indiza el contenido de los BLOB FILESTREAM. Indizar archivos como las imágenes podría no ser útil. Cuando se actualiza un BLOB FILESTREAM, vuelve a indizarse.  
  
##  <a name="FailoverClustering"></a> Agrupación en clústeres de conmutación por error  
 Para la agrupación en clústeres de conmutación por error, los grupos de archivos FILESTREAM deben situarse en un disco compartido. Es preciso habilitar FILESTREAM en cada nodo del clúster que hospedará la instancia de FILESTREAM. Para obtener más información, vea [Configurar FILESTREAM en un clúster de conmutación por error](set-up-filestream-on-a-failover-cluster.md).  
  
##  <a name="SQLServerExpress"></a> SQL Server Express  
 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] es compatible con FILESTREAM. El límite de tamaño de base de datos de 10 GB no incluye el contenedor de datos de FILESTREAM.  
  
##  <a name="contained"></a> Bases de datos independientes  
 La característica FILESTREAM requiere cierta configuración fuera de la base de datos. Por consiguiente, una base de datos que utiliza FILESTREAM o FileTable no es totalmente contenida.  
  
 Puede establecer la contención de la base de datos en PARTIAL si desea utilizar algunas características de bases de datos contenidas, como usuarios contenidos. Sin embargo, en este caso, debe tener en cuenta que algunas de las opciones de base de datos no están contenidas en la base de datos y no se mueven automáticamente cuando lo hace la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](binary-large-object-blob-data-sql-server.md)  
  
  
