---
title: Conceptos de los ejecutables del Agente de replicación | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- programming interfaces [SQL Server replication]
- programming [SQL Server replication], agents
- replication [SQL Server], agents and profiles
- agents [SQL Server replication], executables
- command prompt [SQL Server replication]
ms.assetid: cba476df-d4ea-44c9-bb86-81488971e328
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 451b7ca4cc06269f116c62be2ef7f01f0e33abd2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721897"
---
# <a name="replication-agent-executables-concepts"></a>Conceptos de los ejecutables del Agente de replicación
  Los agentes de replicación se pueden controlar mediante programación de las maneras siguientes:  
  
-   Mediante las interfaces de programación del agente administrado en el espacio de nombres <xref:Microsoft.SqlServer.Replication>.  
  
-   Invocando a los archivos ejecutables de agente desde el símbolo del sistema con un conjunto proporcionado de parámetros.  
  
 Invocar directamente a los agentes de replicación desde el símbolo del sistema permite obtener acceso a los agentes mediante programación desde scripting de la línea de comandos en archivos por lotes. Cuando un agente se invoca desde el símbolo del sistema, se ejecuta en la cuenta de seguridad de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows del usuario que invocó al agente o inició el archivo por lotes.  
  
 Las instancias de los agentes de replicación siguientes se pueden ejecutar con archivos ejecutables.  
  
-   [Agente de distribución de replicación](../agents/replication-distribution-agent.md)  
  
-   [Agente de registro del LOG de replicación](../agents/replication-log-reader-agent.md)  
  
-   [Replication Merge Agent](../agents/replication-merge-agent.md)  
  
-   [Agente de lectura de cola de replicación](../agents/replication-queue-reader-agent.md)  
  
-   [Replication Snapshot Agent](../agents/replication-snapshot-agent.md)  
  
 Al invocar los agentes de replicación, puede utilizar los perfiles de rendimiento para pasar automáticamente un conjunto definido de parámetros a la aplicación ejecutable del agente. Para obtener más información, consulte [Replication Agent Profiles](../agents/replication-agent-profiles.md).  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes se muestra cómo invocar los agentes de replicación desde el símbolo del sistema. Los agentes de replicación también se pueden invocar utilizando Replication Management Objects (RMO). Para obtener más información, vea [Sincronizar suscripciones &#40;replicación&#41;](../synchronize-data.md).  
  
> [!NOTE]  
>  Los saltos de línea de estos ejemplos se agregaron para mejorar la legibilidad. En un archivo por lotes, los comandos se deben realizar en una única línea.  
  
### <a name="running-the-snapshot-agent"></a>Ejecutar el Agente de instantáneas  
 Este archivo por lotes de ejemplo invoca al Agente de instantáneas desde el símbolo del sistema para generar una instantánea para la publicación **AdvWorksSalesOrdersMerge**.  
  
```  
REM -- Declare variables  
SET Publisher=%InstanceName%;  
SET PublicationDB=AdventureWorks2012;   
SET Publication=AdvWorksSalesOrdersMerge;   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1 ;  
  
```  
  
### <a name="running-the-distribution-agent"></a>Ejecutar el Agente de distribución  
 Este archivo por lotes de ejemplo invoca al Agente de distribución desde el símbolo del sistema para replicar continuamente los cambios desde la publicación **AdvWorksProductTran** a un suscriptor de inserción.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksProductsTran;  
  
REM -- Start the Distribution Agent with four subscription streams.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\DISTRIB.EXE" -Subscriber %Subscriber%   
-SubscriberDB %SubscriptionDB% -SubscriberSecurityMode 1 -Publication %Publication%   
-Publisher %Publisher% -PublisherDB %PublicationDB% -Distributor %Publisher%   
-DistributorSecurityMode 1 -Continuous -SubscriptionType 0 -SubscriptionStreams 4 ;  
  
```  
  
### <a name="running-the-merge-agent"></a>Ejecutar el Agente de mezcla  
 Este archivo por lotes de ejemplo invoca al Agente de mezcla desde el símbolo del sistema para sincronizar una suscripción de extracción a la publicación **AdvWorksSalesOrdersMerge**.  
  
```  
REM -- Declare the variables.  
SET Publisher=%instancename%;  
SET Subscriber=%instancename%;  
SET PublicationDB=AdventureWorks2012;  
SET SubscriptionDB=AdventureWorks2012Replica;   
SET Publication=AdvWorksSalesOrdersMerge;  
  
REM --Start the Merge Agent with concurrent upload and download processes.  
REM -- The following command must be supplied without line breaks.  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE" -Publication %Publication%    
-Publisher %Publisher%  -Subscriber  %Subscriber%  -Distributor %Publisher%    
-PublisherDB %PublicationDB%  -SubscriberDB %SubscriptionDB% -PublisherSecurityMode 1    
-OutputVerboseLevel 2  -SubscriberSecurityMode 1  -SubscriptionType 1 -DistributorSecurityMode 1    
-Validate 3  -ParallelUploadDownload 1 ;  
  
```  
  
  
