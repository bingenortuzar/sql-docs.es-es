---
title: Publicar y volver a publicar elementos de informe (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 92dce484-f39b-403c-9caf-d8772bc3aca3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f48415c35b57b889b764abfe44f5bf937ee3f650
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65576623"
---
# <a name="publish-and-republish-report-parts-report-builder-and-ssrs"></a>Publicar y volver a publicar elementos de informe (Generador de informes y SSRS)
  Se trata de elementos de informe paginado que se han publicado por separado en un servidor de informes y se pueden volver a usar en otros informes paginados. Puede publicar un elemento de informe con la configuración predeterminada en una ubicación predeterminada, o editar los metadatos del elemento de informe , por ejemplo el nombre y la descripción, y guardarlo en otra ubicación de un servidor de informes. También puede guardarlo en un sitio de SharePoint que esté integrado con un servidor de informes si tiene los permisos necesarios.  
  
 Puede publicar solo el elemento de informe, con el conjunto de datos del que depende incrustado en él, o publicar el conjunto de datos por separado. Si publica el conjunto de datos por separado, se convierte en un conjunto de datos compartido y el elemento de informe se vincula con él. Para obtener más información, vea [Elementos de informe y conjuntos de datos en el Generador de informes](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md).  
  
 Puede volver a publicar un elemento de informe existente. Si tiene los permisos necesarios, puede volver a guardar la instancia original del elemento de informe en el servidor, aunque no lo haya creado. También puede publicarlo como un nuevo elemento de informe y guardarlo en la misma ubicación o en otra.  
  
## <a name="to-publish-a-report-part"></a>Para publicar un elemento de informe  
  
1.  En el menú del Generador de informes, haga clic en **Publicar elementos de informe**.  
  
     Si no está conectado a un servidor de informes, se le pedirá que lo haga. Si no puede conectarse a un servidor de informes, no puede publicar elementos de informe.  
  
2.  Para guardar elementos de informe con la configuración predeterminada en la ubicación predeterminada, haga clic en **Publicar todos los elementos de informe con configuración predeterminada**.  
  
     Si no desea hacerlo, haga clic en **Revisar y modificar los elementos de informe antes de publicarlos**.  
  
3.  Edite el nombre y la descripción del elemento de informe. Haga doble clic en el nombre para editarlo y haga clic en el campo **Descripción** para agregar una descripción.  
  
    > [!NOTE]  
    >  Es aconsejable dar un nombre y una descripción al elemento de informe, porque ayuda a los usuarios a identificarlo cuando lo buscan. La longitud máxima del nombre de un elemento de informe es de 260 caracteres para la ruta de acceso completa, incluidos los nombres de las carpetas del servidor, seguidos por el nombre del elemento de informe.  
  
4.  Para guardar un elemento de informe en una carpeta que no sea la predeterminada, haga clic en el botón **Examinar** .  
  
5.  Cuando haya configurado las opciones para todos los elementos de informe del informe, haga clic en **Publicar**.  
  
     Después de publicar los elementos de informe, en el cuadro de diálogo se muestra cuáles se publicaron correctamente y cuáles no. En el cuadro de diálogo **Publicar elementos de informe** se muestran los datos de los elementos de informe que no se publicaron.  
  
6.  Haga clic en **Cerrar**.  
  
## <a name="to-republish-a-report-part"></a>Volver a publicar un elemento de informe  
  
1.  Siga el procedimiento anterior de publicación de un elemento de informe.  
  
2.  En el cuadro de diálogo **Publicar elementos de informe** , si hace clic en **Publicar como una nueva copia del elemento de informe**, el Generador de informes no reemplazará el elemento de informe existente en el servidor, si no que creará otro elemento de informe.  
  
> [!NOTE]  
>  Si lo publica como nuevo elemento de informe, tendrá un nuevo identificador único. Ya no recibirá actualizaciones si cambia el elemento de informe original.  
  
## <a name="see-also"></a>Consulte también  
 [Elementos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [Elementos de informe y conjuntos de datos en el Generador de informes](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Solucionar problemas de elementos de informe (Generador de informes y SSRS)](https://msdn.microsoft.com/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Buscar o desactivar actualizaciones (Generador de informes y SSRS)](https://msdn.microsoft.com/9c69792d-d7c4-453b-ae2f-6d2d071d8606)   
 [Buscar elementos de informe y establecer una carpeta predeterminada &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
  
