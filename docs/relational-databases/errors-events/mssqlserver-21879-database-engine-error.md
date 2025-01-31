---
title: MSSQLSERVER_21879 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21879 (Database Engine error)
ms.assetid: fcfab735-05ca-423a-89f1-fdee7e2ed8c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7068229bcfcf63bb08fe46272cf308cee60be022
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056708"
---
# <a name="mssqlserver21879"></a>MSSQLSERVER_21879
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21879|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21879|  
|Texto del mensaje|No se puede consultar al servidor redireccionado "%s" para el publicador original "%s" y la base de datos del publicador "%s" para determinar el nombre del servidor remoto; error %d, mensaje de error "%s".|  
  
## <a name="explanation"></a>Explicación  
**sp_validate_redirected_publisher** usa un servidor vinculado temporal que crea para conectarse al publicador redirigido a fin de detectar el nombre del servidor remoto. Se devuelve el error 21879 si se produce un error en la consulta de servidor vinculado. La llamada para solicitar el nombre del servidor remoto normalmente es el primer uso del servidor vinculado temporal, por lo que si hay problemas de conectividad es probable que aparezcan primero con esta llamada. Esta llamada remota simplemente ejecuta SELECT **@@servername** en el servidor remoto.  
  
El servidor vinculado que se usa para consultar al publicador redirigido usa el modo de seguridad, el inicio de sesión y la contraseña suministrados cuando se llamó a **sp_adddistpublisher** para el publicador original.  
  
-   Si se usó la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (modo 0 de seguridad), se usan el inicio de sesión y la contraseña especificados para conectarse al servidor remoto.  
  
-   Si se usó la autenticación de Windows (modo de seguridad 1), se usa una conexión de confianza para la conexión.  
  
    -   Si un usuario llama a **sp_validate_redirected_publisher** de forma explícita, se usa el inicio de sesión de Windows en el que se ejecuta el usuario para la conexión.  
  
    -   Si un agente de replicación llama a **sp_validate_redirected_** publisher desde **sp_get_redirected_publisher**, se usa el inicio de sesión de Windows asociado al agente.  
  
El error 21879 puede indicar que se llamó a **sp_validate_redirected_publisher** con un inicio de sesión desconocido en el publicador de destino redirigido.  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe que el inicio de sesión de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el inicio de sesión de autenticación de Windows es válido en todas las réplicas de grupo de disponibilidad y que tiene suficiente autenticación para obtener acceso a las tablas de metadatos de suscripciones (syssubscriptions y sysmergesubscriptions) en la base de datos del publicador.  
  
Existen consideraciones especiales en caso de que se devuelva el error 21879 desde una llamada a **sp_get_redirected_publisher** iniciada por un agente de replicación ejecutado en un nodo distinto del distribuidor, como un agente de mezcla que se ejecute en un suscriptor. Si se usa la autenticación de Windows para la conexión al publicador redirigido, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se debe configurar para la autenticación Kerberos a fin de que la conexión se establezca correctamente. Cuando se usa la autenticación de Windows y no se configura [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la autenticación Kerberos, un agente de mezcla que se ejecute en el suscriptor recibe el error 18456 que indica que se produjo un error en el inicio de sesión de "NT AUTHORITY\ANONYMOUS LOGON". Hay tres formas posibles de solucionar este problema:  
  
-   Configure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la autenticación Kerberos. Vea **Utilizar la autenticación Kerberos con SQL Server** en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Use **sp_changedistpublisher** para cambiar el modo de seguridad asociado al publicador original de MSdistpublishers, además de para especificar un inicio de sesión y una contraseña que se usarán para la conexión.  
  
-   Especifique el parámetro de la línea de comandos *BypassPublisherValidation* en la línea de comandos del agente de mezcla para omitir la validación cuando se llama a **sp_get_redirected_publisher** en el distribuidor.  
  
