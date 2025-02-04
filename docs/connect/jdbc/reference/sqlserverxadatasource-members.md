---
title: Miembros SQLServerXADataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 04178645-915f-4569-8907-d45e299bbe7d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2baf4e745e18052646e842eb64445690229ed0b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970175"
---
# <a name="sqlserverxadatasource-members"></a>Miembros de clase SQLServerXADataSource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  En las siguientes tablas se enumeran los miembros que expone la clase [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md).  
  
## <a name="constructors"></a>Constructores  
  
|Nombre|Descripción|  
|----------|-----------------|  
|[SQLServerXADataSource ()](../../../connect/jdbc/reference/sqlserverxadatasource-constructor.md)|Inicializa una instancia nueva de la clase [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md).|  
  
## <a name="fields"></a>Campos  
 Ninguno.  
  
## <a name="inherited-fields"></a>Campos heredados  
 Ninguno.  
  
## <a name="methods"></a>Métodos  
  
|Nombre|Descripción|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve el valor de la propiedad de conexión **applicationIntent**.|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve el nombre de la aplicación.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Intenta establecer una conexión con el origen de datos que representa el objeto DataSource.|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve el nombre de la base de datos.|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve el nombre del servidor de conmutación por error que se utiliza en una configuración de creación de reflejo de la base de datos.|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve un valor **Boolean** que indica si la propiedad lastUpdateCount está habilitada.|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve un valor **int** que indica el número de milisegundos que transcurrirán antes de que la base de datos notifique un tiempo de espera de bloqueo.|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve el número de segundos que transcurrirán hasta que este objeto DataSource intente efectuar una conexión.|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve un flujo de salida de caracteres que se va a utilizar en todos los mensajes de registro y seguimiento.|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Recupera el valor de la propiedad de conexión **multiSubnetFailover**.|  
|[getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)|(Se hereda de [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)) Intenta establecer una conexión a una base de datos física que se puede utilizar como una conexión agrupada.|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve el número de puerto actual que se utiliza para comunicar con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverxadatasource.md)|Devuelve una referencia a este objeto [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md).|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve el tipo de cursor predeterminado que se utiliza para todos los conjuntos de resultados que se crean con el objeto DataSource.|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve un valor **Boolean** que indica si está habilitado el envío de parámetros de tipo **String** al servidor en formato UNICODE.|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve el nombre del equipo que está ejecutando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve la dirección URL que se utiliza para conectar al origen de datos.|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve el nombre de usuario que se utiliza para conectar al origen de datos.|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve el nombre del nombre del equipo cliente que se utiliza para conectar al origen de datos.|  
|[getXAConnection](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)|Intenta establecer una conexión a una base de datos física que se puede utilizar en una transacción distribuida.|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Devuelve un valor **Boolean** que indica si está habilitada la conversión de estados de SQL a estados conforme a XOPEN.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)|Indica si este objeto es un contenedor para la interfaz especificada.|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el valor de la propiedad de conexión **applicationIntent**.|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el nombre de la aplicación.|  
|[setAuthenticationSceme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Indica el tipo de seguridad integrada que quiere que use la aplicación.|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el nombre de la base de datos con la que se va a efectuar la conexión.|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece la descripción del origen de datos.|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el nombre del servidor de conmutación por error que se utiliza en una configuración de creación de reflejo de la base de datos.|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece un valor **Boolean** que indica si la propiedad integratedSecurity está habilitada.|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece un valor **Boolean** que indica si la propiedad lastUpdateCount está habilitada.|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece un valor **int** que indica el número de milisegundos que han de transcurrir antes de que la base de datos notifique un tiempo de espera de bloqueo.|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el número de segundos que transcurrirán hasta que este objeto DataSource intente efectuar una conexión.|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece un flujo de salida de caracteres que se va a utilizar para todos los mensajes de registro y seguimiento.|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el valor de la propiedad de conexión **multiSubnetFailover**.|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece la contraseña que se utilizará para conectar a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el número de puerto que se va a utilizar para comunicar con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el tipo de cursor predeterminado que se utiliza para todos los conjuntos de resultados que se crean con el objeto DataSource.|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece un valor **Boolean** que indica si está habilitado el envío de parámetros de tipo **String** al servidor en formato UNICODE.|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el nombre del equipo que está ejecutando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece la dirección URL que se utiliza para conectar al origen de datos.|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el nombre de usuario que se utiliza para conectar al origen de datos.|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece el nombre del equipo cliente que se utiliza para conectar al origen de datos.|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) Establece un valor **Boolean** que indica si está habilitada la conversión de estados de SQL a estados conforme a XOPEN.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)|Devuelve un objeto que implementa la interfaz especificada para permitir el acceso a los métodos específicos de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].|  
  
## <a name="inherited-methods"></a>Métodos heredados  
  
|Clase heredada de:|Métodos|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource|getPooledConnection|  
|com.microsoft.sqlserver.jdbc.SQLServerDataSource|getApplicationName, getConnection, getDatabaseName, getDescription, getFailoverPartner, getInstanceName, getLastUpdateCount, getLockTimeout, getLoginTimeout, getLogWriter, getPortNumber, getSelectMethod, getSendStringParametersAsUnicode, getServerName, getURL, getUser, getWorkstationID, getXopenStates, setApplicationName, setDatabaseName, setDescription, setFailoverPartner, setInstanceName, setIntegratedSecurity, setLastUpdateCount, setLockTimeout, setLoginTimeout, setLogWriter, setPassword, setPortNumber, setSelectMethod, setSendStringParametersAsUnicode, setServerName, setURL, setUser, setWorkstationID, setXopenStates|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
|javax.sql.XADataSource|getLoginTimeout, getLogWriter, setLoginTimeout, setLogWriter|  
|javax.sql.ConnectionPoolDataSource|getLoginTimeout, getLogWriter, setLoginTimeout, setLogWriter|  
  
## <a name="see-also"></a>Consulte también  
 [Clase SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
