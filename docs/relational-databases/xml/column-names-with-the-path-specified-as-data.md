---
title: Nombres de columna con la ruta de acceso especificada como data() | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: 0b738e44-6108-4417-a9a4-abeb7680d899
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fcec69ca2f7d77f8f5bbdd298dfee3feb2d8c0d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113179"
---
# <a name="column-names-with-the-path-specified-as-data"></a>Nombres de columna con la ruta de acceso especificada como data()

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Si la ruta de acceso especificada como nombre de la columna es "data()", el valor se tratará como valor atómico en el XML generado. Si el siguiente elemento de la serialización también es un valor atómico, se agregará un carácter de espacio al XML. Esto resulta útil cuando se crean valores de elementos y atributos del tipo lista. La consulta siguiente recupera el Id. del modelo de producto, el nombre del producto y una lista de los productos de ese modelo.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT ProductModelID       AS "@ProductModelID",  
       Name                 AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
      FOR XML PATH (''))    AS "@ProductIDs"  
FROM  Production.ProductModel  
WHERE ProductModelID= 7   
FOR XML PATH('ProductModelData');  
```  
  
 La instrucción SELECT anidada recupera una lista de Id. de productos. Especificará "data()" como nombre de columna de los Id. de productos. El modo PATH especifica una cadena vacía para el nombre de elemento de fila, por lo que no se generará ningún elemento de fila. En su lugar, se devolverán los valores como asignados a un atributo ProductIDs del elemento de fila `<ProductModelData>` de la instrucción SELECT primaria. El resultado es el siguiente:  

```sql
<ProductModelData
  ProductModelID="7"
  ProductModelName="HL Touring Frame"
  ProductIDs="885 887 888 889 890 891 892 893"
/>
```

## <a name="see-also"></a>Consulte también  
 [Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
