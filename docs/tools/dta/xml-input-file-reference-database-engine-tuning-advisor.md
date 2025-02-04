---
title: Referencia del archivo de entrada XML (Asistente para la optimización de motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], XML input files
- input file reference [Database Engine Tuning Advisor]
- XML input files [Database Engine Tuning Advisor]
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0572c0aa0b4a49a3c0ce471cb8194124fef73cdb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105783"
---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>Referencia del archivo de entrada XML (Asistente para la optimización de motor de base de datos)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] puede utilizar un archivo de entrada XML para optimizar una base de datos. Este archivo XML designa las bases de datos, las tablas, los archivos o las tablas de carga de trabajo y las opciones de optimización que se van a utilizar durante la sesión de optimización. También se puede utilizar este archivo para definir una configuración especificada por el usuario para realizar análisis de escenarios condicionales.  
  
 Un archivo de entrada XML del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] contiene una jerarquía de elementos XML. Cada uno de estos contiene texto u otros elementos que especifican la configuración de la sesión de optimización. El archivo de entrada XML del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe ajustarse a los estándares de formato XML correcto, de modo que todos los nombres de elemento distingan entre mayúsculas y minúsculas. Los elementos se especifican siguiendo el formato Pascal: el primer carácter y la primera letra de cualquier palabra concatenada siguiente van en mayúsculas.  
  
 Todos los valores de los elementos deben ajustarse a las convenciones de nomenclatura XML. Para obtener más información acerca de estas convenciones, vea el artículo sobre [contenido de texto XML](https://go.microsoft.com/fwlink/?LinkId=7614) en Microsoft MSDN Library.  
  
 Tenga en cuenta que esta referencia no es completa. Para obtener más información acerca de los elementos que se pueden utilizar para definir una entrada XML, vea el esquema XML del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] , DTASchema.xsd.  
  
## <a name="xml-declaration"></a>Declaración XML  
  
-   [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>Elemento raíz DTAXML  
  
-   [Elemento DTAXML &#40;DTA&#41;](../../tools/dta/dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>Elementos DTAInput  
  
-   [Elemento DTAInput &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)  
  
-   [Server &#40;DTA, elemento&#41;](../../tools/dta/server-element-dta.md)  
  
-   [Workload &#40;DTA, elemento&#41;](../../tools/dta/workload-element-dta.md)  
  
-   [Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
-   [Elemento Configuration &#40;DTA&#41;](../../tools/dta/configuration-element-dta.md)  
  
## <a name="server-elements"></a>Elementos Server  
  
-   [Elemento Name de Server &#40;DTA&#41;](../../tools/dta/name-element-for-server-dta.md)  
  
-   [Elemento Database de Server &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>Elementos Workload  
  
-   [Elemento File &#40;DTA&#41;](../../tools/dta/file-element-dta.md)  
  
-   [Database &#40;DTA, elemento de Workload&#41;](../../tools/dta/database-element-for-workload-dta.md)  
  
-   [Elemento EventString &#40;DTA&#41;](../../tools/dta/eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>Elementos de opciones de optimización  
  
-   [Elemento TuningTimeInMin &#40;DTA&#41;](../../tools/dta/tuningtimeinmin-element-dta.md)  
  
-   [Elemento StorageBoundInMB &#40;DTA&#41;](../../tools/dta/storageboundinmb-element-dta.md)  
  
-   [Elemento TestServer &#40;DTA&#41;](../../tools/dta/testserver-element-dta.md)  
  
-   [FeatureSet &#40;DTA, elemento&#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Partitioning &#40;DTA, elemento&#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [DropOnlyMode &#40;DTA, elemento&#41;](../../tools/dta/droponlymode-element-dta.md)  
  
-   [KeepExisting &#40;DTA, elemento&#41;](../../tools/dta/keepexisting-element-dta.md)  
  
-   [OnlineIndexOperation &#40;DTA, elemento&#41;](../../tools/dta/onlineindexoperation-element-dta.md)  
  
-   [Elemento DatabaseToConnect &#40;DTA&#41;](../../tools/dta/databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>Elementos Configuration  
  
-   [Server &#40;DTA, elemento de Configuration&#41;](../../tools/dta/server-element-for-configuration-dta.md)  
  
-   [Elemento Database de Configuration &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)  
  
-   [Elemento Recommendation &#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)  
  
-   [Create &#40;DTA, elemento&#41;](../../tools/dta/create-element-dta.md)  
  
-   [Index &#40;DTA, elemento&#41;](../../tools/dta/index-element-dta.md)  
  
-   [Name &#40;DTA, elemento de Index&#41;](../../tools/dta/name-element-for-index-dta.md)  
  
-   [Column &#40;DTA, elemento de Index&#41;](../../tools/dta/column-element-for-index-dta.md)  
  
-   [Elemento Name de Column &#40;DTA&#41;](../../tools/dta/name-element-for-column-dta.md)  
  
-   [Filegroup &#40;DTA. elemento de Index&#41;](../../tools/dta/filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>Elementos Database  
  
-   [Elemento Name de Database &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)  
  
-   [Elemento Schema de Database &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)  
  
-   [Elemento Name de Schema &#40;DTA&#41;](../../tools/dta/name-element-for-schema-dta.md)  
  
-   [Elemento Table de Schema &#40;DTA&#41;](../../tools/dta/table-element-for-schema-dta.md)  
  
-   [Elemento Name de Table &#40;DTA&#41;](../../tools/dta/name-element-for-table-dta.md)  
  
## <a name="see-also"></a>Consulte también  
 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
