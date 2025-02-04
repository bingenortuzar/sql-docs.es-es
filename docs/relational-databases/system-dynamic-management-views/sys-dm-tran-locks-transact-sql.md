---
title: Sys.dm_tran_locks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_locks
- sys.dm_tran_locks
- sys.dm_tran_locks_TSQL
- dm_tran_locks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_locks dynamic management view
ms.assetid: f0d3b95a-8a00-471b-9da4-14cb8f5b045f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 32140a9ef5b1a8965876c4ee30fe72559ba8b7ce
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262624"
---
# <a name="sysdmtranlocks-transact-sql"></a>sys.dm_tran_locks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información acerca de los recursos del administrador de bloqueos activos actualmente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Cada fila representa una solicitud activa al administrador de bloqueos sobre un bloqueo que se ha concedido o está esperando a ser concedido.  
  
 Las columnas del conjunto de resultados se dividen en dos grupos principales: recurso y solicitud. El grupo sobre el recurso describe el recurso en que se ha solicitado realizar el bloqueo; el grupo sobre la solicitud describe la solicitud de bloqueo.  
  
> [!NOTE]  
> Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_tran_locks**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**resource_type**|**nvarchar(60)**|Representa el tipo de recurso. El valor puede ser uno de los siguientes: Base de datos, archivo, objeto, página, clave, extensión, RID, APPLICATION, metadatos, HOBT o ALLOCATION_UNIT.|  
|**resource_subtype**|**nvarchar(60)**|Representa un subtipo de **resource_type**. Adquirir un bloqueo de subtipo sin mantener un bloqueo sin subtipos del tipo primario es técnicamente válido. Los diferentes subtipos no entran en conflicto, ni entre sí, ni con el tipo primario sin subtipos. No todos los tipos de recurso tienen subtipos.|  
|**resource_database_id**|**int**|Id. de la base de datos en la que se centra este recurso. Todos los recursos manejados por el administrador de bloqueos tienen como ámbito el Id. de la base de datos.|  
|**resource_description**|**nvarchar(256)**|Descripción del recurso que solo contiene información que no está disponible en otras columnas de recurso.|  
|**resource_associated_entity_id**|**bigint**|Id. de la entidad en una base de datos a la que se asocia un recurso. Puede ser un Id. de objeto, de Hobt o de unidad de asignación, dependiendo del tipo de recurso.|  
|**resource_lock_partition**|**Int**|Id. de la partición de bloqueo para un recurso de bloqueo dividido. El valor para recursos de bloqueo sin particiones es 0.|  
|**request_mode**|**nvarchar(60)**|Modo de la solicitud. En el caso de solicitudes concedidas, se trata del modo concedido; en el caso de solicitudes en espera, se trata del modo que se está solicitando.|  
|**request_type**|**nvarchar(60)**|Tipo de solicitud. El valor es LOCK.|  
|**request_status**|**nvarchar(60)**|Estado actual de esta solicitud. Los valores posibles son GRANTED, CONVERT, WAIT, LOW_PRIORITY_CONVERT, LOW_PRIORITY_WAIT o ABORT_BLOCKERS. Para obtener más información sobre los bloqueos de anulación y esperas de prioridad baja, consulte el *low_priority_lock_wait* sección de [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).|  
|**request_reference_count**|**smallint**|Devuelve un número aproximado de veces que el mismo solicitante ha requerido este recurso.|  
|**request_lifetime**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**request_session_id**|**int**|Id. de la sesión que actualmente posee esta solicitud. El Id. de esta sesión puede cambiar en el caso de transacciones distribuidas y enlazadas. Un valor -2 indica que la solicitud pertenece a una transacción distribuida huérfana. El valor -3 indica que la solicitud pertenece a una transacción de recuperación diferida; por ejemplo, una transacción para la que se ha diferido la reversión en la recuperación porque esta reversión no se ha podido terminar correctamente.|  
|**request_exec_context_id**|**int**|Id. del contexto de ejecución del proceso que posee actualmente esta solicitud.|  
|**request_request_id**|**int**|Id. de solicitud (Id. de lote) del proceso que posee actualmente esta solicitud. Este valor cambiará cada vez que cambie la conexión activa del conjunto de resultados activos múltiples (MARS) para una transacción.|  
|**request_owner_type**|**nvarchar(60)**|Tipo de entidad que posee la solicitud. Las solicitudes del administrador de bloqueos pueden ser propiedad de varios tipos de entidades. Los valores posibles son:<br /><br /> TRANSACTION = La solicitud es propiedad de una transacción.<br /><br /> CURSOR = La solicitud es propiedad de un cursor.<br /><br /> SESSION = La solicitud es propiedad de una sesión de usuario.<br /><br /> SHARED_TRANSACTION_WORKSPACE = La solicitud es propiedad de la parte compartida del área de trabajo de la transacción.<br /><br /> EXCLUSIVE_TRANSACTION_WORKSPACE = La solicitud es propiedad de la parte exclusiva del área de trabajo de la transacción.<br /><br /> NOTIFICATION_OBJECT = La solicitud es propiedad de un componente interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este componente ha solicitado al administrador de bloqueos que le notifique cuándo otro componente está a la espera del bloqueo. La característica FileTable es un componente que utiliza este valor.<br /><br /> **Nota:** Espacios de trabajo se usan internamente para mantener bloqueos para sesiones dadas de alta.|  
|**request_owner_id**|**bigint**|Identificador del propietario específico de esta solicitud.<br /><br /> Si una transacción es la propietaria de la solicitud, este valor contiene el identificador de transacción<br /><br /> Cuando un objeto FileTable es el propietario de la solicitud, **request_owner_id** tiene uno de los siguientes valores.<br /><br /> <br /><br /> -4: Un objeto FileTable ha tomado un bloqueo de base de datos.<br /><br /> -3: Un objeto FileTable ha tomado un bloqueo de tabla.<br /><br /> Otro valor: El valor representa un identificador de archivo. Este valor también aparece como **fcb_id** en la vista de administración dinámica [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md).|  
|**request_owner_guid**|**uniqueidentifier**|GUID del propietario específico de esta solicitud. Este valor solo se utiliza en una transacción distribuida cuando el valor corresponde al GUID del servicio MS DTC para esa transacción.|  
|**request_owner_lockspace_id**|**nvarchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] Este valor representa el Id. del espacio de bloqueo del solicitante. El Id. del espacio de bloqueo determina si dos solicitantes son compatibles entre sí y si pueden tener bloqueos en modos que, de otra forma, entrarían en conflicto entre sí.|  
|**lock_owner_address**|**varbinary(8)**|Dirección de memoria de la estructura de datos interna utilizada para realizar el seguimiento de esta solicitud. Esta columna se puede combinar la con **resource_address** columna **sys.dm_os_waiting_tasks**.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> <br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requieren el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere el **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.   
 
## <a name="remarks"></a>Comentarios  
 Un estado de solicitud Granted indica que se ha concedido el bloqueo sobre un recurso al solicitante. Una solicitud en espera indica que la solicitud aún no se ha concedido. Devuelven los siguientes tipos de solicitud en espera la **request_status** columna:  
  
-   Un estado de solicitud Convert indica que el solicitante ya tiene concedida una solicitud para un recurso y está esperando la concesión de una actualización a la solicitud inicial.  
  
-   Un estado de solicitud Wait indica que el solicitante no tiene concedida actualmente ninguna solicitud sobre el recurso.  
  
 Dado que **sys.dm_tran_locks** se rellena a partir de estructuras de datos de administrador de bloqueo interno, mantener esta información no agrega una sobrecarga adicional para regular procesamiento. Materializar la vista requiere acceso a las estructuras de datos internas del administrador de bloqueos. Esto puede tener consecuencias menores en el procesamiento normal en el servidor. Puede que no perciba estas consecuencias o que solo afecten a los recursos con un alto grado de utilización. Como los datos de esta vista corresponden al estado activo del administrador de bloqueos, estos se pueden cambiar en cualquier momento; además, las filas se agregan y quitan según se van adquiriendo y liberando bloqueos. Esta vista no tiene información histórica.  
  
 Dos solicitudes funcionan en el mismo recurso solamente si todas las columnas del grupo de recursos son iguales.  
  
 Puede controlar el bloqueo de operaciones de lectura mediante las siguientes herramientas:  
  
-   SET TRANSACTION ISOLATION LEVEL para especificar el nivel de bloqueo de una sesión. Para obtener más información, vea [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
-   Sugerencias de bloqueo de tablas para especificar el nivel de bloqueo para una referencia individual de una tabla en una cláusula FROM. Para la sintaxis y las restricciones, vea [sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Un recurso que se ejecuta con un Id. de sesión puede tener más de un bloqueo concedido. Distintas entidades que se ejecutan en una sesión pueden poseer un bloqueo en el mismo recurso y la información se muestra en el **request_owner_type** y **request_owner_id** las columnas que son devuelto por **sys.dm_tran_locks**. Si varias instancias del mismo **request_owner_type** existe, el **request_owner_id** columna se utiliza para distinguir cada instancia. Para las transacciones distribuidas, el **request_owner_type** y **request_owner_guid** columnas mostrará la información de entidad diferente.  
  
 Por ejemplo, la sesión S1 mantiene un bloqueo compartido en **Table1**; y la transacción T1, que se ejecuta en la sesión S1, también mantiene un bloqueo compartido en **Table1**. En este caso, el **resource_description** columna devuelta por **sys.dm_tran_locks** mostrará las dos instancias del mismo recurso. El **request_owner_type** columna mostrará una instancia como una sesión y la otra como una transacción. Además, el **resource_owner_id** columna tendrá valores diferentes.  
  
 No es posible distinguir varios cursores que se ejecutan en una misma sesión y, por tanto, se tratan como una sola entidad.  
  
 Las transacciones distribuidas que no están asociadas a un valor de identificador de sesión son transacciones huérfanas y tienen asignado el valor de identificador de sesión -2. Para obtener más información, consulte [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md).  
  
## <a name="resource-details"></a>Detalles del recurso  
 En la tabla siguiente se enumera los recursos que se representan en el **resource_associated_entity_id** columna.  
  
|Tipo de recurso|Descripción del recurso|Resource_associated_entity_id|  
|-------------------|--------------------------|--------------------------------------|  
|DATABASE|Representa una base de datos.|No aplicable|  
|FILE|Representa un archivo de la base de datos. Este archivo puede ser un archivo de datos o de registro.|No aplicable|  
|OBJECT|Representa un objeto de la base de datos. Este objeto puede ser una tabla de datos, una vista, un procedimiento almacenado, un procedimiento almacenado extendido o cualquier objeto que tenga un Id. de objeto.|Id. de objeto|  
|PAGE|Representa una página de un archivo de datos.|Identificador de HoBt. Este valor corresponde al **sys.partitions.hobt_id**. El identificador de HoBt no está siempre disponible para recursos PAGE, ya que es información adicional que puede proporcionar el autor de la llamada y no todos los autores de llamadas pueden proporcionar esta información.|  
|KEY|Representa una fila en un índice.|Identificador de HoBt. Este valor corresponde al **sys.partitions.hobt_id**.|  
|EXTENT|Representa la extensión de un archivo de datos. Una extensión es un grupo de ocho páginas contiguas.|No aplicable|  
|RID|Representa una fila física en un montón.|Identificador de HoBt. Este valor corresponde al **sys.partitions.hobt_id**. El identificador de HoBt no está siempre disponible para recursos RID, ya que es información adicional que puede proporcionar el autor de la llamada y no todos los autores de llamadas pueden proporcionar esta información.|  
|APPLICATION|Representa un recurso específico de aplicación.|No aplicable|  
|METADATA|Representa información de metadatos.|No aplicable|  
|HOBT|Representa un montón o un árbol b. Se trata de las estructuras de ruta de acceso básicas.|Identificador de HoBt. Este valor corresponde al **sys.partitions.hobt_id**.|  
|ALLOCATION_UNIT|Representa un conjunto de páginas relacionadas, por ejemplo, una partición de índice. Cada unidad de asignación cubre una única cadena del Mapa de asignación de índices (IAM).|Identificador de unidad de asignación. Este valor corresponde al **sys.allocation_units.allocation_unit_id**.|  
  
 En la tabla siguiente se muestran los subtipos asociados a cada tipo de recurso.  
  
|Subtipo de recurso|Sincronizaciones|  
|---------------------|------------------|  
|ALLOCATION_UNIT.BULK_OPERATION_PAGE|Las páginas preasignadas usadas para operaciones masivas.|  
|ALLOCATION_UNIT.PAGE_COUNT|Estadísticas de recuentos de páginas de unidades de asignación durante operaciones de eliminación diferida.|  
|DATABASE.BULKOP_BACKUP_DB|Copias de seguridad de base de datos con operaciones masivas.|  
|DATABASE.BULKOP_BACKUP_LOG|Copias de seguridad de registros de base de datos con operaciones masivas.|  
|DATABASE.CHANGE_TRACKING_CLEANUP|Tareas de limpieza de seguimiento de cambios.|  
|DATABASE.CT_DDL|Operaciones DDL de seguimiento de cambios de nivel de tabla y base de datos.|  
|DATABASE.CONVERSATION_PRIORITY|Operaciones de prioridad de conversación de Service Broker como CREATE BROKER PRIORITY.|  
|DATABASE.DDL|Operaciones del Lenguaje de definición de datos (DDL) con operaciones de grupo de archivos, como la eliminación.|  
|DATABASE.ENCRYPTION_SCAN|Sincronización de cifrado de TDE.|  
|DATABASE.PLANGUIDE|Sincronización de la guía de plan.|  
|DATABASE.RESOURCE_GOVERNOR_DDL|Operaciones DDL para las operaciones de gobernador de recursos como ALTER RESOURCE POOL.|  
|DATABASE.SHRINK|Operaciones de reducción de la base de datos.|  
|DATABASE.STARTUP|Se usa para la sincronización de inicios de bases de datos.|  
|FILE.SHRINK|Operaciones de reducción de archivos.|  
|HOBT.BULK_OPERATION|Operaciones de carga masiva optimizadas para montones con recorrido simultáneo bajo estos niveles de aislamiento: instantánea, lectura no confirmada y lectura confirmada con versiones de fila.|  
|HOBT.INDEX_REORGANIZE|Operaciones de reorganización del montón o el índice.|  
|OBJECT.COMPILE|Compilación de procedimiento almacenado.|  
|OBJECT.INDEX_OPERATION|Operaciones de índice.|  
|OBJECT.UPDSTATS|Actualizaciones de estadísticas en una tabla.|  
|METADATA.ASSEMBLY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_CLR_NAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_TOKEN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASYMMETRIC_KEY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_ACTIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_SPECIFICATION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AVAILABILITY_GROUP|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CERTIFICATE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CHILD_INSTANCE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_FRAGMENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_ROWSET|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_ENDPOINT_RECV|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_ENDPOINT_SEND|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_GROUP|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_PRIORITY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CREDENTIAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CRYPTOGRAPHIC_PROVIDER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATA_SPACE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE_PRINCIPAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_SESSION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_WITNESS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_PRINCIPAL_SID|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT_WEBMETHOD|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_COLUMN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_STOPLIST|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEX_EXTENSION_SCHEME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEXSTATS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INSTANTIATED_TYPE_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.MESSAGE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.METADATA_CACHE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PARTITION_FUNCTION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PASSWORD_POLICY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PERMISSIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE_SCOPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.REMOTE_SERVICE_BINDING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ROUTE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SCHEMA|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_CACHE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_DESCRIPTOR|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SEQUENCE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_EVENT_SESSIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_PRINCIPAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_BROKER_GUID|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_CONTRACT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_MESSAGE_TYPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.STATS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SYMMETRIC_KEY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.USER_TYPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COLLECTION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COMPONENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_INDEX_QNAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 En la tabla siguiente proporciona el formato de la **resource_description** columna para cada tipo de recurso.  
  
|Resource|Formato|Descripción|  
|--------------|------------|-----------------|  
|DATABASE|No aplicable|Id. de base de datos ya está disponible en el **resource_database_id** columna.|  
|FILE|< file_id >|Id. del archivo representado por este recurso.|  
|OBJECT|< object_id >|Id. del objeto representado por este recurso. Este objeto puede ser cualquier objeto mostrado en **sys.objects**, no solo una tabla.|  
|PAGE|< file_id >: < page_in_file >|Representa el Id. de página y de archivo de la página representada por este recurso.|  
|KEY|< hash_value >|Representa un hash de las columnas de clave de la fila representada por este recurso.|  
|EXTENT|< file_id >: < page_in_files >|Representa el Id. de página y de archivo de la extensión representada por este recurso. El Id. de extensión es el mismo que el Id. de página correspondiente a la primera página de la extensión.|  
|RID|< file_id >: < page_in_file >: < row_on_page >|Representa el Id. de página y de fila de la fila representada por este recurso. Tenga en cuenta que si el Id. del objeto asociado es 99, este recurso representa una de las ocho zonas de página mixta en la primera página IAM de una cadena IAM.|  
|APPLICATION|\<DbPrincipalId >:\<hasta 32 caracteres > :(< hash_value >)|Representa el Id. de la entidad de seguridad de base de datos utilizada para asignar el ámbito de este recurso de bloqueo de aplicación. También se incluyen hasta 32 caracteres de la cadena del recurso correspondiente a este recurso de bloqueo de la aplicación. En determinados casos solo pueden mostrarse 2 caracteres porque la cadena completa ya no está disponible. Este comportamiento solo se produce en tiempo de recuperación de la base de datos para bloqueos de aplicaciones que se vuelven a adquirir como parte del proceso de recuperación. El valor hash representa un hash de la cadena de recurso completa correspondiente a este recurso de bloqueo de la aplicación.|  
|HOBT|No aplicable|Id. de HoBt se incluye como la **resource_associated_entity_id**.|  
|ALLOCATION_UNIT|No aplicable|Id. de unidad de asignación se incluye como la **resource_associated_entity_id**.|  
|METADATA.ASSEMBLY|assembly_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_CLR_NAME|$qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_TOKEN|assembly_id = A, $token_id|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATOS. ASSYMMETRIC_KEY|asymmetric_key_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT|audit_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_ACTIONS|device_id = D, major_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_SPECIFICATION|audit_specification_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AVAILABILITY_GROUP|availability_group_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CERTIFICATE|certificate_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CHILD_INSTANCE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_FRAGMENT|object_id = O , compressed_fragment_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_ROW|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_ENDPOINT_RECV|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_ENDPOINT_SEND|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_GROUP|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_PRIORITY|conversation_priority_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CREDENTIAL|credential_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CRYPTOGRAPHIC_PROVIDER|provider_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATA_SPACE|data_space_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE|database_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE_PRINCIPAL|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_SESSION|database_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_WITNESS|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_PRINCIPAL_SID|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT|endpoint_id = E|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT_WEBMETHOD|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|fulltext_catalog_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_COLUMN|object_id = O, column_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_HASH|object_id = O, $hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|fulltext_catalog_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_STOPLIST|fulltext_stoplist_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEX_EXTENSION_SCHEME|index_extension_id = I|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEXSTATS|object_id = O, index_id o stats_id = I|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INSTANTIATED_TYPE_HASH|user_type_id = U, hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.MESSAGE|message_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.METADATA_CACHE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PARTITION_FUNCTION|function_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PASSWORD_POLICY|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PERMISSIONS|class = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE|plan_guide_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA. PLAN_GUIDE_HASH|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA. PLAN_GUIDE_SCOPE|scope_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME|$qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME_HASH|$qname_scope_id = Q, $qname_hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.REMOTE_SERVICE_BINDING|remote_service_binding_id = R|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ROUTE|route_id = R|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SCHEMA|schema_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_CACHE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_DESCRIPTOR|sd_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SEQUENCE|$seq_type = S, object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER|server_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_EVENT_SESSIONS|event_session_id = E|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_PRINCIPAL|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE|service_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_BROKER_GUID|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_CONTRACT|service_contract_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_MESSAGE_TYPE|message_type_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.STATS|object_id = O, stats_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SYMMETRIC_KEY|symmetric_key_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.USER_TYPE|user_type_id = U|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COLLECTION|xml_collection_id = X|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COMPONENT|xml_component_id = X|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_INDEX_QNAME|object_id = O, $qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 Los siguientes XEvents se relacionan con la partición **conmutador** y regeneración de índices en línea. Para obtener información sobre la sintaxis, vea [ALTER TABLE &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-table-transact-sql.md) y [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 El XEvent existente **progress_report_online_index_operation** índice en línea, las operaciones se ha mejorado agregando **partition_number** y **partition_id**.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-sysdmtranlocks-with-other-tools"></a>A. Usar sys.dm_tran_locks con otras herramientas  
 En el ejemplo siguiente se trabaja con un escenario en el que una operación de actualización ha sido bloqueada por otra transacción. Mediante el uso de **sys.dm_tran_locks** y otras herramientas, se proporciona información acerca del bloqueo de recursos.  
  
```sql  
USE tempdb;  
GO  
  
-- Create test table and index.  
CREATE TABLE t_lock  
    (  
    c1 int, c2 int  
    );  
GO  
  
CREATE INDEX t_lock_ci on t_lock(c1);  
GO  
  
-- Insert values into test table  
INSERT INTO t_lock VALUES (1, 1);  
INSERT INTO t_lock VALUES (2,2);  
INSERT INTO t_lock VALUES (3,3);  
INSERT INTO t_lock VALUES (4,4);  
INSERT INTO t_lock VALUES (5,5);  
INSERT INTO t_lock VALUES (6,6);  
GO  
  
-- Session 1  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
  
BEGIN TRAN  
    SELECT c1  
        FROM t_lock  
        WITH(holdlock, rowlock);  
  
-- Session 2  
BEGIN TRAN  
    UPDATE t_lock SET c1 = 10  
```  
  
 La siguiente consulta mostrará información de bloqueo. El valor de `<dbid>` debe reemplazarse por el **database_id** desde **sys.databases**.  
  
```sql  
SELECT resource_type, resource_associated_entity_id,  
    request_status, request_mode,request_session_id,  
    resource_description   
    FROM sys.dm_tran_locks  
    WHERE resource_database_id = <dbid>  
```  
  
 La siguiente consulta devuelve información de objetos de la consulta anterior mediante `resource_associated_entity_id`. Esta consulta debe ejecutarse mientras se esté conectado a la base de datos que contiene el objeto.  
  
```  
SELECT object_name(object_id), *  
    FROM sys.partitions  
    WHERE hobt_id=<resource_associated_entity_id>  
```  
  
 La siguiente consulta mostrará información de bloqueo.  
  
```sql  
SELECT   
        t1.resource_type,  
        t1.resource_database_id,  
        t1.resource_associated_entity_id,  
        t1.request_mode,  
        t1.request_session_id,  
        t2.blocking_session_id  
    FROM sys.dm_tran_locks as t1  
    INNER JOIN sys.dm_os_waiting_tasks as t2  
        ON t1.lock_owner_address = t2.resource_address;  
```  
  
 Libere los recursos revirtiendo las transacciones.  
  
```sql  
-- Session 1  
ROLLBACK;  
GO  
  
-- Session 2  
ROLLBACK;  
GO  
```  
  
### <a name="b-linking-session-information-to-operating-system-threads"></a>b. Vincular información de sesión a subprocesos del sistema operativo  
 En el ejemplo siguiente se devuelve información que asocia un identificador de sesión con un identificador de subproceso de Windows. El rendimiento del subproceso puede supervisarse en el Monitor de rendimiento de Windows. Esta consulta no devuelve ningún Id. de sesión que esté actualmente inactiva.  
  
```sql  
SELECT STasks.session_id, SThreads.os_thread_id  
    FROM sys.dm_os_tasks AS STasks  
    INNER JOIN sys.dm_os_threads AS SThreads  
        ON STasks.worker_address = SThreads.worker_address  
    WHERE STasks.session_id IS NOT NULL  
    ORDER BY STasks.session_id;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_tran_database_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con transacciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
