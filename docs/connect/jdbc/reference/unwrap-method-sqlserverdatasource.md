---
title: Método Unwrap (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eb8abe29-f3ec-4752-a590-1d5dc3e48f08
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f8cb254ba464b0e051c00c7ac6d410c5e6da1e36
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997287"
---
# <a name="unwrap-method-sqlserverdatasource"></a>Método unwrap (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un objeto que implementa la interfaz especificada para permitir el acceso a los métodos específicos de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *iface*  
  
 Una clase de tipo T que define una interfaz.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto que implementa la interfaz especificada.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) queda definido por la interfaz java.sql.Wrapper, que se incorporó en las especificaciones de JDBC 4.0.  
  
 Es posible que las aplicaciones necesiten acceso a las extensiones para la API de JDBC que sean específicas de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. El método unwrap admite la desencapsulación para las clases públicas que extiende este objeto si las clases exponen extensiones de proveedor.  
  
 Cuando se llama a este método, el objeto desencapsula la clase [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
 Para obtener más información, vea [contenedores e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método isWrapperFor &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)   
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
