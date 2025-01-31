---
title: Acceso a los ensamblados personalizados a través de expresiones | Microsoft Docs
ms.date: 03/04/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- expressions [Reporting Services], custom assemblies
- static member calls
- instance member calls [Reporting Services]
- calling class members
- custom assemblies [Reporting Services], expressions
ms.assetid: 917c4d47-1a95-4f54-98b1-e8cb2165d90f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 101af9d59d4a3f1e48d85859c91f77c8be2e4719
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194362"
---
# <a name="accessing-custom-assemblies-through-expressions"></a>Acceso a los ensamblados personalizados a través de expresiones
  Cuando haya creado un ensamblado personalizado, lo haya puesto a disposición del Diseñador de informes o del servidor de informes, y haya agregado la directiva de seguridad adecuada y una referencia al ensamblado personalizado en la definición de informe, podrá tener acceso a los miembros de las clases en el ensamblado mediante expresiones de informe. Para incluir en una expresión una referencia a código personalizado, debe llamar al miembro de una clase dentro del ensamblado. La manera de hacerlo depende de si el método es estático o se basa en instancias.  
  
## <a name="calling-static-members-from-a-report-definition-file"></a>Llamar a miembros estáticos desde un archivo de definición de informe  
 Los miembros estáticos pertenecen a la clase o al propio tipo, y no a un objeto con instancias. Se puede tener acceso a estos miembros llamándoles directamente desde la clase. Debería utilizar miembros estáticos para llamar a las funciones personalizadas en un informe siempre que sea posible, porque se comportan mejor. Para llamar a un miembro estático, tiene que hacer referencia a él como expresión con el formato =*EspacioDeNombres.Clase.Método*.  
  
#### <a name="to-call-static-members"></a>Para llamar a los miembros estáticos  
  
-   Para llamar a un miembro estático, establezca la expresión igual al nombre completo del miembro, lo que incluye el espacio de nombres, el nombre de la clase y el nombre del miembro. En el ejemplo siguiente se llama al método **ToGBP**, que convierte el valor de campo **StandardCost** de dólares a libras esterlinas y lo presenta en un informe:  
  
    ```  
    =CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
    ```  
  
### <a name="important-information-regarding-static-fields-and-properties"></a>Información importante con respecto a los campos estáticos y propiedades  
 Actualmente, todos los informes se ejecutan en el mismo dominio de aplicación. Esto significa que los informes con datos estáticos específicos del usuario exponen estos datos a otras instancias del mismo informe. Esta condición podría permitir que los datos estáticos de un usuario estuvieran disponibles para todos los usuarios que ejecutaran actualmente un informe determinado. Por esta razón, es muy aconsejable no usar campos estáticos ni propiedades en ensamblados personalizados ni en el elemento **Code**. En su lugar, utilice campos de instancia o propiedades en los informes. Se pueden seguir utilizando los métodos estáticos, porque no almacenan el estado ni los datos.  
  
## <a name="calling-instance-members-from-a-report-definition-file"></a>Llamar a miembros de instancia desde un archivo de definición de informe  
 Si un ensamblado personalizado contiene miembros de instancia a los que debe obtener acceso en una definición de informe, debe agregar al informe un nombre de instancia para la clase. Puede agregar un nombre de instancia para una clase utilizando la pestaña **Código** del cuadro de diálogo **Propiedades del informe**. Para obtener más información sobre cómo agregar instancias de clases a un informe, vea [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 Para llamar a un miembro estático, tiene que hacer referencia a él como expresión con el formato =Code*NombreDeInstancia.Método*.  
  
#### <a name="to-call-instance-members"></a>Para llamar a los miembros de instancia  
  
-   Para llamar a un miembro de instancia de un ensamblado personalizado, debe hacer referencia a la palabra clave **Code** seguida del nombre de instancia y el método. En el ejemplo siguiente se llama a un método de instancia **ToEUR** que convierte el valor del campo **StandardCost** de dólares a euros y los muestra en un informe:  
  
    ```  
    =Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Usar ensamblados personalizados con informes](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
