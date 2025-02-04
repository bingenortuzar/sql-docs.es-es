---
title: Establecer la configuración regional de un informe o un cuadro de texto (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- locales [Reporting Services]
ms.assetid: df115b01-184b-47f0-b5ec-0ad965ff9bee
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d65c02df74cb89fca3d861f01c01da87ff589e3a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104986"
---
# <a name="set-the-locale-for-a-report-or-text-box-reporting-services"></a>Establecer la configuración regional de un informe o un cuadro de texto (Reporting Services)
  La propiedad **Language** de un informe o un cuadro de texto contiene la configuración regional, que determina los formatos predeterminados para mostrar los datos de informe que difieren según el idioma y la región, como por ejemplo, la fecha, la moneda o los valores numéricos. La propiedad **Language** de un cuadro de texto invalida la propiedad **Language** del informe. Si no se especifica ningún valor para **Language**, Reporting Services usa la configuración regional del sistema operativo del servidor de informes para los informes publicados o la del equipo en que se crea el informe para la vista previa del informe.  
  
 Para los informes HTML, puede invalidar el valor de **Language** predeterminado y usar el idioma especificado por el encabezado HTTP del cliente de explorador usando el campo integrado User!Language en una expresión para la propiedad **Language** de un informe o un cuadro de texto.  
  
 También puede especificar la propiedad **Language** para un informe en una dirección URL. Para más información, vea [Establecer el idioma para los parámetros de informe en una dirección URL](../set-the-language-for-report-parameters-in-a-url.md).  
  
### <a name="to-set-the-locale-for-a-report"></a>Para establecer la configuración regional de un informe  
  
1.  En la vista Diseño, haga clic fuera de la superficie de diseño del informe para seleccionar el informe.  
  
2.  En el panel Propiedades, en la propiedad **Language** , escriba o seleccione el idioma que desea usar para el informe.  
  
### <a name="to-set-the-locale-for-a-text-box"></a>Para establecer la configuración regional de un cuadro de texto  
  
1.  En la vista Diseño, seleccione el cuadro de texto al que desea aplicar la configuración regional.  
  
2.  En el panel Propiedades, haga lo siguiente:  
  
    -   En la propiedad **Calendar** , escriba o seleccione el calendario que desea usar para las fechas.  
  
    -   En la propiedad **Direction** , escriba o seleccione la dirección en que se escribe el texto.  
  
    -   En la propiedad **Language** , escriba o seleccione el idioma que desea usar para el cuadro de texto. Este valor invalida la propiedad **Language** para el informe.  
  
    -   En la propiedad **NumeralLanguage** , escriba o seleccione el formato que desea utilizar para los números del cuadro de texto.  
  
    -   En la propiedad **NumeralVariant** , escriba o seleccione la variante de formato que desea usar para los números del cuadro de texto.  
  
    -   En la propiedad **UnicodeBiDi** , seleccione el nivel de incrustación bidireccional que se va a usar en el cuadro de texto.  
  
## <a name="see-also"></a>Vea también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  
