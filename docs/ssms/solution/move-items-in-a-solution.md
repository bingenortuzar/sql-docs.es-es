---
title: Mover elementos en una solución | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- moving items
- solutions [SQL Server Management Studio], item relocation
- relocating items
ms.assetid: b40a24eb-f528-4e70-b26e-5eaf6e0ed1ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a23aea0f4040ca957d1a3866fdf1d63eaf220085
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262817"
---
# <a name="move-items-in-a-solution"></a>Mover elementos en una solución
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Los elementos de proyecto en los proyectos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] son las consultas, las conexiones y los archivos varios. Puede mover consultas y archivos varios entre proyectos en el Explorador de soluciones. Sin embargo, las conexiones no se pueden mover.  
  
### <a name="to-move-items-in-solution-explorer"></a>Para mover elementos en el Explorador de soluciones  
  
1.  En el Explorador de soluciones, seleccione el elemento que desea mover.  
  
2.  En el menú **Editar** , haga clic en **Cortar**.  
  
3.  En el Explorador de soluciones, seleccione el destino.  
  
4.  En el menú **Editar** , haga clic en **Pegar**.  
  
Puede mover elementos si arrastra consultas y archivos varios dentro del Explorador de soluciones. La acción de arrastrarlos permite ver el resultado de la operación. El mover consultas de un tipo de proyecto a otro puede dar lugar a que éstas se consideren del tipo archivos varios en el proyecto de destino.  
  
> [!NOTE]  
> El mover una consulta conectada no mueve la conexión al proyecto de destino. La consulta perderá su conexión si se mueve al proyecto de destino.  
  
## <a name="see-also"></a>Consulte también  
[Explorador de soluciones](../../ssms/solution/solution-explorer.md)  
[Copiar elementos de una solución](../../ssms/solution/copy-items-in-a-solution.md)  
  
