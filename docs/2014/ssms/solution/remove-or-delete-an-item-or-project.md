---
title: Quitar o eliminar un elemento o un proyecto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dd6d04b186c68b128ad35ec5e5bd8b92ad1541c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035701"
---
# <a name="remove-or-delete-an-item-or-project"></a>Quitar o eliminar un elemento o un proyecto
  Los elementos de proyecto en los proyectos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] son las consultas, las conexiones y los archivos varios. Se pueden quitar consultas y archivos varios del proyecto de una solución sin borrar los archivos almacenados. Quite un proyecto o un elemento que no sea útil para la solución actual, pero que desee incluir en otra solución.  
  
### <a name="to-remove-a-project-item"></a>Para quitar un elemento de un proyecto  
  
1.  En el Explorador de soluciones, seleccione el elemento del proyecto que desea quitar.  
  
2.  En el menú **Editar** , haga clic en **Quitar**.  
  
3.  En el cuadro de diálogo de confirmación, haga clic en **Quitar** para quitar el elemento del proyecto.  
  
 Un elemento quitado aún se encuentra en el sistema de archivos. Por lo tanto, puede agregar ese elemento quitado a la solución original o a otra solución.  
  
#### <a name="to-remove-a-project"></a>Para quitar un proyecto  
  
1.  En el Explorador de soluciones, seleccione el proyecto que desea quitar.  
  
2.  En el menú **Editar** , haga clic en **Quitar**.  
  
3.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**para quitar el proyecto de la solución.  
  
 Un proyecto se puede eliminar de forma permanente, pero primero es necesario quitar todas las referencias al mismo de las soluciones de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y, a continuación, utilizar el Explorador de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para eliminar de forma permanente los archivos asociados almacenados.  
  
#### <a name="to-delete-a-project"></a>Para eliminar un proyecto  
  
1.  En el Explorador de soluciones, quite el proyecto que desea eliminar de la solución.  
  
2.  En el Explorador de Windows, busque y seleccione los archivos asociados al proyecto o elemento que desea eliminar.  
  
3.  En el menú **Archivo** , haga clic en **Eliminar**.  
  
## <a name="see-also"></a>Vea también  
 [Explorador de soluciones](solution-explorer.md)   
 [Agregar nuevos elementos a un proyecto](add-new-items-to-a-project.md)   
 [Agregar elementos existentes a un proyecto](add-existing-items-to-a-project.md)  
  
  
