---
title: Editor de destino de SQL (página avanzadas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdestadapter.advanced.f1
helpviewer_keywords:
- SQL Server Destination Editor
ms.assetid: 9b46bcf8-ddaf-4d7d-90a6-80bc19517e9b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 087f32510b65d7ea505bc4bf816a5ca9edcfe82d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055456"
---
# <a name="sql-destination-editor-advanced-page"></a>Editor de destino de SQL (página Avanzadas)
  Utilice la página **Avanzadas** del cuadro de diálogo **Editor de destino de SQL** para especificar opciones avanzadas de inserción masiva.  
  
 Para obtener más información acerca del destino de SQL Server, vea [SQL Server Destination](data-flow/sql-server-destination.md).  
  
## <a name="options"></a>Opciones  
 **Mantener valores de identidad**  
 Especifique si la tarea debe insertar valores en columnas de identidad. El valor predeterminado de esta propiedad es `False`.  
  
 **Mantener valores NULL**  
 Especifique si la tarea debe mantener valores NULL. El valor predeterminado de esta propiedad es `False`.  
  
 **Bloqueo de tabla**  
 Especifique si la tabla está bloqueada cuando se cargan los datos. El valor predeterminado de esta propiedad es `True`.  
  
 **Restricciones CHECK**  
 Especifique si la tarea debe comprobar restricciones. El valor predeterminado de esta propiedad es `True`.  
  
 **Activar desencadenadores**  
 Especifique si la inserción masiva debe activar desencadenadores en tablas. El valor predeterminado de esta propiedad es `False`.  
  
 **Primera fila**  
 Especifique la primera fila donde se va a insertar. El valor predeterminado de esta propiedad es **-1**, que indica que no se ha asignado ningún valor.  
  
> [!NOTE]  
>  Borre el cuadro de texto del **Editor de destino de SQL** para indicar que no desea asignar un valor a esta propiedad. Use -1 en la ventana **Propiedades** , el **Editor avanzado**y el modelo de objetos.  
  
 **Última fila**  
 Especifique la última fila donde se va a insertar. El valor predeterminado de esta propiedad es **-1**, que indica que no se ha asignado ningún valor.  
  
> [!NOTE]  
>  Borre el cuadro de texto del **Editor de destino de SQL** para indicar que no desea asignar un valor a esta propiedad. Use -1 en la ventana **Propiedades** , el **Editor avanzado**y el modelo de objetos.  
  
 **Número máximo de errores**  
 Especifique el número de errores que se pueden producir antes de que se detenga la inserción masiva. El valor predeterminado de esta propiedad es **-1**, que indica que no se ha asignado ningún valor.  
  
> [!NOTE]  
>  Borre el cuadro de texto del **Editor de destino de SQL** para indicar que no desea asignar un valor a esta propiedad. Use -1 en la ventana **Propiedades** , el **Editor avanzado**y el modelo de objetos.  
  
 **Timeout**  
 Especifique el número de segundos que se debe esperar antes de que la inserción masiva se detenga debido a un tiempo de espera.  
  
 **Columnas de orden**  
 Escriba los nombres de las columnas de orden. Las columnas se pueden ordenar en sentido ascendente o descendente. Si utiliza varias columnas de orden, delimite la lista con comas.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de SQL &#40;página Administrador de conexiones&#41;](../../2014/integration-services/sql-destination-editor-connection-manager-page.md)   
 [Editor de destino de SQL &#40;página Asignaciones&#41;](../../2014/integration-services/sql-destination-editor-mappings-page.md)   
 [Realizar una carga masiva de datos mediante el destino de SQL Server](data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  
