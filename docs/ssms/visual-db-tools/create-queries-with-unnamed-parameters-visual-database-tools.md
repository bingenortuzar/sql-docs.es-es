---
title: Crear consultas con parámetros sin nombre (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c515625ca08555065cd33ecfe1b83de08773260f
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264326"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>Crear consultas con parámetros sin nombre (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede crear una consulta con un parámetro sin nombre incluyendo un signo de interrogación (?) como marcador de posición para un valor literal. El Diseñador de consultas y vistas le asignará un nombre temporal. Puede especificar tantos parámetros sin nombre como necesite en la consulta.  
  
Cuando se ejecute la consulta en el Diseñador de consultas y vistas, se mostrará el cuadro de diálogo Parámetros de la consulta con el nombre temporal.  
  
### <a name="to-specify-an-unnamed-parameter"></a>Para especificar un parámetro sin nombre  
  
1.  Agregue las columnas o expresiones que desea buscar al [panel Criterios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md). Si no desea que las columnas o expresiones de búsqueda aparezcan en los resultados de la consulta, quítelas como columnas de resultados.  
  
2.  Busque la fila que contiene la columna de datos o expresión que va a buscar y, luego, en la columna de cuadrícula **Filtro** , escriba un signo de interrogación (?).  
  
    De forma predeterminada, el Diseñador de consultas y vistas agrega el operador "=". No obstante, puede editar la celda para sustituir el operador por ">", "<" o cualquier otro operador de comparación SQL.  
  
## <a name="see-also"></a>Consulte también  
[Realizar consultas con parámetros &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
