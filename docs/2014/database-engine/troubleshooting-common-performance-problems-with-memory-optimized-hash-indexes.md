---
title: Solución de problemas de rendimiento comunes con los índices Hash optimizados para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 1954a997-7585-4713-81fd-76d429b8d095
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d7ed4098feb8bfd2d156e3de2f81fbf7329915aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62842540"
---
# <a name="troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes"></a>Solucionar problemas habituales de rendimiento con los índices hash con optimización para memoria
  Este tema se centrará en la solución de problemas y soluciones alternativas a los problemas comunes con índices de hash.  
  
## <a name="search-requires-a-subset-of-hash-index-key-columns"></a>La búsqueda requiere un subconjunto de columnas de clave de índice de hash  
 **Problema:** Los índices de hash requieren valores para todas las columnas de clave de índice con el fin de calcular el valor hash y ubicar las filas correspondientes en la tabla hash. Por consiguiente, si una consulta incluye predicados de igualdad únicamente para un subconjunto de las claves de índice en la cláusula WHERE, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no puede utilizar una operación INDEX SEEK para ubicar las filas correspondientes a los predicados de la cláusula WHERE.  
  
 En cambio, los índices ordenados como los índices no clúster basados en disco y los índices no clúster optimizados para memoria admiten INDEX SEEK en un subconjunto de las columnas de clave de índice, siempre y cuando sean las columnas iniciales del índice.  
  
 **Síntoma:** Esto da como resultado una degradación del rendimiento, como [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] debe ejecutar recorridos de tabla completos en lugar de una búsqueda de índice, que normalmente es una operación más rápida.  
  
 **Cómo solucionar problemas:** Además de la degradación del rendimiento, la inspección de los planes de consulta mostrará un recorrido en lugar de una búsqueda de índice. Si la consulta es bastante simple, la inspección del texto de la consulta y de la definición de índice también mostrará si la búsqueda requiere un subconjunto de las columnas de clave de índice.  
  
 Considere la consulta y la tabla siguientes:  
  
```sql  
CREATE TABLE [dbo].[od]  
(  
     o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
     CONSTRAINT PK_od PRIMARY KEY NONCLUSTERED HASH (o_id, od_id) WITH (BUCKET_COUNT = 10000)  
)  
WITH (MEMORY_OPTIMIZED = ON)  
  
 SELECT p_id  
 FROM dbo.od  
 WHERE o_id=1  
```  
  
 La tabla tiene un índice de hash en las dos columnas (o_id, od_id), mientras que la consulta tiene un predicado de igualdad en (o_id). Como la consulta tiene predicados de igualdad en un solo subconjunto de las columnas de clave de índice, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no puede realizar una operación INDEX SEEK con PK_od; en su lugar, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene que volver a un recorrido del índice completo.  
  
 **Soluciones alternativas:** Hay una serie de posibles soluciones. Por ejemplo:  
  
-   Vuelva a crear el índice que sea de tipo no clúster en lugar de hash no clúster. El índice no clúster optimizado para memoria está ordenado y así [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] puede realizar una búsqueda de índice en las columnas iniciales de clave de índice. La definición resultante de clave principal del ejemplo sería `constraint PK_od primary key nonclustered`.  
  
-   Cambie la clave de índice actual para que coincida con las columnas de la cláusula WHERE.  
  
-   Agregue un nuevo índice de hash que coincida con las columnas de la cláusula WHERE de la consulta. En el ejemplo, la definición de tabla resultante se parecería a lo siguiente:  
  
    ```sql  
    CREATE TABLE dbo.od  
     ( o_id INT NOT NULL,  
     od_id INT NOT NULL,  
     p_id INT NOT NULL,  
  
     CONSTRAINT PK_od PRIMARY KEY   
     NONCLUSTERED HASH (o_id,od_id) WITH (BUCKET_COUNT=10000),  
  
     INDEX ix_o_id NONCLUSTERED HASH (o_id) WITH (BUCKET_COUNT=10000)  
  
     ) WITH (MEMORY_OPTIMIZED=ON)  
    ```  
  
 Observe que un índice de hash optimizada para memoria no se ejecuta óptimamente si hay muchas filas duplicadas para un valor de clave de índice determinado: en el ejemplo, si el número de valores únicos para la columna o_id es mucho menor que el número de filas de la tabla, no sería óptimo agregar un índice en (o_id); en su lugar, la mejor solución sería cambiar el tipo del índice PK_od de hash a no clúster. Para obtener más información, vea [Determining the Correct Bucket Count for Hash Indexes](../relational-databases/indexes/indexes.md).  
  
## <a name="see-also"></a>Vea también  
 [Índices de las tablas con optimización para memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
