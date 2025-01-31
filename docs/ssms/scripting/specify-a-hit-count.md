---
title: Especificar un número de llamadas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.breakpt.hitcount
helpviewer_keywords:
- Transact-SQL debugger, breakpoint hit count
ms.assetid: 24836939-94ed-4e57-aa85-5d6938d859e4
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 862d99fd57b22e1643ce2591fccfb0478b664074
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267695"
---
# <a name="specify-a-hit-count"></a>Especificar un número de llamadas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Un número de llamadas al punto de interrupción es un contador que el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] incrementa cada vez que se alcanza el punto de interrupción. Si se alcanza el número de llamadas especificado y se satisface la condición de punto de interrupción especificada, el depurador realiza la acción definida para el punto de interrupción.  
  
## <a name="hit-count-considerations"></a>Consideraciones sobre el número de llamadas  
 De forma predeterminada, la ejecución se interrumpe cada vez se ejecuta un punto de interrupción. Puede elegir entre las siguientes opciones:  
  
-   Interrumpir siempre ( valor predeterminado).  
  
-   Interrumpir cuando el número de llamadas alcanza un valor especificado.  
  
-   Interrumpir cuando el número de llamadas alcanza un múltiplo de un valor especificado.  
  
-   Interrumpir cuando el número de llamadas es mayor o igual que un valor especificado.  
  
 Los números de llamadas al punto de interrupción se incrementan dentro del ámbito de una sesión de depuración. Todos los números de llamadas se establecen en cero al comienzo de cada sesión de depuración.  
  
 Si desea realizar un seguimiento del número de veces que se ejecuta un punto de interrupción sin disponer de la ejecución de detención de punto de interrupción, especifique un número de llamadas con un valor muy alto para que nunca se produzca la detención de punto de interrupción.  
  
 La acción predeterminada para un punto de interrupción es que se detenga la ejecución cuando se hayan satisfecho el número de llamadas y la condición de punto de interrupción. Para obtener información sobre cómo especificar otras acciones, vea [Especificar una acción del punto de interrupción](../../relational-databases/scripting/specify-a-breakpoint-action.md).  
  
#### <a name="to-specify-a-hit-count"></a>Para especificar un número de llamadas  
  
1.  En la ventana del editor, haga clic con el botón derecho en el glifo de punto de interrupción y, luego, haga clic en **Número de llamadas** del menú contextual.  
  
     -O bien-  
  
     En la ventana **Puntos de interrupción** , haga clic con el botón derecho en el glifo de punto de interrupción y, luego, haga clic en **Número de llamadas** del menú contextual.  
  
2.  En el cuadro de diálogo **Número de llamadas al punto de interrupción** , seleccione el comportamiento que desea en el cuadro **Cuando el punto de interrupción se visita** .  
  
     Si elige un valor distinto de **Interrumpir siempre**, aparecerá un cuadro de texto a la derecha de la lista. Escriba un número entero en el cuadro de texto para especificar el número de llamadas que desea.  
  
3.  Haga clic en **Aceptar** para implementar los cambios o en **Cancelar** para salir sin aplicar los cambios.  
  
#### <a name="to-view-or-reset-the-current-hit-count"></a>Para ver o restablecer el número de llamadas actual  
  
1.  En la ventana del editor, haga clic con el botón derecho en el glifo de punto de interrupción y, luego, haga clic en **Número de llamadas** del menú contextual.  
  
     -O bien-  
  
     En la ventana **Puntos de interrupción** , haga clic con el botón derecho en el glifo de punto de interrupción y, luego, haga clic en **Número de llamadas** del menú contextual.  
  
2.  En el cuadro de diálogo **Número de llamadas al punto de interrupción** , se muestra el **Número actual** justo encima del botón **Restablecer** .  
  
3.  Haga clic en **Restablecer** si desea establecer en cero el número de llamadas actual.  
  
4.  Haga clic en **Aceptar** o en **Cancelar** para salir del cuadro de diálogo.  
  
## <a name="see-also"></a>Consulte también  
 [Especificar una condición de punto de interrupción](../../relational-databases/scripting/specify-a-breakpoint-condition.md)  
  
  
