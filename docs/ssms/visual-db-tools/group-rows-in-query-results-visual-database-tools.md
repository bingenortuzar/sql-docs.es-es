---
title: Agrupar filas en los resultados de la consulta (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing table subsets
- grouping rows
- grouping query results
ms.assetid: b07082d5-4d55-4903-9af9-4c470554c6d3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3208a3458098b85325a19c014d99bca3b4f05c4d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68254477"
---
# <a name="group-rows-in-query-results-visual-database-tools"></a>Agrupar filas en los resultados de la consulta (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Si desea crear subtotales o mostrar otra información de resumen para los subconjuntos de una tabla, debe crear grupos mediante una consulta de funciones agregadas. Cada grupo resume los datos para todas las filas de la tabla que tienen el mismo valor.  
  
Por ejemplo, es posible que desee ver el precio medio de un libro en la tabla `titles` , pero con los resultados desglosados por editorial. Para ello, agrupe la consulta por editorial (por ejemplo, `pub_id`). El resultado de la consulta podría tener el siguiente aspecto:  
  
![Resultados de la consulta: precio medio agrupado por publicador](../../ssms/visual-db-tools/media/dv3w9e1.gif "Resultados de la consulta: precio medio agrupado por publicador")  
  
Cuando se agrupan datos, solo se pueden mostrar valores resumidos o agrupados, como:  
  
-   Los valores de las columnas agrupadas (aquellos que aparecen en la cláusula GROUP BY). En el ejemplo anterior, `pub_id` es la columna agrupada.  
  
-   Valores generados por funciones de agregado como SUM( ) y AVG( ). En el ejemplo anterior, la segunda columna se genera usando la función AVG( ) con la columna `price` .  
  
No se pueden mostrar valores de filas individuales. Por ejemplo, si agrupa únicamente por editorial, no podrá mostrar tampoco los títulos individuales en la consulta. Por tanto, si se agregan columnas al resultado de la consulta, el [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) las agregará automáticamente a la cláusula GROUP BY de la instrucción en el [panel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md). Si, en su lugar, se desea agregar una columna, se puede especificar una función de agregado para esa columna.  
  
Si utiliza varias columnas para la agrupación, en cada grupo de la consulta se muestran los valores de agregado de todas las columnas de agrupación.  
  
Por ejemplo, la siguiente consulta de la tabla `titles` agrupa por editorial (`pub_id`) y por tipo de libro (`type`). Los resultados de la consulta se ordenan por editorial e incluyen información de resumen para cada tipo de libro diferente producido por la editorial:  
  
```  
SELECT pub_id, type, SUM(price) Total_price  
FROM titles  
GROUP BY pub_id, type  
```  
  
El resultado de la consulta podría tener el siguiente aspecto:  
  
![Resultados de la consulta: precio agrupado por publicador y tipo](../../ssms/visual-db-tools/media/dv3w9e2.gif "Resultados de la consulta: precio agrupado por publicador y tipo")  
  
### <a name="to-group-rows"></a>Para agrupar filas  
  
1.  Inicie la consulta agregando las tablas que desea resumir al panel Diagrama.  
  
2.  Haga clic con el botón derecho en el fondo del panel Diagrama y, a continuación, elija **Agregar grupo por** en el menú contextual. El Diseñador de consultas y vistas agrega una columna **Agrupar por** a la cuadrícula en el panel Criterios.  
  
3.  Agregue la columna o columnas que desea agrupar al panel Criterios. Si desea que la columna aparezca en los resultados de la consulta, asegúrese de que la columna **Resultados** está seleccionada para el resultado.  
  
    El Diseñador de consultas y vistas agrega una cláusula GROUP BY a la instrucción en el panel SQL. Por ejemplo, la instrucción SQL podría tener el siguiente aspecto:  
  
    ```  
    SELECT pub_id  
    FROM titles  
    GROUP BY pub_id  
    ```  
  
4.  Agregue la columna o columnas que desea agregar al panel Criterios. Asegúrese de que la columna está marcada para el resultado.  
  
5.  En la celda de cuadrícula **Agrupar por** de la columna que se va a agregar, seleccione la función de agregado correspondiente.  
  
    El Diseñador de consultas y vistas asigna automáticamente un alias a la columna que va a resumir. Puede sustituir este alias generado automáticamente por otro más significativo. Para más detalles, consulte [Crear alias de columna (Visual Database Tools)](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
    ![Agregar un alias de columna al conjunto de resultados de la consulta](../../ssms/visual-db-tools/media/dv3w9e3.gif "Agregar un alias de columna al conjunto de resultados de la consulta")  
  
    La instrucción correspondiente en el panel **SQL** podría tener el siguiente aspecto:  
  
    ```  
    SELECT   pub_id, SUM(price) AS Totalprice  
    FROM     titles  
    GROUP BY pub_id  
    ```  
  
## <a name="see-also"></a>Consulte también  
[Ordenar y agrupar los resultados de una consulta (Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
