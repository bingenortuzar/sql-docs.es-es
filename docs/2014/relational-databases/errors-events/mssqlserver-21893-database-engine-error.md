---
title: MSSQLSERVER_21893 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21893 (Database Engine error)
ms.assetid: 1ab1195a-fe2a-4e06-b871-b177b6bea1fe
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6258f36990efccf83b43e8d8ac8bd4c2397477aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914960"
---
# <a name="mssqlserver21893"></a>MSSQLSERVER_21893
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21893|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21893|  
|Texto del mensaje|Los suscriptores (%s) del publicador original "%s" no aparecen como servidores remotos en el publicador redireccionado "%s". Ejecute `sp_addlinkedserver` en el publicador redirigido para agregar estos suscriptores como servidores remotos.|  
  
## <a name="explanation"></a>Explicación  
 `sp_validate_redirected_publisher` usa las tablas de metadatos de suscripción de la base de datos del publicador en el servidor remoto para identificar sus suscriptores asociados y comprueba que hay entradas asociadas en master.dbo.sysservers para los suscriptores. Este error se devuelve si ninguno de los suscriptores identificados está presente.  
  
 Este error no se considera irrecuperable. Los agentes que encuentran este error lo registrarán como informativo pero no finalizarán, ya que un error que tenga las entradas de suscriptor adecuadas en el nuevo publicador tiene un impacto limitado en la replicación. Sin una entrada correspondiente para un suscriptor en sysservers, algunas de las actividades de administración de suscripciones pueden generar un error cuando se ejecutan a través de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No obstante, estas mismas actividades se pueden realizar correctamente mediante la ejecución de los procedimientos almacenados de administración de forma explícita.  
  
## <a name="user-action"></a>Acción del usuario  
 Ejecute `sp_addlinkedserver` en el publicador redireccionado por cada uno de los suscriptores identificados para agregarlos como servidores remotos. A continuación, ejecute `sp_serveroption` para establecer el bit de suscriptor para el servidor.  
  
  
