---
title: SET FORCEPLAN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_FORCEPLAN_TSQL
- SET FORCEPLAN
- FORCEPLAN
- FORCEPLAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- joins [SQL Server], overriding query optimizer process
- FORCEPLAN option
- SET FORCEPLAN statement
- query optimizer [SQL Server], optimizing process
- overriding query optimizer process
ms.assetid: b6c0b08f-2060-4696-9e12-50cb7e674321
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 84060374e3d46dde985e32a549180d8492c72892
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929004"
---
# <a name="set-forceplan-transact-sql"></a>SET FORCEPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cuando se establece FORCEPLAN en ON, el optimizador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procesa una combinación en el mismo orden en que aparecen las tablas en la cláusula FROM de una consulta. Además, si se establece FORCEPLAN en ON, se fuerza el uso de una combinación de bucles anidados, a menos que sea necesario utilizar otros tipos de combinaciones para construir un plan para la consulta o que se soliciten dichas combinaciones con sugerencias de combinación o sugerencias de consulta.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET FORCEPLAN { ON | OFF }  
```  
  
## <a name="remarks"></a>Notas  
 SET FORCEPLAN básicamente invalida la lógica utilizada por el optimizador de consultas para procesar una instrucción SELECT de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Los datos que devuelve la instrucción SELECT son los mismos, independientemente del valor de esta opción. La única diferencia es el modo en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procesa las tablas para satisfacer la consulta.  
  
 Las sugerencias del optimizador de consultas se pueden usar también en las consultas para influir en el modo en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procesa la instrucción SELECT.  
  
 SET FORCEPLAN se aplica en tiempo de ejecución y no en tiempo de análisis.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, todos los usuarios tienen permisos para ejecutar SET FORCEPLAN.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se realiza una combinación de cuatro tablas. La opción `SHOWPLAN_TEXT` está habilitada, por lo que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve información sobre cómo va a procesar la consulta de forma distinta cuando se habilite la opción `SET FORCE_PLAN`.  
  
```  
USE AdventureWorks2012;  
GO  
-- Make sure FORCEPLAN is set to OFF.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Example where the query plan is not forced.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e  
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
-- SET FORCEPLAN to ON.  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN ON;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
-- Reexecute inner join to see the effect of SET FORCEPLAN ON.  
SELECT p.LastName, p.FirstName, v.Name  
FROM Person.Person AS p  
   INNER JOIN HumanResources.Employee AS e   
   ON e.BusinessEntityID = p.BusinessEntityID  
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
SET FORCEPLAN OFF;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET SHOWPLAN_TEXT &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)  
  
  
