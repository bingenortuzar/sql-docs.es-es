---
title: Agregar un parámetro de varios valores a un informe | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 12ad0e77-4c28-4bbb-ab11-473ae89ec9f1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 72a827e8f15627e986008e57ecb9a180b715a8a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106812"
---
# <a name="add-a-multi-value-parameter-to-a-report"></a>Agregar un parámetro de varios valores a un informe
  Puede agregar un parámetro a un informe que permita al usuario seleccionar más de un valor para el parámetro.  
  
 Puede pasar varios valores de parámetro al informe dentro de la dirección URL del informe. Para ver un ejemplo de dirección URL que incluye un parámetro de varios valores, vea [Pasar un parámetro de informe en una dirección URL](../pass-a-report-parameter-within-a-url.md).  
  
 Para obtener información sobre cómo pasar varios valores de parámetro a un procedimiento almacenado, vea [Trabajar con parámetros de selección múltiple en informes de SSRS](https://go.microsoft.com/fwlink/?LinkId=321529) en mssqltips.com.  
  
### <a name="to-add-a-multi-value-parameter"></a>Para agregar un parámetro de varios valores  
  
1.  En el Generador de informes, abra el informe al que desea agregar el parámetro de varios valores.  
  
2.  Haga clic con el botón derecho en el conjunto de datos del informe y, después, haga clic en **Propiedades del conjunto de datos**.  
  
3.  Agregue una variable a la consulta del conjunto de datos; para ello, edite el texto de la consulta en el cuadro **Consulta** o agregue un filtro mediante el diseñador de consultas. Para más información, vea [Crear una consulta en el Diseñador de consultas relacionales &#40;Generador de informes y SSRS&#41;](../report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md).  
  
    > [!IMPORTANT]  
    >  El texto de consulta no debe incluir la instrucción DECLARE para la variable de consulta.  
  
    > [!IMPORTANT]  
    >  El texto de la variable de consulta debe incluir el operador `IN`, como se muestra en el ejemplo siguiente.  
  
    ```  
    WHERE  
      Production.ProductInventory.ProductID IN (@ProductID)  
    ```  
  
    > [!IMPORTANT]  
    >  Si no incluye los paréntesis alrededor de la variable como se indicó anteriormente, no se puede representar el informe y se muestra el error "debe declarar la variable escalar".  
  
     Se crea automáticamente un parámetro de conjunto de datos para un conjunto de datos incrustado o compartido para la variable de consulta. Se crea automáticamente un parámetro de informe para el parámetro de conjunto de datos.  
  
4.  En el panel **Datos de informe** , expanda el nodo **Parámetros** , haga clic con el botón derecho en el parámetro de informe que se creó automáticamente para el parámetro de conjunto de datos y, después, haga clic en **Propiedades del parámetro**.  
  
5.  En la pestaña **General** , seleccione **Permitir varios valores** para permitir a los usuarios seleccionar más de un valor para el parámetro.  
  
6.  (Opcionalmente) En la pestaña **Valores disponibles** , especifique una lista de valores disponibles que se mostrarán al usuario.  
  
     La existencia de una lista de valores disponibles limita las opciones del usuario a únicamente los valores válidos para el parámetro. Cuando hay varios valores, en la parte superior de la lista aparece la característica **Seleccionar todo** , que permite al usuario seleccionar o desactivar todos los valores con un solo clic. Si opta por obtener los valores disponibles para el parámetro de informe a partir de una consulta del conjunto de datos, asegúrese de seleccionar un conjunto de datos que no contenga la variable de consulta que se asoció al mismo parámetro de informe.  
  
     Para más información, vea [Agregar, cambiar o eliminar los valores disponibles para un parámetro de informe &#40;Generador de informes y SSRS&#41;](add-change-or-delete-available-values-for-a-report-parameter.md).  
  
### <a name="to-add-a-multi-value-parameter"></a>Para agregar un parámetro de varios valores  
  
1.  En el Generador de informes, abra el informe al que desea agregar el parámetro de varios valores.  
  
2.  Haga clic con el botón derecho en el conjunto de datos del informe y, después, haga clic en **Propiedades del conjunto de datos**.  
  
3.  Agregue una variable a la consulta del conjunto de datos; para ello, edite el texto de la consulta en el cuadro **Consulta** o agregue un filtro mediante el diseñador de consultas. Para más información, vea [Crear una consulta en el Diseñador de consultas relacionales &#40;Generador de informes y SSRS&#41;](../report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md).  
  
    > [!IMPORTANT]  
    >  El texto de consulta no debe incluir la instrucción DECLARE para la variable de consulta.  
  
    > [!IMPORTANT]  
    >  El texto de la variable de consulta debe incluir el operador `IN`, como se muestra en el ejemplo siguiente.  
  
    ```  
    WHERE  
      Production.ProductInventory.ProductID IN (@ProductID)  
    ```  
  
    > [!IMPORTANT]  
    >  Si no incluye los paréntesis alrededor de la variable como se indicó anteriormente, no se puede representar el informe y se muestra el error "debe declarar la variable escalar".  
  
     Se crea automáticamente un parámetro de conjunto de datos para un conjunto de datos incrustado o compartido para la variable de consulta. Se crea automáticamente un parámetro de informe para el parámetro de conjunto de datos.  
  
4.  En el panel **Datos de informe** , expanda el nodo **Parámetros** , haga clic con el botón derecho en el parámetro de informe que se creó automáticamente para el parámetro de conjunto de datos y, después, haga clic en **Propiedades del parámetro**.  
  
5.  En la pestaña **General** , seleccione **Permitir varios valores** para permitir a los usuarios seleccionar más de un valor para el parámetro.  
  
6.  (Opcionalmente) En la pestaña **Valores disponibles** , especifique una lista de valores disponibles que se mostrarán al usuario.  
  
     La existencia de una lista de valores disponibles limita las opciones del usuario a únicamente los valores válidos para el parámetro. Cuando hay varios valores, en la parte superior de la lista aparece la característica **Seleccionar todo** , que permite al usuario seleccionar o desactivar todos los valores con un solo clic. Si opta por obtener los valores disponibles para el parámetro de informe a partir de una consulta del conjunto de datos, asegúrese de seleccionar un conjunto de datos que no contenga la variable de consulta que se asoció al mismo parámetro de informe.  
  
     Para más información, vea [Agregar, cambiar o eliminar los valores disponibles para un parámetro de informe &#40;Generador de informes y SSRS&#41;](add-change-or-delete-available-values-for-a-report-parameter.md).  
  
## <a name="see-also"></a>Vea también  
 [Agregar parámetros en cascada a un informe &#40;Generador de informes y SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Agregar, cambiar o eliminar parámetros de informe &#40;Generador de informes y SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)  
  
  
