---
title: Método getLastUpdateCount (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0d284e02be13af60bf7d8e7d447835f7eccd90a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982603"
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>Método getLastUpdateCount (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un valor **boolean** que indica si la propiedad lastUpdateCount está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si lastUpdateCount está habilitado. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Si la propiedad lastUpdateCount está establecida en **true**, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] solo devolverá el último recuento de actualizaciones a partir de una instrucción SQL que se haya pasado al servidor. Si la propiedad lastUpdateCount está establecida en **false**, el controlador devolverá todos los recuentos de actualizaciones incluso los que se hayan devuelto por desencadenadores activados. Si no se establece la propiedad lastUpdateCount, el método getLastUpdateCount devuelve el valor predeterminado **true**.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
