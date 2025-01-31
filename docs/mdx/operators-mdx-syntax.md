---
title: Operadores (sintaxis de MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5067793ae0f5533a889973e18f7b300914df9092
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892112"
---
# <a name="operators-mdx-syntax"></a>Operadores (sintaxis de MDX)


  En las expresiones multidimensionales (MDX), los operadores permiten llevar a cabo las siguientes acciones:  
  
-   Cambiar datos, permanente o temporalmente.  
  
-   Buscar valores u objetos que cumplan una condición específica.  
  
-   Implementar una decisión entre columnas o expresiones.  
  
-   Probar determinadas condiciones antes de iniciar o confirmar una transacción, o antes de ejecutar determinadas instrucciones.  
  
 MDX es compatible con los operadores que se indican en la siguiente tabla:  
  
|Para realizar este tipo de operación|Usar|  
|---------------------------------------|---------|  
|Asignar un valor a una variable o asociar una columna de un conjunto de resultados a un alias.|[Operadores de asignación](../mdx/assignment-operators.md)|  
|Sumar, restar, multiplicar, dividir.|[Operadores aritméticos](../mdx/arithmetic-operators.md)|  
|Probar si una condición es cierta, como AND, OR, NOT y XOR.|[Operadores bit a bit](../mdx/bitwise-operators.md)|  
|Comparar un valor con otro valor o una expresión.|[Operadores de comparación](../mdx/comparison-operators.md)|  
|Combinar de forma permanente o temporal dos cadenas en una.|[Operadores de concatenación](../mdx/concatenation-operators.md)|  
|Combinar temporal o permanentemente dos conjuntos de expresiones en un solo conjunto.|[Operadores de conjuntos](../mdx/set-operators.md)|  
|Realizar una operación en un operando.|[Operadores unarios](../mdx/unary-operators.md)|  
  
> [!NOTE]  
>  En las consultas, cualquier persona que pueda ver los datos del cubo que se usarán con algún tipo de operador puede realizar operaciones. Para cambiar los datos correctamente, son necesarios los permisos adecuados.  
  
 Cuando se utilizan varios operadores, el orden en que MDX los evalúa es importante. Del mismo modo, es posible que el usuario de los operadores tenga que convertir un tipo de datos en otro para poder evaluar los operadores.  
  
## <a name="evaluating-complex-expressions"></a>Evaluar expresiones complejas  
 Puede generar una expresión mediante el uso de operadores que combinen varias expresiones más pequeñas. En estas expresiones complejas, MDX evalúa los operadores en orden en función de la definición de la prioridad de los [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]operadores utilizada por. MDX ejecuta los operadores con mayor precedencia antes que los operadores con menor precedencia.  
  
### <a name="understanding-operator-precedence"></a>Descripción de la precedencia de los operadores  
 En la siguiente lista se muestra la precedencia de los operadores, de mayor a menor. Los operadores situados en la misma línea tienen el mismo nivel de precedencia y se evalúan de izquierda a derecha, salvo que el uso de un paréntesis obligue a hacerlo de otro modo:  
  
-   IS  
  
-   AS  
  
-   DISTINCT  
  
-   :  
  
-   ^  
  
-   /, *  
  
-   +, -  
  
-   EXISTING  
  
-   <>, >=, =, \<=, >, <  
  
-   NOT  
  
-   Y  
  
-   XOR  
  
-   OR  
  
 Para obtener más información sobre los operadores en MDX, vea MDX [ &#40;Operator&#41;Reference MDX](../mdx/mdx-operator-reference-mdx.md).  
  
### <a name="determining-results"></a>Determinar los resultados  
 Cuando se combinan expresiones simples para crear una más compleja, el tipo de datos del valor resultante viene determinado por la combinación de las reglas de los operadores con las reglas de precedencia para los tipos de datos.  
  
 Si el resultado es un carácter o un valor de Unicode, la intercalación del resultado viene determinada por la combinación de las reglas de los operadores con las reglas de precedencia de intercalación. Para obtener más información acerca de las intercalaciones, consulte [idiomas e Intercalaciones &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/languages-and-collations-analysis-services).  
  
 También hay reglas que determinan la precisión, escala y longitud del resultado basándose en la precisión, escala y longitud de las expresiones sencillas.  
  
## <a name="converting-data-types"></a>Convertir tipos de datos  
 MDX convierte implícitamente un objeto a un tipo distinto cuando el objeto se usa en una expresión que requiere un tipo diferente. En la siguiente tabla se definen las reglas de conversión de cada objeto.  
  
|Tipo original|Tipo necesario|Conversión|  
|-------------------|-----------------|----------------|  
|Nivel|Establecer|\<Level >. Members|  
|Hierarchy|Member|\<> de jerarquía. DefaultMember|  
|Member|Tuple|(\<> Miembro)|  
|Tuple|Member|\<tuple>.item(0)|  
|Tuple|Escalar|\<tuple>.value|  
  
## <a name="see-also"></a>Vea también  
 [MDX de referencia &#40;de operadores MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [MDX (elementos &#40;de sintaxis MDX)&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
