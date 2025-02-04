---
title: sys.dm_exec_plan_attributes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_plan_attributes_TSQL
- dm_exec_plan_attributes_TSQL
- dm_exec_plan_attributes
- sys.dm_exec_plan_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_plan_attributes dynamic management function
ms.assetid: dacf3ab3-f214-482e-aab5-0dab9f0a3648
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4b6e5b28612efccafa9e2de0606eef821e341081
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255599"
---
# <a name="sysdmexecplanattributes-transact-sql"></a>sys.dm_exec_plan_attributes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada atributo del plan especificado por el identificador de plan. Puede usar esta función con valores de tabla para obtener detalles acerca de un plan determinado, como los valores de las claves de la caché o el número de ejecuciones simultáneas del plan.  
  
> [!NOTE]  
>  Algunos de los datos devueltos a través de esta función se asigna a la [sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) vista de compatibilidad con versiones anteriores.

## <a name="syntax"></a>Sintaxis  
```  
sys.dm_exec_plan_attributes ( plan_handle )  
```  
  
## <a name="arguments"></a>Argumentos  
 *plan_handle*  
 Identifica de forma exclusiva un plan de consulta de un lote que se ha ejecutado y cuyo plan reside en la memoria caché del plan. *plan_handle* es **varbinary (64)** . El identificador del plan puede obtenerse a partir del [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md) vista de administración dinámica.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|atributo|**varchar(128)**|Nombre del atributo asociado a este plan. La tabla inmediatamente debajo de ésta enumeran los posibles atributos, sus tipos de datos y sus descripciones.|  
|valor|**sql_variant**|Valor del atributo asociado a este plan.|  
|is_cache_key|**bit**|Indica si el atributo se utiliza como parte de la clave de búsqueda en caché para el plan.|  

En la tabla anterior, **atributo** puede tener los siguientes valores:

|Atributo|Tipo de datos|Descripción|  
|---------------|---------------|-----------------|  
|set_options|**int**|Indica los valores de las opciones con las que se compiló el plan.|  
|objectid|**int**|Una de las claves principales utilizadas para buscar un objeto en la caché. Este es el objeto identificador almacenado en [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) para objetos de base de datos (procedimientos, vistas, desencadenadores etc.). Con los planes de tipo "ad hoc" o preparados, es un valor hash interno del texto del lote.|  
|dbid|**int**|Es el Id. de la base de datos que contiene la entidad a la que el plan hace referencia.<br /><br /> Con los planes "ad hoc" o preparados, es el Id. de la base de datos desde la que se ejecuta el lote.|  
|dbid_execute|**int**|Para los objetos del sistema almacenados en el **recursos** de base de datos, el Id. de base de datos desde el que se ejecuta el plan almacenado en caché. En todos los demás casos es 0.|  
|user_id|**int**|Un valor de -2 indica que el lote enviado no depende de la resolución implícita de nombres y puede compartirse entre distintos usuarios. Éste es el método preferido. Cualquier otro valor representa el Id. del usuario que envía la consulta en la base de datos.| 
|language_id|**smallint**|Es el Id. del idioma de la conexión que creó el objeto de caché. Para obtener más información, consulte [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).|  
|date_format|**smallint**|Formato de fecha de la conexión que creó el objeto de caché. Para más información, vea [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md).|  
|date_first|**tinyint**|Valor de la fecha. Para más información, vea [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md).|  
|status|**int**|Bits de estado interno que son parte de la clave de búsqueda de caché.|  
|required_cursor_options|**int**|Opciones de cursor especificadas por el usuario, como el tipo de cursor.|  
|acceptable_cursor_options|**int**|Opciones de cursor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede convertir de forma implícita para permitir la ejecución de la instrucción. Por ejemplo, el usuario puede especificar un cursor dinámico, pero el optimizador de consultas puede convertir este tipo de cursor a estático.|  
|inuse_exec_context|**int**|Número de lotes en ejecución que usan el plan de consulta.|  
|free_exec_context|**int**|Número de contextos de ejecución almacenados en caché para el plan de consulta que no se usa en ese momento.|  
|hits_exec_context|**int**|Número de veces que el contexto de ejecución se obtuvo de la caché del plan y se reutilizó, ahorrando la sobrecarga de volver a compilar la instrucción SQL. El valor es un agregado para todas las ejecuciones de lotes hasta el momento.|  
|misses_exec_context|**int**|Número de veces que un contexto de ejecución podría no encontrarse en la caché del plan, provocando la creación de un nuevo contexto de ejecución para la ejecución del lote.|  
|removed_exec_context|**int**|Número de contextos de ejecución que se han quitado debido a la presión de memoria en el plan almacenado en caché.|  
|inuse_cursors|**int**|Número de lotes en ejecución que contienen uno o varios cursores que usan el plan almacenado en caché.|  
|free_cursors|**int**|Número de cursores inactivos o libres para el plan almacenado en caché.|  
|hits_cursors|**int**|Número de veces que un cursor inactivo se obtuvo del plan almacenado en caché y se volvió a utilizar. El valor es un agregado para todas las ejecuciones de lotes hasta el momento.|  
|misses_cursors|**int**|Número de veces que un cursor inactivo no se pudo encontrar en la caché.|  
|removed_cursors|**int**|Número de cursores que se han quitado debido a la presión de memoria en el plan almacenado en caché.|  
|sql_handle|**varbinary**(64)|Identificador SQL para el lote.|  
|merge_action_type|**smallint**|El tipo de plan de ejecución de desencadenadores usados como resultado de la instrucción MERGE.<br /><br /> 0 indica un plan sin desencadenadores, un plan de desencadenadores que no se ejecuta como resultado de una instrucción MERGE o un plan de desencadenadores que se ejecuta como resultado de una instrucción MERGE que solo especifica una acción DELETE.<br /><br /> 1 indica un plan de desencadenadores INSERT que se ejecuta como resultado de una instrucción MERGE.<br /><br /> 2 indica un plan de desencadenadores UPDATE que se ejecuta como resultado de una instrucción MERGE.<br /><br /> 3 indica un plan de desencadenadores DELETE que se ejecuta como resultado de una instrucción MERGE que contiene la correspondiente acción INSERT o UPDATE.<br /><br /> Para los desencadenadores anidados que se ejecutan por acciones en cascada, este valor es la acción de la instrucción MERGE que provocó la cascada.|  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requieren el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere el **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.   

## <a name="remarks"></a>Comentarios  
  
## <a name="set-options"></a>Opciones de Set  
 Copias del mismo plan compilado podrían diferir únicamente en el valor de la **set_options** columna. Esto indica que las diferentes conexiones usan conjuntos distintos de opciones SET para la misma consulta. El uso de conjuntos de opciones distintos no suele ser aconsejable porque puede ocasionar compilaciones adicionales, una menor reutilización de los planes y la inflación de la caché de los planes debido a que hay varias copias de los planes en la caché.  
  
### <a name="evaluating-set-options"></a>Evaluar las opciones de Set  
 Para traducir el valor devuelto en **set_options** para las opciones con la que se compiló el plan, reste los valores de la **set_options** valor, comenzando con el mayor valor posible, hasta que llegue a 0. Cada valor que reste se corresponde con una opción que se usó en el plan de consulta. Por ejemplo, si el valor de **set_options** es 251, las opciones que se compiló el plan con son ANSI_NULL_DFLT_ON (128), QUOTED_IDENTIFIER (64), ANSI_NULLS (32), ANSI_WARNINGS (16), CONCAT_NULL_YIELDS_NULL (8), Parallel plan (2) y ANSI_PADDING (1).  
  
|Opción|Valor|  
|------------|-----------|  
|ANSI_PADDING|1|  
|Parallel Plan|2|  
|FORCEPLAN|4|  
|CONCAT_NULL_YIELDS_NULL|8|  
|ANSI_WARNINGS|16|  
|ANSI_NULLS|32|  
|QUOTED_IDENTIFIER|64|  
|ANSI_NULL_DFLT_ON|128|  
|ANSI_NULL_DFLT_OFF|256|  
|NoBrowseTable<br /><br /> Indica que el plan no usa una tabla de trabajo para implementar una operación FOR BROWSE.|512|  
|TriggerOneRow<br /><br /> Indica que el plan contiene la optimización de una fila para las tablas delta de desencadenadores AFTER.|1024|  
|ResyncQuery<br /><br /> Indica que la consulta fue enviada por procedimientos almacenados del sistema internos.|2048|  
|ARITH_ABORT|4096|  
|NUMERIC_ROUNDABORT|8192|  
|DATEFIRST|16384|  
|DATEFORMAT|32768|  
|LanguageID|65536|  
|UPON<br /><br /> Indica que la opción de base de datos PARAMETERIZATION se estableció en FORCED cuando se compiló el plan.|131072|  
|ROWCOUNT|**Se aplica a:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /><br /> 262144|  
  
## <a name="cursors"></a>Cursores  
 Los cursores inactivos se almacenan en caché en un plan compilado para que los usuarios que usan simultáneamente los cursores puedan volver a utilizar la memoria usada para almacenar el cursor. Por ejemplo, suponga que un lote declara y usa un cursor sin cancelar su asignación. Si hay dos usuarios ejecutando el mismo lote, habrá dos cursores activos. Una vez cancelada la asignación de los cursores (posiblemente en lotes diferentes), la memoria usada para almacenar el cursor se almacena en caché y no se libera. La lista de cursores inactivos se conserva en el plan compilado. La siguiente vez que un usuario ejecute el lote, la memoria del cursor almacenado en caché se volverá a usar y se inicializará de forma apropiada como un cursor activo.  
  
### <a name="evaluating-cursor-options"></a>Evaluar las opciones de los cursores  
 Para traducir el valor devuelto en **required_cursor_options** y **acceptable_cursor_options** para las opciones con la que se compiló el plan, reste los valores del valor de columna, a partir de el mayor valor posible, hasta que llegue a 0. Cada valor que reste se corresponde con una opción de cursor que se usó en el plan de consulta.  
  
|Opción|Valor|  
|------------|-----------|  
|None|0|  
|INSENSITIVE|1|  
|SCROLL|2|  
|READ ONLY|4|  
|FOR UPDATE|8|  
|LOCAL|16|  
|GLOBAL|32|  
|FORWARD_ONLY|64|  
|KEYSET|128|  
|DYNAMIC|256|  
|SCROLL_LOCKS|512|  
|OPTIMISTIC|1024|  
|STATIC|2048|  
|FAST_FORWARD|4096|  
|IN PLACE|8192|  
|FOR *select_statement*|16384|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-attributes-for-a-specific-plan"></a>A. Devolver los atributos de un plan concreto  
 En el ejemplo siguiente se devuelven todos los atributos de un plan especificado. La vista de administración dinámica `sys.dm_exec_cached_plans` se consulta primero para obtener el identificador del plan especificado. En la segunda consulta, sustituya `<plan_handle>` por el valor del identificador del plan de la primera consulta.  
  
```sql  
SELECT plan_handle, refcounts, usecounts, size_in_bytes, cacheobjtype, objtype   
FROM sys.dm_exec_cached_plans;  
GO  
SELECT attribute, value, is_cache_key  
FROM sys.dm_exec_plan_attributes(<plan_handle>);  
GO  
```  
  
### <a name="b-returning-the-set-options-for-compiled-plans-and-the-sql-handle-for-cached-plans"></a>b. Devolver las opciones SET para los planes compilados y el identificador SQL para los planes almacenados en caché  
 En el ejemplo siguiente se devuelve un valor que representa las opciones con las que se compiló cada plan. Además, se devuelve el identificador SQL para todos los planes en caché.  
  
```sql  
SELECT plan_handle, pvt.set_options, pvt.sql_handle  
FROM (  
    SELECT plan_handle, epa.attribute, epa.value   
    FROM sys.dm_exec_cached_plans   
        OUTER APPLY sys.dm_exec_plan_attributes(plan_handle) AS epa  
    WHERE cacheobjtype = 'Compiled Plan') AS ecpa   
PIVOT (MAX(ecpa.value) FOR ecpa.attribute IN ("set_options", "sql_handle")) AS pvt;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica y funciones relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  

