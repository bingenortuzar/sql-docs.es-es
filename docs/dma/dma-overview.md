---
title: Información general de Data Migration Assistant (SQL Server) | Microsoft Docs
description: Aprenda a usar Data Migration Assistant para migrar bases de datos de SQL Server a otras bases de datos de SQL Server o de Azure.
ms.custom: ''
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: ac039906bddc700e9e0b2517d0e34274e088ad2e
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304705"
---
# <a name="overview-of-data-migration-assistant"></a>Información general de Data Migration Assistant
El Data Migration Assistant (DMA) le ayuda a actualizar a una plataforma de datos moderna mediante la detección de problemas de compatibilidad que pueden afectar a la funcionalidad de la base de datos en la nueva versión de SQL Server o Azure SQL Database. DMA recomienda mejoras de rendimiento y confiabilidad para el entorno de destino y permite trasladar el esquema, los datos y los objetos no contenidas del servidor de origen al servidor de destino.

> [!NOTE] 
> En el caso de las migraciones de gran tamaño (en cuanto al número y el tamaño de las bases de datos), se recomienda usar el [Azure Database Migration Service](/azure/dms/dms-overview), que puede migrar las bases de datos a escala.
  
## <a name="get-data-migration-assistant"></a>Obtener Data Migration Assistant
Para instalar DMA, descargue la versión más reciente de la herramienta en el [centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=53595)y, a continuación, ejecute el archivo **DataMigrationAssistant. msi** .

## <a name="capabilities"></a>Capabilities
- Evalúe las instancias locales de SQL Server migrar a Azure SQL Database (s). El flujo de trabajo de evaluación le ayuda a detectar los siguientes problemas que pueden afectar a la migración de Azure SQL Database y proporciona instrucciones detalladas sobre cómo resolverlos.

  - Problemas de bloqueo de la migración: Detecta los problemas de compatibilidad que bloquean la migración de bases de datos SQL Server locales a Azure SQL Database. DMA proporciona recomendaciones para ayudarle a solucionar esos problemas.

  - Características admitidas parcialmente o no admitidas: Detecta características parcialmente admitidas o no admitidas que se están usando actualmente en la instancia de SQL Server de origen. DMA proporciona un conjunto completo de recomendaciones, enfoques alternativos disponibles en Azure y procedimientos de mitigación para que pueda incorporarlos en los proyectos de migración.

- Detectar problemas que pueden afectar a una actualización a un SQL Server local. Estos se describen como problemas de compatibilidad y se organizan en las siguientes categorías:

  - Cambios importantes
  - Cambios de comportamiento
  - Características en desuso

- Descubra las nuevas características de la plataforma de SQL Server de destino de las que puede beneficiarse la base de datos después de una actualización. Se describen como recomendaciones de características y se organizan en las siguientes categorías:

  - Rendimiento
  - Seguridad
  - Almacenamiento

- Migre una instancia de SQL Server local a una instancia de SQL Server moderna hospedada localmente o en una máquina virtual (VM) de Azure que sea accesible desde la red local. Se puede tener acceso a la máquina virtual de Azure mediante VPN u otras tecnologías. El flujo de trabajo de migración le ayuda a migrar los componentes siguientes:

  - Esquema de bases de datos
  - Datos y usuarios
  - Roles del servidor
  - Inicios de sesión de SQL Server y Windows

- Después de una migración correcta, las aplicaciones pueden conectarse a las bases de datos de SQL Server de destino sin problemas.

- Evalúe los paquetes de SQL Server Integration Services local (SSIS) que migran a Azure SQL Database o Azure SQL Database instancia administrada. La evaluación ayuda a detectar problemas que pueden afectar a la migración. Estos se describen como problemas de compatibilidad y se organizan en las siguientes categorías:

  - Bloqueadores de migración: detecta los problemas de compatibilidad que bloquean la migración de paquetes de origen a Azure. DMA proporciona recomendaciones para ayudarle a solucionar esos problemas.

  - Problemas de información: detecta características parcialmente admitidas o desusadas que se usan en los paquetes de origen.

  > [!NOTE]
  > Solo se admite la evaluación de paquetes hospedados en el sistema de archivos.
  > La evaluación de los paquetes hospedados en MSDB, el almacén de paquetes o SSISDB se incluye más adelante.

## <a name="prerequisites"></a>Requisitos previos
Para ejecutar una evaluación, debe ser miembro del rol SQL Server **sysadmin** .

## <a name="supported-source-and-target-versions"></a>Versiones de origen y de destino admitidas
DMA reemplaza todas las versiones anteriores de SQL Server Asesor de actualizaciones y debe usarse para las actualizaciones de la mayoría de las versiones de SQL Server. Las versiones de origen y de destino admitidas son:

**Orígenes**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 en Windows

**Destinos**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 en Windows y Linux
- Se aplica a: Base de datos SQL de Azure
- Instancia administrada de Azure SQL Database
- SQL Server que se ejecuta en una máquina virtual de Azure

## <a name="see-also"></a>Vea también
[Evaluación de la migración de SQL Server](../dma/dma-assesssqlonprem.md)     
[Data Migration Assistant: Opciones de configuración](../dma/dma-configurationsettings.md)     
[Migre SQL Server local mediante Data Migration Assistant](../dma/dma-migrateonpremsql.md)     
[Data Migration Assistant: Procedimientos recomendados](../dma/dma-bestpractices.md)     
