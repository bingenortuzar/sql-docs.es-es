---
title: Propiedades del índice de texto completo (página programaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.schedule.f1
ms.assetid: a828e284-097e-4854-8c49-931934eb73bf
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 067c77839a852965c7684359acf50fb328d21a6a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779035"
---
# <a name="full-text-index-properties-schedules-page"></a>Propiedades del índice de texto completo (página Programaciones)
  Utilice esta página con el fin de ver y crear calendarios para ejecutar un trabajo del Agente SQL Server que inicia un rellenado incremental de actualizaciones en la tabla base del índice de texto completo. Si la tabla base o la vista no contienen ninguna columna del tipo de datos `timestamp`, se realiza un rellenado completo.  
  
 **Para ver o cambiar las propiedades de un índice de texto completo**  
  
-   [Administrar índices de texto completo](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Programaciones**  
 Enumera cada rellenado incremental programado, si lo hay, en la tabla base para el índice de texto completo.  
  
 **Name**  
 Muestra el nombre de cada rellenado programado.  
  
 **Tipo de rellenado**  
 Muestra el tipo de cada rellenado programado.  
  
 **Enabled**  
 Indica si el rellenado programado está habilitado o deshabilitado actualmente.  
  
 **Descripción**  
 Muestra la descripción que se especificó cuando se creó la programación.  
  
 **Nueva**  
 Haga clic en esta opción si desea crear una programación nueva para rellenar el índice de texto completo.  
  
## <a name="see-also"></a>Vea también  
 [Use el Asistente para indización de texto completo](../relational-databases/search/use-the-full-text-indexing-wizard.md)   
 [Rellenar índices de texto completo](../relational-databases/search/populate-full-text-indexes.md)  
  
  
