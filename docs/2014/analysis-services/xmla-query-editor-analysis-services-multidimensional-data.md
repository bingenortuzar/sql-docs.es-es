---
title: Editor de consultas XMLA (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.editor.xmla.f1
helpviewer_keywords:
- XMLA Query Editor
- Query Editor [XMLA]
ms.assetid: 14623019-7839-4038-9d12-2f8953d2ec04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1939ea9e1de7b0b7858ad09ad26bc3b4fbf008c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065308"
---
# <a name="xmla-query-editor-analysis-services---multidimensional-data"></a>Editor de consultas XMLA (Analysis Services - Datos multidimensionales)
  Utilice el Editor de consultas XMLA para diseñar y ejecutar instrucciones y scripts escritos en lenguaje de expresiones multidimensionales (XMLA).  
  
## <a name="features"></a>Características  
  
-   Escriba los scripts en el panel del Editor de consultas XMLA.  
  
-   Para ejecutar scripts, presione **F5**o haga clic en **Ejecutar** en la barra de herramientas, o haga clic en **Ejecutar** en el menú **Consulta**. Si se selecciona un fragmento del código, solamente se ejecutará dicho fragmento. Si no se ha seleccionado ningún código, se ejecuta todo el contenido del Editor de consultas XMLA.  
  
-   Vea los metadatos para cubos y otros objetos contenidos en una base de datos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el panel de metadatos.  
  
-   Para obtener ayuda sobre la sintaxis del lenguaje XMLA, seleccione una palabra clave en el Editor de consultas XMLA y, a continuación, haga clic en **F1**.  
  
-   Para obtener ayuda dinámica sobre la sintaxis del lenguaje XMLA, en el menú **Ayuda** , haga clic en **Ayuda dinámica** para abrir el componente Ayuda dinámica. En Ayuda dinámica, los temas de ayuda se muestran en la ventana **Ayuda dinámica** al escribir las palabras clave en el Editor de consultas.  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>Barra de herramientas Editores de SQL Server Analysis Services  
 Cuando se abre el Editor de consultas XMLA, aparece la barra de herramientas **Editores de SQL Server Analysis Services** con los siguientes botones.  
  
|Término|Definición|  
|----------|----------------|  
|**Conectar**|Abre el cuadro de diálogo **Conectar a servidor** para establecer una conexión a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Desconectar**|Desconecta el Editor de consultas XMLA de una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Cambiar conexión**|Abre el cuadro de diálogo **Conectar a servidor** para establecer una conexión a una instancia distinta de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Consulta con conexión actual**|Abre una nueva ventana del Editor de consultas XMLA utilizando la información de conexión de la ventana actual del Editor de consultas XMLA.|  
|**Bases de datos disponibles**|Cambia la conexión a una base de datos distinta de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en la misma instancia.|  
|**Ejecutar**|Ejecuta el código seleccionado o, si no se ha seleccionado ningún código, esta opción ejecuta todo el código del Editor de consultas XMLA.|  
|**Analizar**|Comprueba la sintaxis del código seleccionado. Si no se ha seleccionado ningún código, esta opción comprueba la sintaxis de toda la ventana del Editor de consultas XMLA.|  
|**Cancelar ejecución de la consulta**|Envía una solicitud de cancelación al servidor. Algunas consultas no pueden cancelarse inmediatamente, sino que deben esperar a una condición de cancelación adecuada. Al cancelar las consultas, podrían producirse retrasos mientras se revierten las transacciones.|  
  
## <a name="xmla-query-editor-window"></a>Editor de consultas XMLA (ventana)  
 Las siguientes opciones están disponibles en el Editor de consultas XMLA:  
  
|Término|Definición|  
|----------|----------------|  
|**Ventana editor de consultas**|Escriba las instrucciones y scripts XMLA que desee ejecutar con el Editor de consultas XMLA.<br /><br /> El menú contextual del editor de consultas proporciona las siguientes opciones:<br /><br /> **Cortar**: Copia la selección actual en el portapapeles y quita la selección de la ventana del editor de consultas.<br />**Copiar**: Copia la selección actual en el portapapeles.<br />**Pegar**: Pega el contenido del portapapeles en la selección actual.<br />**Conectar**: Abre el cuadro de diálogo **Conectar a servidor** para establecer una conexión a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br />**Desconectar**: Desconecta el editor de consultas actual de una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br />**Desconectar todas las consultas**: Desconecta todos los editores de consultas abiertos.<br />**Cambiar conexión**: Abre el cuadro de diálogo **Conectar a servidor** para establecer una conexión a una instancia distinta de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br />**Abrir servidor en el Explorador de objetos**: Abre el cuadro de diálogo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a la que está conectado el editor de consultas actual en el **Explorador de objetos**.<br />**Ejecutar**: Ejecuta el código seleccionado o, si no se ha seleccionado ningún código, ejecuta todo el código del editor de consultas actual.<br />**Ventana Propiedades**: Muestra la ventana **Propiedades** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para la ventana de consultas actual.<br />**Opciones de consulta**: Muestra el cuadro de diálogo **Opciones de consulta** .|  
|**Ventana de resultados**|Muestra los resultados de una instrucción o script XMLA en formato de texto.|  
|**Ventana de mensajes**|Muestra información sobre cómo se ejecutan una instrucción o script XMLA. Por ejemplo, esta ventana muestra todos los errores encontrados durante la ejecución o el número de celdas recuperadas tras la ejecución.|  
  
## <a name="see-also"></a>Vea también  
 [Editor de consultas MDX &#40;Analysis Services - datos multidimensionales&#41;](mdx-query-editor-analysis-services-multidimensional-data.md)   
 [Editor de consultas DMX &#40;Analysis Services - minería de datos&#41;](dmx-query-editor-analysis-services-data-mining.md)   
 [Editores de consultas y texto &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [Métodos abreviados de teclado de SQL Server Management Studio](../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
