---
title: Novedades de Data Migration Assistant (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: 2a4780c9be50275959a0f32091b90c518ccea124
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000593"
---
# <a name="whats-new-in-data-migration-assistant"></a>Novedades de Data Migration Assistant
En este artículo se enumeran las adiciones en cada versión de Data Migration Assistant (DMA).

## <a name="dma-v45"></a>DMA v 4.5

La versión v 4.5 de DMA proporciona compatibilidad para la evaluación de la migración de paquetes SQL Server Integration Services (SSIS) hospedados en el sistema de archivos a Azure SQL Database o Azure SQL Database instancia administrada.

## <a name="dma-v44"></a>DMA v 4.4

La versión v 4.4 de DMA proporciona compatibilidad para cargar evaluaciones en Azure Migrate.

## <a name="dma-v43"></a>DMA v 4.3

La versión v 4.3 de DMA proporciona compatibilidad con:

* Recomendaciones de SKU para instancias administradas de Azure SQL Database basadas en la evaluación de la carga de trabajo.
* RDS SQL Server como origen para las evaluaciones.
* Evaluaciones de trabajos del agente para la instancia administrada de Azure SQL Database como destino.
* La capacidad de omitir determinadas reglas de evaluación; la lista de códigos de error especificada en la propiedad ' ignoreErrorCodes ' configurada en DMA no se mostrará en los resultados de la evaluación de DMA.
* Evaluación de consultas de T-SQL en los pasos de la actividad de trabajo y proporcionar las recomendaciones adecuadas
* Evaluaciones de eventos extendidos (versión preliminar pública).

Además, esta versión de DMA proporciona un rendimiento mejorado para controlar un gran número de objetos de esquema en bases de datos, así como correcciones de errores relacionados con:

* Procedimientos compilados con compilación nativa, en algunos casos.
* Esquemas de base de datos complicados.

## <a name="dma-v42"></a>DMA v 4.2

La versión v 4.2 de DMA proporciona compatibilidad con la línea de comandos para la evaluación de la preparación de destino para una o varias instancias del servidor al migrar desde el SQL Server local a una instancia administrada de Azure SQL Database. Los clientes ahora pueden utilizar la línea de comandos de DMA para recopilar metadatos sobre el esquema de la base de datos, detectar los bloqueadores y obtener información sobre las características parcialmente compatibles o no admitidas que afectan a la migración a una instancia administrada de Azure SQL Database. Después, los resultados se pueden representar mediante el Power BI plantilla proporcionada.

## <a name="dma-v41"></a>DMA v 4.1

La versión v 4.1 de DMA incorpora compatibilidad para la evaluación completa de bases de datos locales de SQL Server que migran a Instancia administrada de Azure SQL Database.

El flujo de trabajo de evaluación le ayuda a detectar los siguientes problemas, lo que puede afectar a la migración a Instancia administrada de Azure SQL Database:

* **Características no admitidas o parcialmente admitidas**. DMA evalúa la base de datos de SQL Server de origen para las características en uso que se admiten parcialmente o no se admiten en el Instancia administrada de Azure SQL Database de destino. A continuación, la herramienta proporciona un conjunto completo de recomendaciones, enfoques alternativos disponibles en Azure y mitigando los pasos para que los clientes puedan tener en cuenta esta información al planear sus proyectos de migración.

* **Problemas de compatibilidad**. DMA también identifica problemas de compatibilidad relacionados con las siguientes áreas:

  * Cambios importantes:  Los objetos de esquema específicos que pueden interrumpir la funcionalidad de migración a la base de datos de destino.  Se recomienda corregir estos objetos de esquema después de la migración de la base de datos.
  * Cambios de comportamiento: Los objetos de esquema que se indican pueden seguir funcionando, pero pueden presentar un comportamiento diferente, por ejemplo, una degradación del rendimiento.
  * Problemas informativos:  Estos objetos no afectarán a la migración, pero pueden haber quedado en desuso de las versiones de SQL Server de características.

Una vez completada la evaluación, use nuestro [Azure Database Migration Service](https://azure.microsoft.com/services/database-migration/) (DMS) para realizar la migración de las bases de datos de SQL Server a instancia administrada de Azure SQL Database.  DMS admite migraciones de bases de datos [sin conexión](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance) (de un solo uso) y [en línea](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online) (tiempo de inactividad mínimo) a instancia administrada de Azure SQL Database.

## <a name="dma-v40"></a>DMA v 4.0

La versión v 4.0 de DMA presenta la característica de recomendaciones de SKU Azure SQL Database, que permite a los usuarios identificar la SKU mínima recomendada Azure SQL Database basada en los contadores de rendimiento recopilados en los equipos que hospedan las bases de datos. Esta característica proporciona recomendaciones relacionadas con el plan de tarifa, el nivel de proceso y el tamaño máximo de los datos, así como el costo estimado al mes. También ofrece la posibilidad de aprovisionar todas las bases de datos en Azure de forma masiva.

> [!NOTE]
> Actualmente, esta funcionalidad solo está disponible a través de la interfaz de la línea de comandos (CLI).

Para obtener más información, consulte el artículo [identificación de la SKU de Azure SQL Database adecuada para la base de datos local](dma-sku-recommend-sql-db.md).

## <a name="dma-v36"></a>DMA v 3.6

La versión v 3.6 de DMA presenta "corrección automática" para los objetos de esquema que se ven afectados por los bloqueadores de migración más comunes.

Esta versión proporciona AutoFix para los siguientes problemas de bloqueo de migración y comportamiento:

* Los objetos de esquema que utilizan la sintaxis de combinación incompleta.
* Los objetos de esquema que utilizan la instrucción RAISEERROR heredada.
* Instrucciones SQL que utilizan un literal de tipo order by.

DMA realiza la conversión automática de esquemas para los objetos afectados por los problemas enumerados y solicita confirmación al usuario antes de continuar con la conversión del esquema. Los usuarios pueden revisar los cambios sugeridos en el código y aceptar o rechazar todas las conversiones de cualquier objeto de base de datos determinado.

DMA usa la tecnología de síntesis de programa de Microsoft (PROSE) para sugerir correcciones de código. Más información sobre [PROSE](https://microsoft.github.io/prose/).

## <a name="dma-v35"></a>DMA v 3.5

La versión v 3.5 de DMA incluye las siguientes adiciones:

* Mejoras de rendimiento significativas para la migración a Azure SQL Database (las pruebas comparativas indican que el proceso es cuatro veces más rápido que con versiones anteriores de DMA).
* La superficie de memoria se optimiza aún más para mejorar la estabilidad del flujo de trabajo de migración.
* La capacidad de omitir las evaluaciones durante el esquema y las migraciones de datos (si ya ha realizado la evaluación y ha solucionado todos los objetos de esquema de interrupción antes de la migración).
* Una corrección para solucionar un problema con la herramienta que se bloquea cuando se proporciona una ruta de acceso de recurso compartido de red no válida para los archivos de copia de seguridad, al realizar una actualización de una versión heredada de SQL Server local a una versión posterior o a SQL Server en máquinas virtuales de Azure.

## <a name="dma-v34"></a>DMA v 3.4

La versión v 3.4 de DMA incluye las siguientes adiciones:

* Compatibilidad con SQL Server 2017 como origen para las migraciones a Azure SQL Database.
* Mejoras en la estabilidad, el rendimiento y la corrección de la regla de evaluación.

## <a name="dma-v33"></a>DMA v 3.3

La versión v 3.3 de DMA permite la migración de una instancia de SQL Server local a la nueva versión de SQL Server 2017, tanto en Windows como en Linux. Aunque el flujo de trabajo general de migración para Windows y Linux es el mismo, el cambio a SQL Server 2017 para Linux requiere un par de consideraciones adicionales.

### <a name="specifying-the-back-up-path"></a>Especificación de la ruta de acceso de copia de seguridad

Linux y Windows usan distintos formatos de ruta de acceso. Como resultado, la migración a SQL Server 2017 en Linux requiere que el usuario proporcione las versiones de Windows y Linux de la ruta de acceso a la ubicación del archivo físico. Puede proporcionar ambas versiones de la ruta de acceso de maneras diferentes, en función de la ubicación del archivo físico.
Si el archivo de copia de seguridad físico se encuentra en un equipo que ejecuta:

* Linux, use un recurso compartido de "Samba" para compartir el archivo con otros equipos de la red.
* Windows, use el comando ' mnt ' para montar el recurso compartido en el equipo que ejecuta Linux.

> [!NOTE]
> Los detalles sobre el uso de un recurso compartido de "Samba" o el comando "mnt" quedan fuera del ámbito de este artículo.

### <a name="migrating-windows-logins"></a>Migrar inicios de sesión de Windows

Aunque la migración de inicios de sesión de Active Directory (AD) es oficialmente compatible con SQL Server 2017 en Linux, requiere una configuración adicional para funcionar correctamente. Consulte el artículo [Active Directory la autenticación con SQL Server en Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication) para obtener información detallada sobre la configuración de inicios de sesión de Active Directory en SQL Server 2017 en Linux. Después de realizar la configuración necesaria, se completa la instalación y puede migrar los inicios de sesión de Active Directory como de costumbre. La autenticación de SQL estándar funciona según lo previsto sin necesidad de ninguna configuración adicional.

## <a name="dma-v32"></a>DMA v 3.2

La versión v 3.2 de DMA incluye las siguientes adiciones:

* La migración de esquemas y datos se habilita desde las bases de datos locales de SQL Server para Azure SQL Database con un nuevo flujo de trabajo de migración.
* Durante la migración de esquemas a Azure SQL Database, los scripts de DMA de los objetos de base de datos de origen proporcionan instrucciones sobre cómo corregir los posibles problemas de compatibilidad y, a continuación, se implementa el esquema en Azure.

## <a name="dma-v31"></a>DMA v 3.1

La versión v 3.1 de DMA incluye las siguientes adiciones:

* Recomendaciones de evaluación mejoradas para las bases de datos SQL de Azure en lo que respecta a las intercalaciones de base de datos, el uso de procedimientos almacenados del sistema no admitidos y objetos CLR.
* Instrucciones de evaluación de los niveles de compatibilidad 130, 120, 110 y 100 al migrar a bases de datos SQL de Azure.

## <a name="dma-v30"></a>DMA v 3.0

La versión v 3.0 de DMA amplía la evaluación de Azure SQL Database para proporcionar recomendaciones completas que le ayuden a solucionar problemas relacionados con:

* Problemas de bloqueo de la migración.
* Características y funciones parciales o no admitidas.

## <a name="dma-v21"></a>DMA v 2.1

La versión v 2.1 de DMA incluye las siguientes adiciones:

* Compatibilidad de la línea de comandos para ejecutar evaluaciones en modo desatendido, lo que ayuda a ejecutar evaluaciones a escala. Para obtener detalles adicionales, consulte el artículo [ejecución de Data Migration Assistant desde la línea de comandos](dma-commandline.md).
* Mejoras de rendimiento cuando los usuarios inician y cierran DMA.
* La capacidad de configurar el tiempo de espera de conexión SQL. Para obtener detalles adicionales, consulte los [valores de configuración del artículo para obtener Data Migration Assistant](dma-configurationsettings.md).

## <a name="dma-v20"></a>DMA v 2.0

La versión v 2.0 de DMA incluye recomendaciones de características de stretch Database mejoradas para proporcionar tablas con prioridades adecuadas que maximicen el ahorro de almacenamiento.

## <a name="dma-v10"></a>DMA v 1.0

La versión v 1.0 de DMA es la versión inicial y proporciona:

* Detección de problemas que pueden afectar a una actualización a una versión local de SQL Server. Los hallazgos se describen como problemas de compatibilidad y se clasifican en las siguientes áreas:
  * Cambios importantes
  * Cambios de comportamiento
  * Características en desuso
* Detección de nuevas características en la plataforma de SQL Server de destino en la que se puede beneficiar la base de datos después de una actualización. Los hallazgos se describen como recomendaciones de características y se clasifican en las siguientes áreas:
  * Rendimiento
  * Seguridad
  * Almacenamiento
* Experiencia de usuario moderna para realizar evaluaciones.

## <a name="see-also"></a>Vea también

[Información general de Data Migration Assistant](../dma/dma-overview.md)
