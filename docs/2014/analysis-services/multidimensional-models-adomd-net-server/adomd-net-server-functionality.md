---
title: Funcionalidad del servidor ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: b74c6957-3f64-4e09-aa09-d06ee93f82fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc127a8bafc9ad2f53465caeca013d5033e5c396
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62702973"
---
# <a name="adomdnet-server-functionality"></a>Funcionalidad del servidor de ADOMD.NET
  Todos los objetos de servidor de ADOMD.NET proporcionan acceso de solo lectura a los datos y metadatos del servidor. Para recuperar datos y metadatos, utilice el modelo de objetos del servidor ADOMD.NET, ya que el modelo de objetos de servidor no admite conjuntos de filas de esquema.  
  
 Con objetos de servidor ADOMD.NET, puede crear una función definida por el usuario (UDF) o un procedimiento almacenado para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para llamar a estos métodos incrustados se utilizan instrucciones de consulta creadas en lenguajes como MDX (Expresiones multidimensionales), DMX (Extensiones de minería de datos) o SQL. Estos métodos incrustados también proporcionan otras funciones sin las latencias asociadas a las comunicaciones de red.  
  
> [!NOTE]  
>  El objeto <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> solamente admite DMX.  
  
## <a name="what-is-a-udf"></a>¿Qué es una UDF?  
 Un *UDF* es un método que tiene las siguientes características:  
  
-   Puede llamar a la UDF en el contexto de una consulta.  
  
-   La UDF puede aceptar un número cualquiera de parámetros.  
  
-   La UDF puede devolver varios tipos de datos.  
  
 En el ejemplo siguiente se utiliza una UDF ficticia, `FinalSalesNumber`:  
  
```  
SELECT SalesPerson.Name ON ROWS,  
       FinalSalesNumber() ON COLUMNS  
FROM SalesModel  
```  
  
## <a name="what-is-a-stored-procedure"></a>¿Qué es un procedimiento almacenado?  
 Un *procedimiento almacenado* es un método que tiene las siguientes características:  
  
-   Se llama a un procedimiento almacenado en su propio con el MDX [llamar](/sql/mdx/mdx-data-manipulation-call) instrucción.  
  
-   Un procedimiento almacenado puede aceptar un número cualquiera de parámetros.  
  
-   Un procedimiento almacenado puede devolver un conjunto de datos, un elemento `IDataReader` o un resultado vacío.  
  
 En el ejemplo siguiente se utiliza un procedimiento almacenado ficticio, `FinalSalesNumbers`:  
  
```  
CALL FinalSalesNumbers()  
```  
  
## <a name="see-also"></a>Vea también  
 [Programación del servidor ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
