---
title: Sys. DM _ _operation_status (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/05/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dm_operation_status_TSQL
- dm_operation_status
- sys.dm_operation_status
- sys.dm_operation_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_operation_status dynamic management view
- sys.dm_operation_status dynamic management view
ms.assetid: cc847784-7f61-4c69-8b78-5f971bb24d61
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: c49e4e01dd8ddaf0667546a8cc221a7918f42c81
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "70911204"
---
# <a name="sysdm_operation_status-azure-sql-database"></a>sys.dm_operation_status (Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Devuelve información acerca de las operaciones realizadas en las bases de datos de un servidor [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|session_activity_id|**uniqueidentifier**|Identificador de la operación. NOT NULL.|  
|resource_type|**int**|Indica el tipo de recurso en el que se realiza la operación. NOT NULL. En la versión actual, esta vista solo realiza el seguimiento de las operaciones realizadas en [!INCLUDE[ssSDS](../../includes/sssds-md.md)], y el valor entero correspondiente es 0.|  
|resource_type_desc|**nvarchar(2048)**|Descripción del tipo de recurso en el que se realiza la operación. En la versión actual, esta vista solo realiza el seguimiento de las operaciones realizadas en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|  
|major_resource_id|**sql_variant**|Nombre del [!INCLUDE[ssSDS](../../includes/sssds-md.md)] en el que se realiza la operación. No NULL.|  
|minor_resource_id|**sql_variant**|Exclusivamente para uso interno. NOT NULL.|  
|operación|**nvarchar(60)**|Operación realizada en un [!INCLUDE[ssSDS](../../includes/sssds-md.md)], como Create o ALTER.|  
|state|**tinyint**|El estado de la operación.<br /><br /> 0 = Pendiente<br />1 = en curso<br />2= Completado<br />3 = error<br />4 = Cancelado|  
|state_desc|**nvarchar(120)**|PENDING = la operación está esperando disponibilidad de los recursos o la cuota.<br /><br /> IN_PROGRESS = la operación se ha iniciado y está en curso.<br /><br /> COMPLETED = la operación finalizó correctamente.<br /><br /> FAILED= se produjo un error en la operación Vea la columna **error_desc** para obtener más información.<br /><br /> CANCELLED = la operación se detuvo a petición del usuario.|  
|percent_complete|**int**|Porcentaje de la operación que se ha completado. Los valores no son continuos y los valores válidos se enumeran a continuación. NOT NULL.<br/><br/>0 = operación no iniciada<br/>50 = operación en curso<br/>100 = operación completada|  
|error_code|**int**|Código que indica el error que se produjo durante una operación con errores. Si el valor es 0, indica que la operación se completó correctamente.|  
|error_desc|**nvarchar(2048)**|Descripción del error que se produjo durante una operación con errores.|  
|error_severity|**int**|Nivel de gravedad del error que se produjo durante una operación con errores. Para obtener más información acerca de los errores de gravedad, consulte [motor de base de datos errores de gravedad](https://go.microsoft.com/fwlink/?LinkId=251052).|  
|error_state|**int**|Reservado para un uso futuro. La compatibilidad con versiones posteriores no está garantizada.|  
|start_time|**datetime**|Marca de tiempo del inicio de la operación.|  
|last_modify_time|**datetime**|Marca de tiempo en la que se modificó el registro por última vez para una operación de ejecución prolongada. En el caso de operaciones completadas correctamente, este campo muestra la marca de tiempo en la que se completó la operación.|  
  
## <a name="permissions"></a>Permisos  
 Esta vista solo está disponible en la base de datos **maestra** para el inicio de sesión principal de nivel de servidor.  
  
## <a name="remarks"></a>Comentarios  
 Para usar esta vista, debe estar conectado a la base de datos **maestra** . Use la `sys.dm_operation_status` vista en la base de datos maestra [!INCLUDE[ssSDS](../../includes/sssds-md.md)] del servidor para realizar un seguimiento del estado de las siguientes operaciones [!INCLUDE[ssSDS](../../includes/sssds-md.md)]realizadas en un:  
  
-   Crear base de datos  
  
-   Copiar base de datos. Copia de base de datos crea un registro en esta vista tanto en el servidor de origen como en el de destino.  
  
-   Modificar base de datos  
  
-   Cambiar el nivel de rendimiento de un nivel de servicio  
  
-   Cambiar el nivel de servicio de una base de datos, como cambiar de básico a estándar.  
  
-   Configuración de una relación de replicación geográfica  
  
-   Finalización de una relación de replicación geográfica  
  
-   Restaurar base de datos  
  
-   Eliminar base de datos  
  
## <a name="example"></a>Ejemplo  
 Mostrar las operaciones de replicación geográfica más recientes asociadas a la base de datos ' mydb '.  
  
```  
SELECT * FROM sys.dm_operation_status   
   WHERE major_resource_id = 'myddb'   
   ORDER BY start_time DESC;  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;y vistas de administración dinámica de replicación geográfica Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [Sys. DM _ &#40;_geo_replication_link_status Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [Sys. geo _replication_links &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
  
  
