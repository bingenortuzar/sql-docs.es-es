---
title: Rendimiento (categoría de eventos) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Performance event category
- Performance event category [SQL Server]
- event classes [SQL Server], Performance event category
ms.assetid: 708f3585-d8be-4980-bbff-672d7c59397e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 42eb4676454f71bbc7b1dd1def4ec5de3d0b3867
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050415"
---
# <a name="performance-event-category"></a>Rendimiento (categoría de eventos)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Use la categoría de eventos **Performance** para supervisar las clases de eventos **Showplan** y las clases de eventos que se producen al ejecutar operadores de lenguaje de manipulación de datos (DML) de SQL.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Auto Stats (clase de eventos)](../../relational-databases/event-classes/auto-stats-event-class.md)|Indica que se ha producido una actualización automática de las estadísticas de índices y columnas.|  
|[Degree of Parallelism &#40;7.0 Insert&#41; clase de eventos](../../relational-databases/event-classes/degree-of-parallelism-7-0-insert-event-class.md)|Indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha ejecutado una instrucción SELECT, INSERT, UPDATE o DELETE utilizando un plan serie o paralelo. Se informa también del número de CPUs utilizadas para realizar la operación.|  
|[Performance Statistics (clase de eventos)](../../relational-databases/event-classes/performance-statistics-event-class.md)|Supervisa el rendimiento de las consultas que se están ejecutando.|  
|[Showplan All (clase de eventos)](../../relational-databases/event-classes/showplan-all-event-class.md)|Identifica los operadores de **Showplan** de una instrucción SQL.|  
|[Showplan All for Query Compile (clase de eventos)](../../relational-databases/event-classes/showplan-all-for-query-compile-event-class.md)|Muestra los datos de tiempo de compilación de los operadores de **Showplan** .|  
|[Showplan Statistics Profile (clase de eventos)](../../relational-databases/event-classes/showplan-statistics-profile-event-class.md)|Muestra el costo estimado de una consulta.|  
|[Showplan XML (clase de eventos)](../../relational-databases/event-classes/showplan-xml-event-class.md)|Identifica los operadores de **Showplan** en una instrucción SQL. La clase de eventos almacena cada evento como un documento XML bien definido.|  
|[Showplan XML For Query Compile (clase de eventos)](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)|Muestra los datos de tiempo de compilación de los operadores de **Showplan** en formato XML.|  
|[Showplan XML Statistics Profile (clase de eventos)](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)|Identifica los operadores de **Showplan** asociados a una instrucción SQL. La salida es un documento XML.|  
|[SQL:FullTextQuery (clase de eventos)](../../relational-databases/event-classes/sql-fulltextquery-event-class.md)|Indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha ejecutado una consulta de texto completo.|  
|[Clase de evento Guía de plan correcta](../../relational-databases/event-classes/plan-guide-successful-event-class.md)|Indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generó correctamente un plan de ejecución para una consulta o lote que contenía una guía de plan.|  
|[Clase de eventos Plan Guide Unsuccessful](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md)|Indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pudo generar un plan de ejecución para una consulta o lote que contenía una guía de plan.|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
