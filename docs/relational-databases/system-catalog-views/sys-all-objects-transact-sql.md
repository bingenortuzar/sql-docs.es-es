---
title: Sys.all_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.all_objects
- all_objects_TSQL
- all_objects
- sys.all_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_objects catalog view
ms.assetid: 547e4be4-a8e4-48ce-9d8d-37b169985081
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 499b1ddeeafbc21a923f15102a67d9c0a332f069
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018162"
---
# <a name="sysallobjects-transact-sql"></a>sys.all_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Muestra la unión de todos los objetos definidos por el usuario y los objetos del sistema en el ámbito del esquema.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Nombre del objeto.|  
|object_id|**int**|Número de identificación del objeto. Es único en una base de datos.|  
|principal_id|**int**|Identificador del propietario individual si es diferente del propietario del esquema. De forma predeterminada, los objetos contenidos en el esquema pertenecen al propietario del esquema. No obstante, se puede especificar otro propietario mediante la instrucción ALTER AUTHORIZATION para cambiar la propiedad.<br /><br /> Es NULL si no hay ningún propietario individual alternativo.<br /><br /> Es NULL si el tipo de objeto es uno de los siguientes:<br /><br /> C = restricción CHECK<br /><br /> D = DEFAULT (restricción o independiente)<br /><br /> F = Restricción FOREIGN KEY<br /><br /> PK = Restricción PRIMARY KEY<br /><br /> R = Regla (estilo antiguo, independiente)<br /><br /> TA = Desencadenador de ensamblado (CLR)<br /><br /> TR = Desencadenador SQL<br /><br /> UQ = Restricción UNIQUE|  
|schema_id|**int**|Identificador del esquema que contiene el objeto.<br /><br /> Para todos los objetos del sistema del ámbito del esquema incluidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], este valor siempre se encuentra en (schema_id('sys'), schema_id('INFORMATION_SCHEMA')).|  
|parent_object_id|**int**|Identificador del objeto al que pertenece este objeto.<br /><br /> 0 = No es un objeto secundario.|  
|type|**char(2)**|Tipo de objeto:<br /><br /> AF = Función de agregado (CLR)<br /><br /> C = restricción CHECK<br /><br /> D = DEFAULT (restricción o independiente)<br /><br /> F = Restricción FOREIGN KEY<br /><br /> FN = Función escalar de SQL<br /><br /> FS = Función escalar del ensamblado (CLR)<br /><br /> FT = Función con valores de tabla de ensamblado (CLR)<br /><br /> IF = Función SQL insertada con valores de tabla<br /><br /> IT = tabla interna<br /><br /> P = Procedimiento almacenado de SQL<br /><br /> PC = Procedimiento almacenado del ensamblado (CLR)<br /><br /> PG = Guía de plan<br /><br /> PK = Restricción PRIMARY KEY<br /><br /> R = Regla (estilo antiguo, independiente)<br /><br /> RF = Procedimiento de filtro de replicación<br /><br /> S = Tabla base del sistema<br /><br /> SN = Sinónimo<br /><br /> SQ = Cola de servicio<br /><br /> TA = Desencadenador DML del ensamblado (CLR)<br /><br /> TF = Función con valores de tabla SQL<br /><br /> TR = Desencadenador DML de SQL<br /><br /> TT = Tipo de tabla<br /><br /> U = Tabla (definida por el usuario)<br /><br /> UQ = Restricción UNIQUE<br /><br /> V = Vista<br /><br /> X = Procedimiento almacenado extendido|  
|type_desc|**nvarchar(60)**|Descripción del tipo de objeto. AGGREGATE_FUNCTION<br /><br /> CHECK_CONSTRAINT<br /><br /> DEFAULT_CONSTRAINT<br /><br /> FOREIGN_KEY_CONSTRAINT<br /><br /> SQL_SCALAR_FUNCTION<br /><br /> CLR_SCALAR_FUNCTION<br /><br /> CLR_TABLE_VALUED_FUNCTION<br /><br /> SQL_INLINE_TABLE_VALUED_FUNCTION<br /><br /> INTERNAL_TABLE<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> PLAN_GUIDE<br /><br /> PRIMARY_KEY_CONSTRAINT<br /><br /> RULE<br /><br /> REPLICATION_FILTER_PROCEDURE<br /><br /> SYSTEM_TABLE<br /><br /> SYNONYM<br /><br /> SERVICE_QUEUE<br /><br /> CLR_TRIGGER<br /><br /> SQL_TABLE_VALUED_FUNCTION<br /><br /> SQL_TRIGGER<br /><br /> TABLE_TYPE<br /><br /> USER_TABLE<br /><br /> UNIQUE_CONSTRAINT<br /><br /> VIEW<br /><br /> EXTENDED_STORED_PROCEDURE|  
|create_date|**datetime**|Fecha de creación del objeto.|  
|modify_date|**datetime**|Fecha en que se modificó el objeto por última vez con una instrucción ALTER. Si el objeto es una tabla o vista, modify_date cambia también cuando se crea o modifica un índice clúster en la tabla o vista.|  
|is_ms_shipped|**bit**|Objeto creado por un componente interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|is_published|**bit**|El objeto se publica.|  
|is_schema_published|**bit**|Solo se ha publicado el esquema del objeto.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)  
  
  
