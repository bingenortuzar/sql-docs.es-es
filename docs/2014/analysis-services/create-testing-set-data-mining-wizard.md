---
title: Crear conjunto de pruebas (Asistente para minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.holdout.f1
ms.assetid: d0a44b59-ffbd-45fc-baa8-6b8046b1a2f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f0e4d1a384995c0c49c346102f8fddbcdf47f68
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086790"
---
# <a name="create-testing-set-data-mining-wizard"></a>Crear conjunto de pruebas (Asistente para minería de datos)
  Utilice la página **Crear conjunto de pruebas** para especificar qué cantidad de datos se va a utilizar para el entrenamiento y cuánta se va a reservar para utilizarla en un conjunto de pruebas. Al separar los datos en un conjunto de aprendizaje y de pruebas cuando se crea una estructura de minería de datos, resulta más fácil evaluar la exactitud de los modelos de minería que se crean después.  
  
 Puede especificar la cantidad de datos de prueba como un porcentaje o puede especificar un número para limitar el número de casos que se utilizan para pruebas. Si especifica un porcentaje y un número máximo de casos que puedan utilizarse en pruebas, se utilizan ambas configuraciones y el conjunto de datos de pruebas contiene el número menor de casos. De forma predeterminada, el 30 por ciento de los datos se utiliza para pruebas, el 70 por ciento para aprendizaje y no hay ningún número máximo de casos de prueba.  
  
 De manera predeterminada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] genera un valor de inicialización numérico que se usa para iniciar las particiones. Este valor de inicialización está basado en el nombre de la estructura de minería de datos. Si desea asegurarse de que la partición se queda igual incluso si se cambia el nombre de la estructura de minería de datos, puede especificar un valor de inicialización si establece la propiedad HoldoutSeed de la estructura de minería de datos. Si cambia el valor de inicialización de la exclusión, debe volver a procesar la estructura.  
  
 Si desea cambiar la cantidad de datos de entrenamiento o pruebas más adelante, puede modificar el `HoldoutMaxCases` y `HoldoutMaxPercent` propiedades en la estructura de minería de datos mediante el uso de la **propiedades** ventana. Sin embargo, después de realizar la modificación debe volver a procesar la estructura de minería de datos y todos los modelos de minería asociados. También se aplican las siguientes limitaciones:  
  
-   El particionamiento de una estructura de minería de datos solamente se admite cuando la estructura está almacenada en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no permiten almacenar en memoria caché información de la partición para las estructuras de minería de datos.  
  
-   No se puede dividir una estructura de minería de datos si ésta contiene una columna de clave temporal, que se requiere para los modelos de minería de datos de serie temporal.  
  
-   No se pueden dividir los datos si está intentando predecir un valor que está almacenado en una tabla anidada.  
  
 **Para obtener más información:** [Pruebas y validación &#40;minería de datos&#41;](data-mining/testing-and-validation-data-mining.md), [crear una estructura de minería de datos relacional](data-mining/create-a-relational-mining-structure.md), [Tutorial de minería de datos básicos](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
## <a name="options"></a>Opciones  
 **Porcentaje de datos de prueba**  
 Haga clic en las flechas arriba y abajo para aumentar o disminuir el porcentaje de datos que se van a utilizar como un conjunto de aprendizaje o escriba un valor entre 0 y 100 en el cuadro de texto.  
  
 **Número máximo de casos en el conjunto de datos de prueba**  
 Escriba un número para limitar el número de casos que se pueden utilizar para realizar las pruebas.  
  
 Si especifica un número mayor que el número de casos reales en los datos, se utilizarán todos los casos.  
  
 El valor predeterminado es NULL. Esto significa que no hay ningún límite.  
  
## <a name="see-also"></a>Vea también  
 [Asistente para la Ayuda de F1 de minería de datos &#40;Analysis Services - minería de datos&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Sugerir columnas relacionadas &#40;Asistente para minería de datos&#41;](suggest-related-columns-data-mining-wizard.md)   
 [Especificar tipos de tablas &#40;Asistente para minería de datos&#41;](specify-table-types-data-mining-wizard.md)   
 [Especificar el contenido y el tipo de datos de la columna &#40;Asistente para minería de datos&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
