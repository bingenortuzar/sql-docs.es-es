---
title: Consultar un modelo Tabular | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: b01d45d9-4598-4ded-9a9e-e3419cc3df8e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61b6f366843b326a8983c27c3d5ee945604756f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62757741"
---
# <a name="querying-a-tabular-model"></a>Consultar un modelo tabular
  Cuando un programador consulta un modelo tabular, implica la recuperación de datos de la base de datos tabular (TDS); para lograr este objetivo tiene dos opciones: usar consultas de tabla de uso en DAX o usar MDX y recuperar los datos como si provinieran de un cubo. Sin embargo, según el modo subyacente del modelo tabular, podría tener que limitarse a usar solo consultas de tabla DAX; el modo DirectQuery requiere el uso de consultas de tabla DAX.  
  
## <a name="querying-with-adomdnet"></a>Consultar con ADOMD.Net  
 El uso de ADOMD.Net para consultar un modelo tabular es simple y flexible; puede enviar instrucciones MDX o expresiones de consulta tabulares desde DAX al servidor para obtener los resultados.  
  
 El código siguiente muestra cómo pasar las instrucciones de consulta a un modelo tabular y recibir los resultados  
  
```csharp  
//Function: tabularQueryExecute(string qry, ADOMD.AdomdConnection cnx)  
//   - arg: qry, the tabular query or MDX expression to be evaluated  
//   - arg: cnx, an active and opened ADOMD connection to the database where 'qry' is to be evaluated  
//  
// This function takes a query or mdx expression -qry-, a connection -cnx-  
// and runs the query it against a Tabular Model using ADOMD.net  
//  
// Important note:  
//    If the MDX query contains more than 2 axes (ON COLUMNS, ON ROWS), each axis will come as a new column  
//    If the (All) value of the members in any axis have not been defined, a blank cell is returned. This might be misleading  
//    if the model also has missing values... which are also represented with blank cells.  
private DataTable tabularQueryExecute(string qry, ADOMD.AdomdConnection cnx)  
{  
    ADOMD.AdomdDataAdapter currentDataAdapter = new ADOMD.AdomdDataAdapter(qry, cnx);  
    DataTable tabularResults = new DataTable();  
    currentDataAdapter.Fill(tabularResults);  
    return tabularResults;  
}  
  
```  
  
### <a name="example"></a>Ejemplo  
 Si el código anterior se utiliza con la siguiente expresión MDX:  
  
```  
SELECT { [Measures].[Internet Total Sales], [Measures].[Reseller Total Sales], [Measures].[Total Sales] } ON COLUMNS  
     , NON EMPTY [Product Category].[Product Category Name].MEMBERS ON ROWS "  
     , NON EMPTY [Date].[Calendar Year].members ON 2 \n"  
FROM [Model]  
  
```  
  
 Con el modelo de muestra “Adventure Works DW Tabular Denali CTP3” debería recibir los siguientes valores como tabla resultante:  
  
|Año del calendario|Nombre de categoría del producto|Ventas totales por Internet|Ventas totales por distribuidor|Total Sales|  
|-------------------|---------------------------|--------------------------|--------------------------|-----------------|  
|||$     29,358,677.22|$     80,450,596.98|$   109,809,274.20|  
||Accessories|$           700,759.96|$           571,297.93|$        1,272,057.89|  
||Bikes|$     28,318,144.65|$     66,302,381.56|$     94,620,526.21|  
||Clothing|$           339,772.61|$        1,777,840.84|$        2,117,613.45|  
||Componentes||$     11,799,076.66|$     11,799,076.66|  
|2001||$        3,266,373.66|$        8,065,435.31|$     11,331,808.96|  
|2001|Accessories||$              20,235.36|$              20,235.36|  
|2001|Bikes|$        3,266,373.66|$        7,395,348.63|$     10,661,722.28|  
|2001|Clothing||$              34,376.34|$              34,376.34|  
|2001|Componentes||$           615,474.98|$           615,474.98|  
|2002||$        6,530,343.53|$     24,144,429.65|$     30,674,773.18|  
|2002|Accessories||$              92,735.35|$              92,735.35|  
|2002|Bikes|$        6,530,343.53|$     19,956,014.67|$     26,486,358.20|  
|2002|Clothing||$           485,587.15|$           485,587.15|  
|2002|Componentes||$        3,610,092.47|$        3,610,092.47|  
|2003||$        9,791,060.30|$     32,202,669.43|$     41,993,729.72|  
|2003|Accessories|$           293,709.71|$           296,532.88|$           590,242.59|  
|2003|Bikes|$        9,359,102.62|$     25,551,775.07|$     34,910,877.69|  
|2003|Clothing|$           138,247.97|$           871,864.19|$        1,010,112.16|  
|2003|Componentes||$        5,482,497.29|$        5,482,497.29|  
|2004||$        9,770,899.74|$     16,038,062.60|$     25,808,962.34|  
|2004|Accessories|$           407,050.25|$           161,794.33|$           568,844.58|  
|2004|Bikes|$        9,162,324.85|$     13,399,243.18|$     22,561,568.03|  
|2004|Clothing|$           201,524.64|$           386,013.16|$           587,537.80|  
|2004|Componentes||$        2,091,011.92|$        2,091,011.92|  
  
 Si la expresión MDX se reemplaza con esta expresión de consulta de la tabla DAX:  
  
```  
DEFINE  
   MEASURE 'Product Category'[Internet Sales] = SUM( 'Internet Sales'[Sales Amount])  
   MEASURE 'Product Category'[Reseller Sales] = SUM('Reseller Sales'[Sales Amount]) \n"  
   EVALUATE ADDCOLUMNS('Product Category', \"Internet Sales - All Years\", 'Product Category'[Internet Sales], \"Reseller Sales - All Years\", 'Product Category'[Reseller Sales])  
  
```  
  
 Y si se envía al servidor utilizando el código anterior, con el modelo de muestra “Adventure Works DW Tabular Denali CTP3” debería recibir los siguientes valores como tabla resultante:  
  
|Id. de categoría del producto|Id. alternativo de categoría del producto|Nombre de categoría del producto|Internet Sales|Reseller Sales|  
|-------------------------|-----------------------------------|---------------------------|--------------------|--------------------|  
|4|4|Accessories|$        700,759.96|$        571,297.93|  
|1|1|Bikes|$  28,318,144.65|$  66,302,381.56|  
|3|3|Clothing|$        339,772.61|$    1,777,840.84|  
|2|2|Componentes||$  11,799,076.66|  
  
  
