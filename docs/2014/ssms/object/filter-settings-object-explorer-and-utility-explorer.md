---
title: Configuración de filtro (Explorador de objetos y Explorador de Utilidad) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.filtersettings.f1
- sql12.swb.common.filtersettings.f1
ms.assetid: 4aab04bc-e1ab-4d4b-ab74-b287fc805bc2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 78573a21a5aa6a719a9bb55d0ee17bf9837258f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63277082"
---
# <a name="filter-settings-object-explorer-and-utility-explorer"></a>Configuración de filtro (Explorador de objetos y Explorador de la utilidad)
  Utilice este cuadro de diálogo para especificar un filtro. Un filtro permite configurar el Explorador de objetos y el Explorador de la utilidad para mostrar únicamente los elementos que cumplen criterios específicos. Por ejemplo, puede utilizar un filtro para mostrar solo los trabajos con nombres que contienen la palabra "Mantenimiento". El encabezado del cuadro de diálogo **Configuración del filtro** contiene el nombre del servidor y puede contener el nombre de la base de datos.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Propiedad**  
 Muestra la propiedad que se va filtrar.  
  
 **Operador**  
 Seleccione la forma en que el filtro va a aplicar el valor a la propiedad. Existen las siguientes opciones:  
  
-   **Es igual a**  
  
     El filtro muestra los elementos en los que la propiedad y el valor coinciden plenamente.  
  
-   **Contiene**  
  
     El filtro muestra los elementos en los que la propiedad contiene el valor. La propiedad puede contener otro texto.  
  
-   **No contiene**  
  
     El filtro muestra los elementos en los que la propiedad no contiene el valor.  
  
-   **Menor que**  
  
     Disponible para fechas; este filtro muestra los elementos cuya fecha es anterior al valor proporcionado.  
  
-   **Menor que o igual a**  
  
     Disponible para fechas; este filtro muestra los elementos cuya fecha es igual o anterior al valor proporcionado.  
  
-   **Mayor que**  
  
     Disponible para fechas; este filtro muestra los elementos cuya fecha es posterior al valor proporcionado.  
  
-   **Mayor que o igual a**  
  
     Disponible para fechas; este filtro muestra los elementos cuya fecha es igual o posterior al valor proporcionado.  
  
-   **Entre**  
  
     Disponible para fechas; este filtro muestra los elementos cuya fecha se encuentra entre dos fechas proporcionadas. Seleccione **Entre** y presione la tecla TAB para agregar otra fila a fin de escribir la segunda fecha.  
  
-   **No entre**  
  
     Disponible para fechas; este filtro muestra los elementos cuya fecha es anterior o posterior a dos fechas proporcionadas. Seleccione **No entre** y salga de la columna **Operador** para agregar otra fila a fin de escribir la segunda fecha.  
  
 **Valor**  
 Escriba el valor que va a compararse con la propiedad. Para seleccionar una fecha, haga clic en la flecha abajo para que aparezca un calendario donde seleccionarla.  
  
 **Borrar filtro**  
 Elimina toda la configuración actual del filtro.  
  
## <a name="see-also"></a>Vea también  
 [Usar SQL Server Management Studio](../sql-server-management-studio-ssms.md)   
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
