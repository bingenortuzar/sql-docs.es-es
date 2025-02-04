---
title: Página Propiedades generales, informes partes (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 93ddce72-31f1-42f7-abd5-8191acbb00c5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aa3f8b6ec0cd81f1a29ea3262bd3ec52dd8158ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109085"
---
# <a name="general-properties-page-report-parts-report-manager"></a>Página de propiedades generales, Elementos de informe (Administrador de informes)
  Use la página de propiedades para ver y administrar las propiedades generales de un elemento de informe.  
  
 En el Administrador de informes, no puede ver ni cambiar la apariencia y la funcionalidad del elemento de informe. Para cambiar el diseño, debe utilizar una herramienta de creación para abrir y modificar el diseño, y publicarlo de nuevo en el servidor.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-properties-page-for-a-report-part"></a>Para abrir la página de propiedades de un elemento de informe  
  
1.  Abra el Administrador de informes y busque el elemento de informe cuyas propiedades desea configurar.  
  
2.  Desplace el puntero sobre el elemento de informe y haga clic en la flecha de lista desplegable.  
  
3.  En la lista desplegable, haga clic en **Administrar**. Se abre la página de propiedades General.  
  
## <a name="options"></a>Opciones  
 **Fecha de modificación**  
 La fecha y la hora en que las propiedades del elemento de informe se modificaron por última vez en el servidor o en que una nueva versión del elemento de informe publicado se publicó en el servidor. Solo lectura.  
  
 **Modificado por**  
 Nombre del usuario que modificó por última vez el elemento de informe. Solo lectura.  
  
 **Fecha de creación**  
 La fecha y hora en que el elemento de informe se publicó originalmente en el servidor. Solo lectura.  
  
 **Creado por**  
 Nombre del usuario que creó originalmente el elemento de informe publicado. Solo lectura.  
  
 **Tamaño**  
 Tamaño del archivo del elemento de informe. Solo lectura.  
  
 **Name**  
 Escriba un nombre para identificar el elemento de informe.  
  
 **Descripción**  
 Proporcione información acerca del elemento de informe. La descripción aparece en la página Contenido del Administrador de informes. Se puede buscar en el texto de descripción cuando un usuario busca los elementos de informe con una herramienta de creación de informes.  
  
 **Ocultar en la vista de lista**  
 Seleccione esta opción para ocultar el elemento de informe a los usuarios que usen el modo de vista de lista en el Administrador de informes. El modo de vista de lista es el formato de vista predeterminado al examinar la jerarquía de carpetas del servidor de informes. Aunque se puede ocultar un elemento en la vista de lista, no se puede ocultar en la vista Detalles. Si desea restringir el acceso a un elemento, deberá crear una asignación de roles.  
  
 **Tipo**  
 Tipo del elemento de informe. Solo lectura.  
  
 **Aplicar**  
 Guarde los cambios.  
  
 **Eliminar**  
 Quite el elemento de informe de la base de datos del servidor de informes. Al eliminar un elemento de informe del servidor, no se evitará la representación de informes existentes a los que se agregó.  
  
 **Mover**  
 Haga clic para abrir la página Mover elementos para mover un elemento de informe dentro de la jerarquía de carpetas del servidor de informes. Para obtener más información, consulte [página Mover elementos &#40;el Administrador de informes&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Descargar**  
 Extraiga una copia de la definición del elemento de informe que se va a guardar como archivo .rsc. El archivo .rsc se puede cargar en una carpeta del servidor de informes o utilizarse para reemplazar un elemento de informe existente en una carpeta del servidor de informes.  
  
 **Reemplazar**  
 Reemplace la definición del elemento de informe con otra diferente de un archivo .rsc.  
  
## <a name="see-also"></a>Vea también  
 [Administrar elementos de informe](report-design/managing-report-parts.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Contenido &#40;página del Administrador de informes&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Elementos de informe &#40;Generador de informes y SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [El Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)   
 [Elementos de informe y conjuntos de datos en el Generador de informes](report-data/report-parts-and-datasets-in-report-builder.md)  
  
  
