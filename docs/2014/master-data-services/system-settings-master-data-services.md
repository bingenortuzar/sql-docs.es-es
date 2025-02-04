---
title: Configuración del sistema (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- Master Data Services, system settings
- system settings [Master Data Services]
ms.assetid: 83075cdf-f059-4646-8ba2-19be8202f130
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a411290435a10e351c05e9dd1350bde597dbe449
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478820"
---
# <a name="system-settings-master-data-services"></a>Configuración del sistema (Master Data Services)
  Para todas las aplicaciones web y servicios web asociados a la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , puede configurar las opciones del sistema.  
  
 Muchas de estas opciones se pueden configurar en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] en la página **Base de datos** . Otras se pueden configurar en la tabla Configuración del sistema (mdm.tblSystemSetting) en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 La configuración puede agruparse en las siguientes categorías:  
  
-   [Configuración general](#General)  
  
-   [Configuración de la administración de versiones](#Versions)  
  
-   [Configuración del almacenamiento provisional](#Staging)  
  
-   [Configuración del Explorador](#Explorer)  
  
-   [Configuración del complemento para Excel](#xls)  
  
-   [Configuración de las reglas de negocios](#BusinessRules)  
  
-   [Configuración de notificaciones](#Notifications)  
  
-   [Configuración de seguridad](#Security)  
  
-   [No se utiliza](#NotUsed)  
  
##  <a name="General"></a> Configuración general  
  
|Configuración del Administrador de configuración|Configuración del sistema|Descripción|  
|-----------------------------------|--------------------|-----------------|  
|**Tiempo de espera de conexión de la base de datos**|**DatabaseConnectionTimeOut**|El número de segundos que la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] espera para que una conexión se complete. Si la conexión no se completa en este tiempo, la conexión se cancela y se devuelve un error. El valor predeterminado es **60** segundos (1 minuto).|  
|**Tiempo de espera de conexión de un comando de base de datos**|**DatabaseCommandTimeOut**|El número de segundos que la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] espera para que un comando se complete. Si el comando no se completa dentro de este tiempo, se cancela y se devuelve un error. El valor predeterminado es **3600** segundos (60 minutos).|  
|**Tiempo de espera del servicio web**|**ServerTimeOut**|El número de segundos que ASP.NET espera a que se complete la solicitud de una página de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Si la solicitud no se completa dentro de este tiempo, se cancela y se devuelve un error. El valor predeterminado es **120000** segundos (2000 minutos).|  
|**Tiempo de espera de cliente**|**ClientTimeOut**|El número de segundos de inactividad antes de que [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] vuelva a la página principal. El valor predeterminado es **300** segundos (5 minutos).|  
|**Número de filas por lote**|**RowsPerBatch**|El número de registros que se van a recuperar en cada lote del servicio web. El valor predeterminado es **50**.|  
||**ApplicationName**|El texto que se muestra en los registros de eventos. El valor predeterminado es **MDM**.|  
||**SiteTitle**|El texto que se muestra en la barra de título del explorador web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . El valor predeterminado es **Administrador de datos maestros**.|  
  
##  <a name="Versions"></a> Configuración de la administración de versiones  
  
|Configuración del Administrador de configuración|Configuración del sistema|Descripción|  
|-----------------------------------|--------------------|-----------------|  
|**Copiar solo las versiones confirmadas**|**CopyOnlyCommittedVersion**|En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], determina si los usuarios pueden copiar versiones de modelos con el estado **Confirmado**o las versiones con cualquier tipo de estado. El valor predeterminado es **Sí** o **1**, que indica que los usuarios solo pueden copiar las versiones **Confirmadas** . Cambie a **No** o **2** , para permitir que los usuarios copien todas las versiones.|  
  
 Para más información, vea [Versiones &#40;Master Data Services&#41;](versions-master-data-services.md).  
  
##  <a name="Staging"></a> Configuración del almacenamiento provisional  
  
|Configuración del Administrador de configuración|Configuración del sistema|Descripción|  
|-----------------------------------|--------------------|-----------------|  
|**Registrar todas las transacciones de almacenamiento provisional**|**StagingTransactionLogging**|Solo se aplica a SQL Server 2008 R2. Determina si se van a registrar o no todas las transacciones cuando se cargan los registros de almacenamiento provisional en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . El valor predeterminado es **Off** o **2**. Cambie a **On** o **1** para activar el registro.|  
|**Intervalo del lote de almacenamiento provisional**|**StagingBatchInterval**|En el área funcional de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **de** , número de segundos después de seleccionar **Iniciar lotes** en que se procesa un lote. El valor predeterminado es **60** segundos (1 minuto).|  
  
 Para más información, vea [Importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
##  <a name="Explorer"></a> Configuración del Explorador  
  
|Configuración del Administrador de configuración|Configuración del sistema|Descripción|  
|-----------------------------------|--------------------|-----------------|  
|**Número predeterminado de miembros en la jerarquía**|**HierarchyChildNodeLimit**|En el área funcional del **Explorador** de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], el número máximo de miembros que se muestran en cada nodo de la jerarquía antes de que se muestre **...más...** . Puede hacer clic en **...más...** para mostrar el grupo siguiente de miembros. El valor predeterminado es **50**.|  
|**Mostrar nombres en jerarquía de manera predeterminada**|**ShowNamesInHierarchy**|En el área funcional del [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **de** , determina la configuración predeterminada que se selecciona al ver jerarquías.<br /><br /> El valor predeterminado es **Sí** o **1**, que indica que se muestran el nombre y el código de cada miembro. Cambie a **No** o **2** para mostrar solo el código.|  
|**Número de atributos basados en dominio de la lista**|**DBAListRowLimit**|En el área funcional del [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **Explorer** functional area, the number of attributes that are displayed in a list when you double-click a domain-based attribute value in the grid. El valor predeterminado es **50**. Si hay más de 50 miembros, en su lugar se muestra un cuadro de diálogo en el que se puede buscar.|  
||**GridFilterDefaultFuzzySimilarityLevel**|En el área funcional del [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **de** , nivel de similitud que se usa cuando se utiliza el criterio de filtro **Coincide** . El valor predeterminado es **0.3**. Establezca el valor más próximo a **1** para devolver una coincidencia que se aproxime más al criterio de búsqueda. Establezca el valor en **1** para obtener una coincidencia exacta.|  
  
##  <a name="xls"></a> Configuración del complemento para Excel  
  
|Configuración del Administrador de configuración|Configuración del sistema|Descripción|  
|-----------------------------------|--------------------|-----------------|  
|Mostrar el complemento del texto de Excel en la página principal del sitio web|ShowAddInText|En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , muestra un vínculo para que los usuarios puedan descargar [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].|  
|Ruta de instalación del complemento de Excel en la página principal del sitio web|AddInURL|En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , si se muestra el vínculo a [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] , la ubicación a la que se dirigen los usuarios al hacer clic en el vínculo.|  
  
##  <a name="BusinessRules"></a> Configuración de las reglas de negocios  
  
|Configuración del Administrador de configuración|Configuración del sistema|Descripción|  
|-----------------------------------|--------------------|-----------------|  
|**Incrementar nuevas reglas de negocios en**|**BusinessRuleDefaultPriorityIncrement**|En el área funcional de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **de** , número en que se incrementa la prioridad de cada nueva regla de negocio. El valor predeterminado es **10**.|  
|**Número de miembros a los que aplicar las reglas de negocios**|**BusinessRuleRealtimeMemberCount**|En el área funcional [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **de** , número máximo de miembros en la cuadrícula al que se van a aplicar las reglas de negocios. En [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)], número máximo de miembros en la hoja de cálculo activa a los que se van a aplicar reglas de negocios. El valor predeterminado es **10000**.|  
  
 Para más información, vea [Reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md).  
  
##  <a name="Notifications"></a> Configuración de notificaciones  
  
|Configuración del Administrador de configuración|Configuración del sistema|Descripción|  
|-----------------------------------|--------------------|-----------------|  
|**Dirección URL de Master Data Manager para notificaciones**|**MDMRootURL**|La dirección URL de la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], que se usa en el vínculo en las notificaciones por correo electrónico; por ejemplo, http://constoso/mds.|  
|**Intervalo de las notificaciones de correo electrónico**|**NotificationInterval**|La frecuencia, en segundos, con la que se envían las notificaciones de correo electrónico. El valor predeterminado es **120** segundos (2 minutos).|  
|**Número de notificaciones en un solo correo electrónico**|**NotificationsPerEmail**|El número máximo de problemas de validación que se enumerarán en un solo correo electrónico de notificación. Los problemas adicionales, si los hay, no se incluyen en el correo electrónico, pero están disponibles en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].|  
|**Formato de correo electrónico predeterminado**|**EmailFormat**|El formato de todas las notificaciones de correo electrónico. El valor predeterminado es **HTML** o **1**. La configuración de la base de datos **2** indica **Texto**.<br /><br /> Nota: Puede invalidar esta opción para un usuario individual en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], si cambia y guarda el **Formato de correo electrónico** en la pestaña **General** del usuario.|  
|**Expresión regular para la dirección de correo electrónico**|**EmailRegExPattern**|En el área funcional de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **de** , expresión regular que se utiliza para validar la dirección de correo electrónico escrita en la pestaña **General** del usuario. Para obtener más información sobre las expresiones regulares, consulte [Elementos del lenguaje de expresiones regulares](https://go.microsoft.com/fwlink/?LinkId=164401) en MSDN Library.|  
|**Cuenta de Correo electrónico de base de datos**|**EmailProfilePrincipalAccount**|Muestra la cuenta de Correo electrónico de base de datos que utilizar al enviar notificaciones de correo electrónico. El perfil predeterminado es **mds_email_user**.|  
|**Perfil de Correo electrónico de base de datos**|**DatabaseMailProfile**|El perfil de Correo electrónico de base de datos que utilizar al enviar notificaciones de correo electrónico. Está en blanco de forma predeterminada.|  
||**ValidationIssueHTML**|En formato HTML, texto que los usuarios de correo electrónico obtienen cuando una regla de negocios produce un error en la validación.|  
||**ValidationIssueText**|En formato de texto plano, texto que los usuarios de correo electrónico obtienen cuando una regla de negocios produce un error en la validación.|  
||**VersionStatusChangeText**|En formato de texto plano, texto que los usuarios de correo electrónico obtienen cuando el estado de una versión cambia. Solo los usuarios con permiso **Actualizar** para el modelo completo reciben este correo electrónico.|  
||**VersionStatusChangeHTML**|En el formato HTML, texto que los usuarios de correo electrónico obtienen cuando el estado de una versión cambia. Solo los usuarios con permiso **Actualizar** para el modelo completo reciben este correo electrónico.|  
  
 Para más información, vea [Notificaciones &#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md).  
  
##  <a name="Security"></a> Configuración de seguridad  
  
|Configuración del Administrador de configuración|Configuración del sistema|Descripción|  
|-----------------------------------|--------------------|-----------------|  
||**SecurityMemberProcessInterval**|En el área funcional de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] **de** , frecuencia, en segundos, con que se aplican los permisos de usuario y de grupo establecidos en la pestaña **Miembros de la jerarquía** . El valor predeterminado es **3600** segundos (60 minutos).|  
  
 Para obtener más información, consulte [Aplicar inmediatamente los permisos de los miembros &#40;Master Data Services&#41;](../../2014/master-data-services/immediately-apply-member-permissions-master-data-services.md).  
  
##  <a name="NotUsed"></a> No se utiliza  
 La siguiente configuración de la tabla Configuración del sistema no se usa.  
  
-   **SecurityMode**  
  
-   **MDSHubName**  
  
-   **ApplicationLogging**  
  
-   **ReportServer**  
  
-   **ReportDirectory**  
  
-   **BusinessRuleEngineIterationLimit**  
  
-   **BusinessRuleExtensibility**  
  
-   **AttributeExplorerMarkAllActionMemberCount**  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de objetos de base de datos &#40;Master Data Services&#41;](../../2014/master-data-services/database-object-security-master-data-services.md)  
  
  
