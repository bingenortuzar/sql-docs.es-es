---
title: Agregar nuevos elementos a un proyecto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], item additions
- adding project items
ms.assetid: 76af8692-324f-4f5e-b1a0-d72ca8a107e3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cbec800c8d13914e0d1ddd54ac5014844995210e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62956104"
---
# <a name="add-new-items-to-a-project"></a>Agregar nuevos elementos a un proyecto
  Agregue elementos nuevos a un proyecto para ampliar la funcionalidad de la aplicación. Un elemento nuevo puede ser una consulta o una conexión. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tiene dos tipos de proyecto: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Proyecto de script y proyecto de script de Analysis Services. El tipo de proyecto determina los elementos que se pueden agregar al proyecto. Por ejemplo, se puede agregar una consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] (un archivo con una extensión .sql) a un proyecto de script de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pero no a un proyecto de script de Analysis Services.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no permite crear carpetas dentro de los proyectos. Para organizar el trabajo, cree varios proyectos dentro de la solución.  
  
### <a name="to-add-a-new-query-to-an-existing-project"></a>Para agregar una consulta nueva a un proyecto existente  
  
1.  En el Explorador de soluciones, seleccione el proyecto de destino.  
  
2.  En el menú **Proyecto** , haga clic en **Agregar nuevo elemento**.  
  
3.  En el cuadro de diálogo **Agregar nuevo elemento** , seleccione una categoría en el panel de la izquierda.  
  
4.  Seleccione una plantilla de consulta en el panel de la derecha y haga clic en **Agregar**. La consulta nueva se agrega a la carpeta **Consultas** del proyecto.  
  
5.  En el cuadro de diálogo **Conectar al motor de base de datos** , especifique una conexión para la consulta nueva y haga clic en **Conectar**. Si no desea asociar una conexión a la consulta nueva, puede hacer clic en **Cancelar** en el cuadro de diálogo de conexión.  
  
6.  Si lo desea, cambie el nombre de la consulta en el Explorador de soluciones.  
  
### <a name="to-add-a-new-connection-to-an-existing-project"></a>Para agregar una conexión nueva a un proyecto existente  
  
1.  En el Explorador de soluciones, seleccione el proyecto de destino.  
  
2.  En el menú **Proyecto** , haga clic en **Agregar nuevo elemento**.  
  
3.  Seleccione **Conexión** en el panel de la izquierda.  
  
4.  Seleccione **Nueva conexión** en el panel de la derecha y haga clic en **Agregar**.  
  
5.  En el cuadro de diálogo **Conectar al motor de base de datos** , especifique una conexión para la consulta nueva y haga clic en **Conectar**. La conexión nueva se agrega a la carpeta **Conexiones** del proyecto.  
  
## <a name="see-also"></a>Vea también  
 [Explorador de soluciones](solution-explorer.md)   
 [Asociar extensiones de archivo a un Editor de código](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)   
 [Agregar elementos existentes a un proyecto](add-existing-items-to-a-project.md)   
 [Quitar o eliminar un elemento o un proyecto](remove-or-delete-an-item-or-project.md)  
  
  
