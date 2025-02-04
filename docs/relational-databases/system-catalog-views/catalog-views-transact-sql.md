---
title: Vistas de catálogo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sql13.SysViewExpandPortal.f1
dev_langs:
- TSQL
helpviewer_keywords:
- catalog metadata [SQL Server]
- system views [SQL Server], catalog
- metadata [SQL Server], views
- catalogs [SQL Server], metadata
- catalog views [SQL Server]
- Database Engine [SQL Server], metadata
- catalog views [SQL Server], about catalog views
ms.assetid: 13bccc2f-ed3c-4b58-abd0-ca8bf34a66b8
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9532ee19ec8489caa51d090feaff464e030a0da0
ms.sourcegitcommit: c70a0e2c053c2583311fcfede6ab5f25df364de0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2019
ms.locfileid: "68670557"
---
# <a name="system-catalog-views-transact-sql"></a>Vistas de catálogo del sistema (Transact-SQL)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Las vistas de catálogo devuelven información utilizada por el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Se recomienda utilizar las vistas de catálogo porque son la interfaz más general para los metadatos del catálogo y proporcionan el método más eficaz para obtener, transformar y presentar formas personalizadas de esta información. Todos los metadatos del catálogo disponibles para el usuario se exponen mediante las vistas de catálogo.

> [!NOTE]
> Las vistas de catálogo no contienen información sobre los datos de catálogo de replicación, copia de seguridad, plan de mantenimiento de bases de datos o Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

 Algunas vistas de catálogo heredan filas de otras vistas de catálogo. Por ejemplo, la vista de catálogo [Sys. Tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) hereda de la vista de catálogo [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) . La vista de catálogo sys.objects se denomina vista base y la vista sys.tables se denomina vista derivada. La vista de catálogo sys.tables devuelve las columnas específicas de tablas y todas las columnas que devuelve la vista de catálogo sys.objects. La vista de catálogo sys.objects devuelve filas de objetos distintos de tablas, como procedimientos almacenados y vistas. Después de crear una tabla, sus metadatos se devuelven en ambas vistas. Si bien las dos vistas de catálogo devuelven diferentes niveles de información sobre la tabla, solo existe una entrada en los metadatos para esta tabla con un nombre y un object_id. Esto se puede resumir de la manera siguiente:

- La vista base contiene un subconjunto de columnas y un superconjunto de filas.
- La vista derivada contiene un superconjunto de columnas y un subconjunto de filas.

> [!IMPORTANT]
> En versiones futuras de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[msCoName](../../includes/msconame-md.md)] puede aumentar la definición de cualquier vista de catálogo del sistema y agregar columnas al final de la lista. Se recomienda no usar la sintaxis SELECT \* from *Sys. catalog_view_name* en el código de producción porque el número de columnas devueltas podría cambiar e interrumpir la aplicación.

Las vistas de catálogo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se han organizado en las siguientes categorías:

|||
|-|-|
|[Vistas &#40;de catálogo de grupos de disponibilidad de Always on TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)|[Mensajes &#40;para errores&#41; vistas &#40;de catálogo de Transact&#41;-SQL](../system-catalog-views/messages-for-errors-catalog-views-sys-messages.md))|
|[Azure SQL Database vistas de catálogo](../../relational-databases/system-catalog-views/azure-sql-database-catalog-views.md)|[Vistas &#40;de catálogo de objetos de TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)|
|[Vistas &#40;de catálogo de Change Tracking TRANSACT-SQL&#41;](../system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)|[Vistas &#40;de catálogo de la función de partición TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)|
|[Vistas &#40;de catálogo del ensamblado CLR TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)|[Vistas de administración basada en directivas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)|
|[Vistas &#40;del recopilador de datos de TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)|[Vistas &#40;de catálogo de Resource Governor TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)|
|[Espacios &#40;de datos TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)|[Query Store Catalog Views (Vistas de catálogo del almacén de consultas) &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)|
|[Correo electrónico de base de datos vistas &#40;de TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md)|[Vistas &#40;de catálogo de tipos escalares de TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)|
|[Vistas &#40;de catálogo del testigo de creación de reflejo de la base de datos TRANSACT-SQL&#41;](../system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)|[Vistas &#40;de catálogo de esquemas de TRANSACT-SQL&#41;](../system-catalog-views/schemas-catalog-views-sys-schemas.md)|
|[Vistas &#40;de catálogo de archivos y bases de datos de TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)|[Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|
|[Vistas &#40;de catálogo de extremos de TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)|[Vistas de catálogo de Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)|
|[Vistas de catálogo de eventos extendidos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)|[Vistas &#40;de catálogo de configuración de todo el servidor TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)|
|[Vistas de catálogo de propiedades extendidas &#40;Transact-SQL&#41;](../system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)|[Vistas de Data Catalog espaciales](../../relational-databases/system-catalog-views/spatial-data-catalog-views.md)|
|[Vistas &#40;de catálogo de operaciones externas TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/external-operations-catalog-views-transact-sql.md)|[SQL Data Warehouse y vistas de catálogo de almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)|
|[Vistas &#40;de catálogo de FileStream y filetable TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)|[Vistas &#40;de catálogo de stretch Database TRANSACT-SQL&#41;](../system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-databases.md)|
|[Vistas &#40;de catálogo de búsqueda de texto completo y búsqueda semántica TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)|[Esquemas XML &#40;, tipo XML&#41; vistas &#40;de catálogo del sistema Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)|
|[Vistas &#40;de catálogo de servidores vinculados TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)||

## <a name="see-also"></a>Vea también

- [Vistas &#40;de esquema de información de TRANSACT-SQL&#41;](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)
- [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
- [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)
