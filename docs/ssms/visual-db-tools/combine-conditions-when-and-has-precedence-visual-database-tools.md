---
title: Combinar condiciones cuando AND tiene prioridad (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- AND, Criteria pane
ms.assetid: 450eb2eb-6ea3-405b-8dd2-1ff926c016e7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 58519cd3150c11496c3b8d3b672f3fe9001ae39a
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262510"
---
# <a name="combine-conditions-when-and-has-precedence-visual-database-tools"></a>Combinar condiciones cuando AND tiene prioridad (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Para combinar condiciones con AND, agregue la columna a la consulta dos veces (una para cada condición). Para combinar condiciones con OR, debe incluir la primera de ellas en la columna Filtro y las demás en una columna **O…** .  
  
Imagine, por ejemplo, que desea buscar los empleados que llevan trabajando más de cinco años en la compañía en puestos de bajo nivel o los empleados con puestos de nivel intermedio independientemente de su fecha de contratación. Esta consulta requiere tres condiciones, dos de ellas unidas con AND:  
  
-   Empleados con una fecha de contratación anterior a cinco años AND con un puesto de nivel 100.  
  
    -O bien-  
  
-   Empleados con un puesto de nivel 200.  
  
### <a name="to-combine-conditions-when-and-has-precedence"></a>Para combinar condiciones cuando AND tiene precedencia  
  
1.  En el [panel Criterios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), agregue las columnas de datos en las que desee realizar la búsqueda. Si desea buscar en la misma columna utilizando dos o más condiciones unidas con AND, debe agregar el nombre de la columna de datos una vez por cada valor que desee buscar.  
  
2.  En la columna **Filtro** , especifique todas las condiciones que desea vincular con AND. Por ejemplo, para vincular condiciones con AND que busquen en las columnas `hire_date` y `job_lvl` , deberán especificarse los valores `< '1/1/91'` y `= 100`, respectivamente, en la columna Filtro.  
  
    Estas entradas de la cuadrícula generan la siguiente cláusula WHERE en la instrucción del [panel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md):  
  
    ```  
    WHERE (hire_date < '01/01/91') AND  
      (job_lvl = 100)  
    ```  
  
3.  En la columna de cuadrícula **O...** , especifique las condiciones que desea unir con OR. Por ejemplo, para agregar una condición que busque otro valor en la columna `job_lvl` , especifique un valor adicional en la columna **O…** (por ejemplo, `= 200`).  
  
    Al agregar un valor a la columna **O…** , se agrega otra condición a la cláusula WHERE en la instrucción del panel SQL:  
  
    ```  
    WHERE (hire_date < '01/01/91' ) AND  
      (job_lvl = 100) OR   
      (job_lvl = 200)  
    ```  
  
## <a name="see-also"></a>Consulte también  
[Combinar condiciones cuando OR tiene prioridad (Visual Database Tools)](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
[Convenciones para combinar condiciones de búsqueda en el panel Criterios (Visual Database Tools)](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[Reglas para especificar valores de búsqueda (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Especificar criterios de búsqueda (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
