---
title: Método getXopenStates (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de6fdf6b-8345-4490-b35e-7115b61e782e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5c263a94b8df0337d05cc8f3ee41df4e2f30fc72
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977932"
---
# <a name="getxopenstates-method-sqlserverdatasource"></a>Método getXopenStates (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un valor **boolean** que indica si está habilitada la conversión de estados SQL a estados conformes a XOPEN.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getXopenStates()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si está habilitada la conversión de Estados SQL a Estados conforme a XOPEN. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Si la propiedad xopenStates se establece en **true**, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] convertirá los estados SQL en estados conformes a XOPEN. El valor predeterminado es **false**, que hace que el controlador JDBC genere códigos de estado de SQL 99. Si no se establece xopenStates, el método getXopenStates devuelve el valor predeterminado **false**.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
