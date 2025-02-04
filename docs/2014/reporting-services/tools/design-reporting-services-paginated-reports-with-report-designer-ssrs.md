---
title: Diseñar informes con el Diseñador de informes (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], report creation
ms.assetid: 3a26dccc-6ad6-48f5-a882-f96c6c0dd405
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ffd46d75f0d3dc803f2fa3739b363bbb53b7d55b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100349"
---
# <a name="design-reports-with-report-designer-ssrs"></a>Diseñar informes con el Diseñador de informes (SSRS)
  Use el Diseñador de informes para crear informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y soluciones de informes completos. El Diseñador de informes proporciona una interfaz gráfica en la que se pueden definir orígenes de datos, conjuntos de datos y consultas, posiciones de diseño del informe para las regiones de datos y campos, y características interactivas como parámetros y conjuntos de informes que funcionan conjuntamente.  
  
## <a name="benefits-for-projects"></a>Ventajas de los proyectos  
 Use los proyectos para hacer lo siguiente:  
  
-   Organizar los informes y elementos relacionados en un contenedor.  
  
-   Soluciones de informe de prueba que incluyen informes y elementos relacionados localmente.  
  
-   Implementar conjuntamente los elementos relacionados. Usar las propiedades del proyecto y la administración de configuración para implementar varios entornos.  
  
-   Mantener un conjunto de copias maestras para los informes y elementos relacionados. Después de la implementación, los informes publicados se pueden modificar accidentalmente.  
  
 Use la información de este tema para diseñar informes y elementos relacionados para un solo proyecto de informes en una solución de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] . Para más información sobre soluciones y proyectos múltiples en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vea [Reporting Services in SQL Server Data Tools &#40;SSDT&#41;](reporting-services-in-sql-server-data-tools-ssdt.md).  
  
##  <a name="bkmk_SharedDataSources"></a> Orígenes de datos compartidos  
 Usar [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para definir e implementar orígenes de datos compartidos para una solución de informes. Los orígenes de datos compartidos se pueden implementar independientemente de otros elementos de un proyecto mediante las propiedades **OverwriteDataSources** y **TargetDataSourceFolder** . Para más información, vea [Establecer propiedades de implementación &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md).  
  
 En el Diseñador de informes, se trabaja en el panel Datos de informe y en el Explorador de soluciones para definir los orígenes de datos usados en un informe. Para más información, consulte [Report Data Pane](reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_ReportDataPane). No puede usar [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para abrir los orígenes de datos publicados en un servidor de informes o en un sitio de SharePoint, pero no incluidos en la solución de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] . Para esta característica, use [Report Builder &#40;SSRS&#41;](report-builder-authoring-environment-ssrs.md).  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] es una herramienta de cliente. Puede probar la solución de elaboración de informes localmente en el equipo, implementarla un entorno de pruebas para probar la solución de servidor y, a continuación, implementarla en un entorno de producción. Después de la implementación, compruebe que las extensiones de procesamiento de origen de datos y las credenciales del origen de datos están configuradas para el entorno del servidor de informes. Puede usar el administrador de configuración para ayudar a administrar las propiedades de distintas implementaciones. Para obtener más información, vea [Reporting Services en SQL Server Data Tools &#40;SSDT&#41;](reporting-services-in-sql-server-data-tools-ssdt.md).  
  
 Para más información, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
  
##  <a name="bkmk_SharedDatasets"></a> Conjuntos de datos compartidos  
 Use [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para definir e implementar conjuntos de datos compartidos para una solución de informes. Los conjuntos de datos compartidos pueden implementarse independientemente de otros elementos de un proyecto mediante las propiedades **OverwriteDatasets** y **TargetDatasetFolder** . Para más información, vea [Establecer propiedades de implementación &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md).  
  
 En el Diseñador de informes, se trabaja en el panel Datos de informe y en el Explorador de soluciones para definir los conjuntos de datos compartidos usados en un informe. Para más información, consulte [Report Data Pane](reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_ReportDataPane). No puede usar [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para abrir los conjuntos de datos publicados directamente desde un servidor de informes o un sitio de SharePoint. Para esta característica, use [Report Builder &#40;SSRS&#41; ](report-builder-authoring-environment-ssrs.md) en modo de conjunto de datos compartido.  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] es una herramienta de cliente. Puede usar los Diseñadores de consultas para crear y probar los resultados de la consulta localmente en la vista previa. Después de la implementación, puede administrar los conjuntos de datos compartidos independientemente de los orígenes de datos compartidos e informes de los que dependen. Para obtener más información, consulte [conjuntos de datos compartidos y conjuntos de datos incrustado de informe &#40;generador de informes y SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md), [herramientas de diseño de consulta de SQL Server Data Tools de diseñador de informes &#40;SSRS&#41; ](../report-data/query-design-tools-ssrs.md), y [administrar conjuntos de datos compartidos](../report-data/manage-shared-datasets.md).  
  
  
##  <a name="bkmk_Reports"></a> Informes  
 Los informes son archivos que se almacenan en un proyecto de informe. Los informes se pueden usar como informes independientes, subinformes o destinos para las acciones de obtención de detalles a partir de informes principales. Los informes pueden implementarse independientemente de otros elementos de un proyecto mediante **TargetReportFolder** y otras propiedades. Para más información, vea [Establecer propiedades de implementación &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md).  
  
> [!NOTE]  
>  Si se publican en un servidor de informes en modo de SharePoint, algunas características de solución de informes no se pueden probar en el proyecto de Diseñador de informes. Las referencias a los informes, subinformes e informes detallados solo deben usar las direcciones URL completas que se probaron una vez que se implemente el proyecto de informe. Para obtener más información, vea [Ejemplos de dirección URL para los elementos de informe publicados en un servidor de informes en modo de SharePoint &#40;SSRS&#41;](url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
 Puede agregar informes a un proyecto de las maneras siguientes:  
  
-   **Agregar un nuevo proyecto de informe.** De forma predeterminada, se abre un informe en blanco en el Diseñador de informes. Para más información, vea [Agregar un informe nuevo o existente a un proyecto de informe &#40;SSRS&#41;](add-a-new-or-existing-report-to-a-report-project-ssrs.md).  
  
-   **Agregar un proyecto de Asistente para informes.** Se puede crear un informe de forma gradual dirigida. El Asistente para informes simplifica la definición de datos y el diseño de un informe, con una serie de pasos que dan como resultado un informe terminado. Puede agregar estilos para personalizar el asistente para su propia organización. Para más información, vea [Agregar un informe nuevo o existente a un proyecto de informe &#40;SSRS&#41;](add-a-new-or-existing-report-to-a-report-project-ssrs.md).  
  
-   **Agregar un nuevo elemento de tipo informe.** Se abre un informe en blanco en el Diseñador de informes.  
  
-   **Agregar un elemento existente.** Se abre una definición de informe existente (.rdl) en el Diseñador de informes. El abrir un informe o un proyecto desde una versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] puede actualizar automáticamente el proyecto a la versión actual y el informe al esquema actual. Para más información, consulte [Upgrade Reports](../install-windows/upgrade-reports.md).  
  
-   **Importar un informe de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access** Se pueden importar todos los informes de Access (.mdb, .accdb) o el archivo de proyecto (.adp). El Diseñador de informes convierte a RDL (Report Definition Language) cada informe de una base de datos o archivo de proyecto y lo guarda en el proyecto de informe. No todas las funcionalidades de un informe de Access se transfieren a un archivo de definición de informe (.rdl). Para más información, vea [Importar informes desde Microsoft Access &#40;Reporting Services&#41;](../import-reports-from-microsoft-access-reporting-services.md) y [Compatibilidad con características de informes de Access &#40;SSRS&#41;](../supported-access-report-features-ssrs.md).  
  
    > [!NOTE]  
    >  Para poder usar la característica de importación, debe tener instalado Access 2002 o una versión posterior en el mismo equipo donde está instalado el Diseñador de informes. El origen de datos de los informes de Access debe estar disponible cuando se importan los informes.  
  
-   **Trabajar directamente en RDL.** Cuando se escribe un informe en el Diseñador de informes, el informe se guarda en formato XML como un archivo RDL (Report Definition Language). Este archivo se puede modificar en el Diseñador de informes, en un editor de texto o en cualquier herramienta de edición de XML.  
  
     Cuando modifique el origen de la definición de informe en el Diseñador de informes, trabajará en el esquema actual de RDL para la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde la que instaló las herramientas de desarrollo. Al compilar un proyecto, la versión de esquema puede cambiar según las propiedades de implementación. Para obtener más información, vea [Implementación y compatibilidad de versiones en las herramientas de datos de SQL Server &#40;SSRS&#41;](deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
     Si modifica el archivo RDL directamente, es posible que el informe resultante no se pueda publicar en el servidor de informes o no se pueda ejecutar. Como en cualquier archivo XML, compruebe que los caracteres específicos de XML utilizados en los elementos están correctamente codificados. Cuando se publica el informe, el servidor de informes usa el esquema para validar el código XML contenido en el archivo RDL.  
  
     Para incluir elementos que no forman parte del esquema RDL, colóquelos en el elemento personalizado. El elemento personalizado se puede leer en las extensiones de representación personalizadas, pero lo omiten las extensiones de representación proporcionadas por [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Por ejemplo, puede usar el elemento personalizado para almacenar comentarios en el informe.  
  
     Para más información, vea [Report Definition Language &#40;SSRS&#41;](../reports/report-definition-language-ssrs.md).  
  
  
##  <a name="bkmk_ReportParts"></a> Elementos de informe  
 En el Diseñador de informes, después de crear tablas, gráficos y otros elementos de informe en un proyecto, puede publicarlos como *elementos de informe* en un servidor de informes o en el sitio de SharePoint integrado con un servidor de informes para que usted y otros usuarios puedan reutilizarlos en otros informes. Para más información, vea [Elementos de informe en el Diseñador de informes &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md).  
  
 Los elementos de informe pueden implementarse independientemente de otros elementos de un proyecto mediante **TargetReportPartFolder** y otras propiedades. Para más información, vea [Establecer propiedades de implementación &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md).  
  
  
##  <a name="bkmk_Resources"></a> Recursos  
 Puede agregar al proyecto archivos relacionados con el informe, pero no procesados por el servidor de informes. Por ejemplo, puede agregar imágenes para las imágenes o archivos de forma ESRI para los datos espaciales. Para más información, consulte [Resources](../report-server/report-server-content-management-ssrs-native-mode.md#bkmk_Resources).  
  
  
##  <a name="bkmk_ReportLayout"></a> Diseño del informe  
 Para crear el diseño del informe, arrastre los elementos del informe y las regiones de datos desde el cuadro de herramientas hasta la superficie de diseño y organícelos. Arrastre los campos de conjunto de datos a los elementos en la superficie de diseño para agregar datos al informe. Para organizar los datos en grupos dentro de una región de datos Tablix, arrastre los campos de conjunto de datos hasta el panel de agrupación. Dado que las herramientas de creación de informes son básicamente una manera de crear definiciones de informe, el enfoque del diseño de informe es muy similar entre el Generador de informes y el Diseñador de informes.  
  
  
##  <a name="bkmk_Preview"></a> Vista previa  
 Use la **Vista previa** para comprobar los datos del informe y el diseño del informe. Al obtener la vista previa de un informe, el procesador de este valida el esquema de definición del informe y la sintaxis de sus expresiones, y enumera los problemas en la ventana [Output](reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_Output) .  
  
> [!NOTE]  
>  Cuando se obtiene una vista previa de un informe, los datos de ese informe se almacenan en la caché en un archivo del equipo local. Cuando se obtiene de nuevo una vista previa del mismo informe mediante la misma consulta, los mismos parámetros y las mismas credenciales, el Diseñador de informes recupera la copia en caché en lugar de volver a ejecutar la consulta. El archivo de datos se guarda como *\<nombreDeInforme>* .rdl.data en el mismo directorio que el archivo de definición de informe. El archivo no se elimina cuando se cierra el Diseñador de informes.  
  
 Puede obtener una vista previa de un informe de varias maneras:  
  
-   **Mostrar la vista previa.** Haga clic en la pestaña **Vista previa** . El informe se ejecuta en modo local, con la misma funcionalidad de procesamiento y representación de informes que proporciona el servidor de informes. El informe que se muestra es una imagen interactiva; puede seleccionar parámetros, hacer clic en vínculos, ver el mapa del documento, así como expandir y contraer las áreas ocultas del informe. También puede exportar el informe con cualquiera de los formatos de representación instalados.  
  
-   **Vista previa independiente.** Ejecute el informe local en un explorador. Con una configuración de depuración, también puede usar este modo para depurar los ensamblados personalizados que escriba. Existen tres modos de ejecutar un proyecto en modo de depuración:  
  
    -   En el menú **Depurar** , haga clic en **Iniciar**.  
  
    -   En la barra de herramientas estándar de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] , haga clic en el botón **Inicio** .  
  
    -   Presione F5.  
  
     Si utiliza una configuración de proyecto que genera el informe pero no lo implementa, el informe especificado en la propiedad `StartItem` de la configuración actual se abrirá en una ventana de vista previa distinta.  
  
    > [!NOTE]  
    >  Para usar el modo de depuración, debe establecer un elemento de inicio. En el Explorador de soluciones, haga clic en el proyecto de informe, haga clic en **propiedades**y en `StartItem`, seleccione el nombre del informe para mostrar.  
  
     Si quiere obtener la vista previa de un informe determinado que no es el elemento de inicio del proyecto, seleccione una configuración que genere el informe pero no lo implemente (por ejemplo, la configuración de depuración local), haga clic con el botón derecho en el informe y, luego, haga clic en **Ejecutar**. Debe elegir una configuración que no implemente el informe; de lo contrario, éste se publicará en el servidor de informes en lugar de mostrarse localmente en una ventana de vista previa.  
  
-   **Vista previa de impresión.**  
  
     La primera vez que se ve un informe en el modo de vista previa o en la ventana de vista previa, la vista del informe se asemeja a un informe generado mediante la extensión de representación en HTML. La vista previa no es HTML, pero el diseño y la paginación del informe son similares a la salida con formato HTML.  
  
     Para cambiar la vista de manera que represente un informe impreso, cambie al modo de vista previa de impresión. Haga clic en el botón **Vista previa de impresión** de la barra de herramientas de la vista previa. El informe se mostrará como si estuviera en una página física. Esta vista se asemeja a la salida que se obtiene mediante las extensiones de representación en imágenes y en PDF. La vista previa de impresión no es un archivo de imagen ni un archivo PDF, pero el diseño y la paginación del informe son similares a la salida con estos formatos. Puede elegir el tamaño de la imagen del informe, por ejemplo, establezca el ancho de la página.  
  
     La vista previa de impresión le ayuda a identificar los problemas de representación que podría encontrar si imprimiera el informe. Entre los problemas de representación comunes se incluyen:  
  
    -   Páginas en blanco adicionales porque el informe es demasiado ancho para el tamaño de papel especificado para el informe.  
  
    -   Páginas en blanco adicionales porque el informe contiene una matriz que se expande dinámicamente y supera el ancho del papel especificado.  
  
    -   Los saltos de página entre grupos no funcionan de la manera deseada.  
  
    -   Los encabezados y pies de página no se muestran como se esperaba.  
  
    -   El diseño del informe necesita modificaciones para poder leerlo mejor en un formato impreso.  
  
  
##  <a name="bkmk_SaveandDeploy"></a> Guardar e implementar  
 En el Diseñador de informes, puede guardar informes y otros archivos del proyecto localmente o implementarlos en un servidor de informes o en un sitio de SharePoint. Los orígenes de datos compartidos, conjuntos de datos compartidos, informes, recursos de informes y elementos de informe se pueden implementar de forma independiente o conjuntamente en función de las propiedades de implementación del proyecto que configure. Para más información, consulte [Configuration and Deployment Properties](deployment-and-version-support-in-sql-server-data-tools-ssrs.md#bkmk_ConfigurationandDeploymentProperties).  
  
 En el Diseñador de informes, es importante entender que un informe se diseña mediante el esquema de definición de informe que admite la versión actual de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Cuando se establecen las propiedades de implementación del proyecto para un servidor de informes o un sitio de SharePoint concretos y, a continuación, se guarda el informe, el Diseñador de informes guarda la definición de informe en el directorio de compilación del esquema que coincide con la versión del servidor de informes de destino. Para crear informes que se pueden publicar en un servidor de informes de nivel inferior, el Diseñador de informes quita los elementos de informe que no existen en el esquema de destino. Esto ocurre automáticamente y sin pedir confirmación. Cuando esto sucede, la definición de informe original se mantiene en la carpeta del proyecto. La definición de informe modificada que se implementa está en la carpeta de compilación.  
  
> [!NOTE]  
>  Para depurar expresiones y errores de implementación, debe visualizar la definición de informe en la carpeta de compilación. No use **Ver código fuente**. **Ver código fuente** muestra el origen de la definición de informe almacenado en la carpeta del proyecto.  
  
 Para obtener más información, vea [Implementación y compatibilidad de versiones en las herramientas de datos de SQL Server &#40;SSRS&#41;](deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
### <a name="save-a-report-locally"></a>Guardar un informe localmente  
 Cuando trabaje en informes u otros elementos de proyecto en el Diseñador de informes, los archivos se guardarán en el equipo local o en un recurso compartido de otro equipo al que tenga acceso.  
  
 Si usa el software de control de código fuente, podría comprobar los informes en el servidor de control de código fuente al guardar el informe. Para más información, consulte [Source Control](reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_SourceControl).  
  
### <a name="deploy-or-publish"></a>Implementar o publicar  
 En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], puede implementar informes u otros elementos de proyecto en varias versiones de los servidores de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Use las configuraciones de proyecto para controlar la actualización de las definiciones de informe en las versiones de esquema compatibles con los servidores de informes de destino. Entre las propiedades que se controlan mediante configuraciones de proyecto se incluyen el servidor de informes de destino, la carpeta donde el proceso de compilación almacena temporalmente las definiciones de informe para la vista previa e implementación, y los niveles de error. Para más información, vea [Propiedades de configuración e implementación](deployment-and-version-support-in-sql-server-data-tools-ssrs.md#bkmk_ConfigurationandDeploymentProperties) y [Establecer propiedades de implementación &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md).  
  
### <a name="export-a-report-to-a-different-file-format"></a>Exportar un informe a un formato de archivo diferente  
 Los informes se pueden exportar a una gran variedad de formatos y estos formatos determinan el funcionamiento de algunas de las características interactivas y de diseño del informe. Para obtener más información sobre las consideraciones de diseño de varios formatos de salida, vea [exportar informes &#40;generador de informes y SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md).  
  
  
##  <a name="bkmk_ReportValidationandErrorLevels"></a> Validación de informes y niveles de error  
 Los informes se validan antes de la vista previa y durante la implementación. Se pueden producir varios problemas al compilar los informes. Por ejemplo, los informes podrían contener cadenas como expresiones o consultas que sean incompatibles con la versión de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que la configuración de proyecto especifique.  
  
 Use la propiedad ErrorLevel para administrar las advertencias y los errores de compilación. La propiedad ErrorLevel puede contener un valor comprendido entre 0 y 4, ambos incluidos. El valor determina qué problemas de generación se notifican como errores y cuáles como advertencias. El valor predeterminado es 2. Las advertencias y los errores se escriben en la ventana [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)][Salida](reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_Output).  
  
 Los problemas con un nivel de gravedad menor o igual que el valor de ErrorLevel se notifican como errores; de lo contrario, se notifican como advertencias.  
  
 En la tabla siguiente se enumeran los niveles de error.  
  
|Nivel del error|Descripción|  
|-----------------|-----------------|  
|0|Problemas de generación más graves e inevitables que impiden la vista previa y la implementación de los informes.|  
|1|Problemas de la generación graves que cambian el diseño del informe drásticamente.|  
|2|Problemas de la generación menos graves que cambian el diseño del informe significativamente.|  
|3|Problemas de la generación poco importantes que cambian el diseño del informe de una manera insignificante que podría no ser apreciable.|  
|4|Solo se utiliza para publicar advertencias.|  
  
 Al intentar ofrecer una vista previa de un informe que contiene elementos de informe nuevos o implementarlo en [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], por ejemplo mapas y barras de datos, esos elementos de informe se pueden quitar del informe. De forma predeterminada, la propiedad ErrorLevel de la configuración está establecida en 2, lo que haría que la compilación del informe diera un error al quitarse el mapa. Pero si cambia el valor de la propiedad ErrorLevel a 0 o 1, se quita el mapa, se emite una advertencia y el proceso de compilación continúa.  
  
  
## <a name="see-also"></a>Vea también  
 [Reporting Services en SQL Server Data Tools &#40;SSDT&#41;](reporting-services-in-sql-server-data-tools-ssdt.md)   
 [Herramientas de diseño de herramientas de datos del servidor de informes SQL Diseñador de consultas &#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)   
 [Implementación y compatibilidad de versiones en las herramientas de datos de SQL Server &#40;SSRS&#41;](deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  
  
  
