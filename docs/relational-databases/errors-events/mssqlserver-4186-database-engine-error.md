---
title: MSSQLSERVER_4186 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4186 (Database Engine error)
ms.assetid: 1ae88554-f291-45bc-a186-6f41d9cd0fca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3efa12b744d331949fc0af18f555e603f18e33ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123098"
---
# <a name="mssqlserver4186"></a>MSSQLSERVER_4186
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|4186|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico||  
|Texto del mensaje|No se puede hacer referencia a la columna '%ls.%.*ls' en la cláusula OUTPUT porque la definición de columna contiene una subconsulta o hace referencia a una función que obtiene acceso a datos de usuario o del sistema. De forma predeterminada, se asume que una función obtiene acceso a los datos si no está enlazada a un esquema. Considere la posibilidad de quitar la subconsulta o la función de la definición de columna o quitar la columna de la cláusula OUTPUT.|  
  
## <a name="explanation"></a>Explicación  
Para evitar un comportamiento no determinista, la cláusula OUTPUT no puede hacer referencia a una columna desde una vista o una función insertada con valores de tabla si dicha tabla se ha definido mediante uno de los métodos siguientes:  
  
-   Una subconsulta.  
  
-   Una función definida por el usuario que obtiene acceso a datos de usuario o del sistema, o que se asume que obtiene dicho acceso.  
  
-   Una columna calculada que contiene una función definida por el usuario que obtiene acceso a datos de usuario o del sistema en su definición.  
  
### <a name="examples"></a>Ejemplos  
**Columna de vista definida por una subconsulta**  
  
En el ejemplo siguiente se crea una vista que usa una subconsulta en la lista de selección para definir la columna `State`. A continuación, una instrucción UPDATE hace referencia a la columna `State` en la cláusula OUTPUT y produce un error a causa de la subconsulta en la lista de selección.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW dbo.V1  
AS  
    SELECT City,  
-- subquery to return the State name  
           (SELECT Name FROM Person.StateProvince AS sp   
            WHERE sp.StateProvinceID = a.StateProvinceID) AS State  
    FROM Person.Address AS a;  
GO  
--Reference the State column in the OUTPUT clause of an UPDATE statement  
UPDATE dbo.V1   
SET City = City + 'Test'   
OUTPUT deleted.City, deleted.State, inserted.City, inserted.State  
WHERE State = 'Texas';  
GO  
```  
  
**Columna de vista definida por una función**  
  
En el ejemplo siguiente se crea una vista que usa la función escalar de acceso a datos `dbo.ufnGetStock`de la lista de selección para definir la columna `CurrentInventory`. A continuación, una instrucción UPDATE hace referencia a la columna `CurrentInventory` en la cláusula OUTPUT.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW Production.ReorderLevels  
AS  
    SELECT ProductID, ProductModelID, ReorderPoint,  
           dbo.ufnGetStock(ProductID) AS CurrentInventory  
    FROM Production.Product;  
GO  
  
UPDATE Production.ReorderLevels  
SET ReorderPoint += CurrentInventory  
OUTPUT deleted.ReorderPoint, deleted.CurrentInventory,  
       inserted.ReorderPoint, inserted.CurrentInventory  
WHERE ProductModelID BETWEEN 75 and 80;  
```  
  
## <a name="user-action"></a>Acción del usuario  
El error 4186 se puede corregir de una de las siguientes maneras:  
  
-   Use combinaciones en lugar de subconsultas para definir la columna en la vista o en la función. Por ejemplo, puede volver a escribir la vista `dbo.V1` como sigue.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE VIEW dbo.V1  
    AS  
        SELECT City, sp.Name AS State  
        FROM Person.Address AS a   
        JOIN Person.StateProvince AS sp   
        ON sp.StateProvinceID = a.StateProvinceID;  
    ```  
  
-   Examine la definición de la función definida por el usuario. Si la función no obtiene acceso a datos de usuario o del sistema, modifíquela para que incluya la cláusula WITH SCHEMABINDING.  
  
-   Quite la columna de la cláusula OUTPUT.  
  
## <a name="see-also"></a>Consulte también  
[OUTPUT Clause &#40;Transact-SQL&#41;](~/t-sql/queries/output-clause-transact-sql.md)  
  
