---
title: Transformación Copiar columna | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.copycolumntrans.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7ebdcc68c4fe8c4782251e2f4e5896e4557e23e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770331"
---
# <a name="copy-column-transformation"></a>Copiar columna, transformación
  La transformación Copiar columna crea columnas nuevas copiando columnas de entrada y agregando las columnas nuevas a la salida de transformación. En una fase posterior del flujo de datos se pueden aplicar distintas transformaciones a las copias de columnas. Por ejemplo, puede usar la transformación Copiar columna para crear una copia de una columna y después convertir los datos copiados a mayúsculas mediante la transformación Mapa de caracteres, o aplicar agregaciones a la nueva columna mediante la transformación Agregado.  
  
## <a name="configuration-of-the-copy-column-transformation"></a>Configuración de la transformación Copiar columna  
 Puede configurar la transformación Copiar columna especificando las columnas de entrada que desea copiar. Puede crear varias copias de una columna o crear copias de varias columnas en una operación.  
  
 Esta transformación tiene una entrada y una salida. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Copiar columna** , vea [Copy Column Transformation Editor](../../copy-column-transformation-editor.md).  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vea también  
 [Flujo de datos](../data-flow.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
  
