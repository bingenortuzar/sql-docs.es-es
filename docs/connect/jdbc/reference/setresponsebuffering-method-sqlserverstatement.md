---
title: Método setResponseBuffering (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a55f1d5695c2595b5ea721680fc77f88d13494ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973111"
---
# <a name="setresponsebuffering-method-sqlserverstatement"></a>Método setResponseBuffering (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el modo de almacenamiento en búfer de respuesta para este objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) en **String full** sin distinción entre mayúsculas y minúsculas o en **adaptive**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *value*  
  
 Un objeto **String** que contiene el modo de almacenamiento en búfer de respuesta. El modo válido puede ser uno de los siguientes valores String que no distinguen mayúsculas de minúsculas: **full** o **adaptive**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El valor **adaptive** especifica que se almacenen en búfer los menos datos posibles cuando sea necesario.  
  
 El valor **full** se especifica mediante la lectura del resultado completo desde el servidor en el tiempo de ejecución.  
  
 Adaptive es el valor predeterminado en la versión 2,0 y 3,0 del controlador JDBC. Full era el valor predeterminado antes de la versión 2,0 del controlador JDBC.  
  
 El método [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) le permite invalidar la propiedad **String** de la conexión **responseBuffering** para el objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) actual. Para obtener más información sobre cómo usar el modo de almacenamiento en búfer de respuesta, vea [usar el almacenamiento en búfer adaptable](../../../connect/jdbc/using-adaptive-buffering.md).  
  
 Si la aplicación especifica un valor de parámetro no válido para el método [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md), se produce una excepción [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [Usar el almacenamiento en búfer adaptable](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  
