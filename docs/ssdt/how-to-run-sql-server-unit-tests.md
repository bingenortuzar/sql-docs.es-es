---
title: 'Procedimientos: Ejecutar pruebas unitarias de SQL Server | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 34fe2d1e-d47b-4808-af56-8cc0fdae6518
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d17120b0c13ab1910d4636a376963f5ec74813eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035021"
---
# <a name="how-to-run-sql-server-unit-tests"></a>Procedimientos: Ejecución de pruebas unitarias de SQL Server
Puede ejecutar una prueba unitaria de SQL Server de varias maneras, por ejemplo mediante varias ventanas y la ventana del símbolo del sistema.  
  
> [!NOTE]  
> No puede ejecutar pruebas unitarias de forma remota.  
  
Las maneras disponibles dependen del software que haya instalado, como se describe en [Ejecutar pruebas unitarias de SQL Server](../ssdt/running-sql-server-unit-tests.md).  
  
### <a name="to-run-sql-server-unit-tests-using-test-view-visual-studio-2010"></a>Para ejecutar pruebas unitarias de SQL Server mediante la Vista de pruebas (Visual Studio 2010)  
  
1.  En el menú **Prueba**, seleccione **Ventanas** y haga clic en **Vista de pruebas**.  
  
    Se abre la ventana **Vista de pruebas**.  
  
2.  En la ventana **Vista de pruebas**, haga clic en la prueba o pruebas que desea ejecutar. Mediante la tecla CTRL o la tecla MAYÚS, puede especificar bloques discontinuos o continuos de pruebas.  
  
3.  Realice una de las acciones siguientes:  
  
    -   Haga clic con el botón secundario en la superficie de la ventana **Vista de pruebas** y haga clic en **Ejecutar selección**.  
  
    -   En la barra de herramientas **Vista de pruebas**, haga clic en **Ejecutar selección**.  
  
### <a name="to-run-sql-server-unit-tests-using-test-explorer-visual-studio-2012"></a>Para ejecutar pruebas unitarias de SQL Server mediante el Explorador de pruebas (Visual Studio 2012)  
  
1.  En el menú **Prueba**, seleccione **Ventanas** y haga clic en **Explorador de pruebas**.  
  
    Se abre la ventana **Explorador de pruebas**.  
  
2.  En la ventana **Explorador de pruebas**, haga clic en la prueba o pruebas que desea ejecutar. Mediante la tecla CTRL o la tecla MAYÚS, puede especificar bloques discontinuos o continuos de pruebas.  
  
3.  Haga clic con el botón secundario en una de las pruebas resaltadas y, a continuación, haga clic en **Ejecutar pruebas seleccionadas**.  
  
### <a name="to-run-sql-server-unit-tests-from-the-sql-server-unit-test-designer-visual-studio-2010"></a>Para ejecutar pruebas unitarias de SQL Server desde el Diseñador de pruebas unitarias de SQL Server (Visual Studio 2010)  
  
-   En la barra de herramientas **Herramientas de prueba** encontrará botones para iniciar un proyecto con o sin el depurador.  
  
Este paso ejecuta todas las pruebas de la serie de pruebas actual. En cuanto se inicia una serie de pruebas, aparece la ventana **Resultados de pruebas**, que muestra el progreso de la serie de pruebas. Esta pantalla incluye las pruebas que se están ejecutando y las pruebas que se han completado. Para más información, consulte [Interpretar los resultados de pruebas unitarias de SQL Server](../ssdt/interpreting-sql-server-unit-test-results.md).  
  
## <a name="see-also"></a>Consulte también  
[Ejecutar pruebas unitarias de SQL Server](../ssdt/running-sql-server-unit-tests.md)  
[Cómo: Ejecutar pruebas automatizadas desde Microsoft Visual Studio 2010](https://msdn.microsoft.com/library/ms182470(VS.100).aspx)  
[Ejecutar pruebas automatizadas desde la línea de comandos (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182486(VS.100).aspx)  
[Probar la aplicación (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182409.aspx)  
  
