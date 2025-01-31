---
title: Suplantación y seguridad de la integración de CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- impersonation [CLR integration]
- security [CLR integration]
- execution context [CLR integration]
- user impersonation [CLR integration]
- context [CLR integration]
ms.assetid: 1495a7af-2248-4cee-afdb-9269fb3a7774
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2c32691a065c2bfc43868d6b4105fbf1395a63ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781133"
---
# <a name="impersonation-and-clr-integration-security"></a>Suplantación y seguridad de la integración CLR
  Cuando el código administrado obtiene acceso a recursos externos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no suplanta automáticamente el contexto de ejecución actual en el que se ejecuta la rutina. El código de los ensamblados `EXTERNAL_ACCESS` y `UNSAFE` puede suplantar explícitamente el contexto de ejecución actual.  
  
> [!NOTE]  
>  Para obtener información sobre los cambios de comportamiento en la suplantación, vea [cambios recientes en las características del motor de base de datos de SQL Server 2014](../breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
 El proveedor de acceso a datos en proceso proporciona una interfaz de programación de aplicaciones, `SqlContext.WindowsIdentity`, que puede usarse para recuperar el token asociado al contexto de seguridad actual. El código administrado de los ensamblados `EXTERNAL_ACCESS` y `UNSAFE` puede usar este método para recuperar el contexto y usar el método `WindowsIdentity.Impersonate` de .NET Framework para suplantar ese contexto. Se aplican las siguientes restricciones a la suplantación explícita del código de usuario:  
  
-   No se permite el acceso a datos en proceso cuando el código administrado se encuentra en un estado suplantado. El código puede deshacer la suplantación y llamar al acceso a datos en proceso. Tenga en cuenta que esto requiere el almacenamiento del valor devuelto (un objeto `WindowsImpersonationContext`) por el método `Impersonate` original y una llamada al método `Undo` en este contexto `WindowsImpersonationContext`.  
  
     Esta restricción significa que, cuando se produce el acceso a datos en proceso, siempre se produce en el contexto de seguridad actual en vigor para la sesión. No puede modificarse mediante la suplantación explícita dentro del código administrado.  
  
-   En el caso del código administrado que se ejecuta de forma asincrónica (por ejemplo, a través de ensamblados `UNSAFE` que crean subprocesos y ejecutan código de forma asincrónica), no se permite nunca el acceso a datos en proceso. Esto es cierto haya o no haya suplantación.  
  
 Cuando el código se ejecuta en un contexto suplantado distinto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no puede realizar llamadas de acceso a datos en proceso; debe deshacer el contexto de suplantación para poder realizar llamadas de acceso a datos en proceso. Cuando el acceso a datos en proceso se realiza desde el código administrado, el contexto de ejecución original del punto de entrada [!INCLUDE[tsql](../../includes/tsql-md.md)] en el código administrado siempre se utiliza para la autorización.  
  
 Los ensamblados `EXTERNAL_ACCESS` y `UNSAFE` obtienen acceso a los recursos del sistema operativo con la cuenta de servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a menos que suplanten voluntariamente el contexto de seguridad actual tal y como se ha descrito anteriormente. Debido a ello, los autores de ensamblados `EXTERNAL_ACCESS` requieren un mayor nivel de confianza que los autores de ensamblados `SAFE`, que se especifica mediante el permiso de nivel de inicio de sesión `EXTERNAL ACCESS`. Solo debe concederse el permiso `EXTERNAL ACCESS` a los inicios de sesión en los que se confíe para ejecutar código con la cuenta del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de la integración CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Suplantación y credenciales para conexiones](../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
  
  
