---
title: Reconciliar un diagrama de base de datos con una base de datos modificada (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- updating diagram to match database
- reconciling database diagrams
- diagrams [SQL Server], reconciling changes
- updating database to match diagram
- database diagrams [SQL Server], reconciling changes
ms.assetid: eda8dea2-eedd-43a7-85aa-92bd97783b5f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 37801a47dc7ee4df7253f554adc522798b964891
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266250"
---
# <a name="reconcile-a-database-diagram-with-a-modified-database-visual-database-tools"></a>Reconciliar un diagrama de base de datos con una base de datos modificada (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Debe guardar el diagrama de base de datos cuando esté preparado para actualizar la base de datos de forma que coincida con el diagrama. Sin embargo, si otros usuarios han actualizado la base de datos desde que abrió el diagrama, los cambios que hayan realizado podrían afectar al diagrama y viceversa.  
  
Cuando guarde el diagrama, la base de datos se reconciliará con el diagrama, sobrescribiéndose los cambios de los otros usuarios de forma que la base de datos coincida con su diagrama.  
  
### <a name="to-update-a-database-to-match-your-diagram"></a>Para actualizar una base de datos de forma que coincida con su diagrama  
  
1.  Guarde el diagrama de base de datos.  
  
    Si no guardó previamente el diagrama, escriba un nombre para el diagrama en el cuadro de diálogo **Guardar nuevo diagrama de base de datos** y elija **Aceptar**.  
  
2.  El cuadro de diálogo **Guardar** muestra las tablas que se verán afectadas cuando guarde el diagrama. Elija **Sí** para continuar.  
  
3.  En el cuadro de diálogo **Se han detectado cambios en la base de datos** se muestran los objetos que se han modificado y que se van a cambiar para que coincidan con su diagrama. Elija **Sí** para guardar el diagrama y aceptar la lista de cambios.  
  
    > [!NOTE]  
    > Si el diagrama contiene tablas y columnas que se eliminaron de la base de datos, solo se volverán a crear sus definiciones en la base de datos cuando guarde el diagrama. Este proceso no restaura los datos que existían en estos objetos antes de su eliminación.  
  
### <a name="to-update-your-diagram-to-match-a-modified-database"></a>Para actualizar su diagrama de forma que coincida con una base de datos modificada  
  
1.  Cierre su diagrama sin guardar los cambios.  
  
2.  Haga clic con el botón secundario en el diagrama en el Explorador de objetos.  
  
3.  En el menú contextual, haga clic en **Actualizar**.  
  
4.  Vuelva a abrir el diagrama.  
  
## <a name="see-also"></a>Consulte también  
[Trabajar con diagramas de base de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
