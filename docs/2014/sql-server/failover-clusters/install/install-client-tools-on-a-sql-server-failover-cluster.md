---
title: Instalar las herramientas de cliente en un clúster de conmutación por error de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 3c82d510-9798-46be-bebb-cac9bef56936
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69ca337b8b4ed4ab0e801cbb510ad533b4558448
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62657495"
---
# <a name="install-client-tools-on-a-sql-server-failover-cluster"></a>Instalar las herramientas de cliente en un clúster de conmutación por error de SQL Server
  Las herramientas de cliente tales como [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] son características compartidas comunes a todas las instancias del mismo equipo. Son compatibles con versiones anteriores, con versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admitidas que se pueden instalar en paralelo. Solo existe una versión de las herramientas de cliente en un nodo a la vez.  
  
 Si las herramientas de cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se instalan durante el proceso de instalación en el primer nodo del clúster de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , se agregarán automáticamente a los nodos que se puedan agregar más adelante a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando Agregar nodo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se agregan automáticamente a los nodos adicionales agregados al clúster de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando Agregar nodo. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se pueden instalar manualmente en los nodos en que desee que haya una copia local de los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Si no instala las herramientas de cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] durante la instalación inicial del clúster de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , puede instalarlas más adelante como se describe en los procedimientos siguientes.  
  
## <a name="installation-procedures"></a>Procedimientos de instalación  
  
#### <a name="installing-includessnoversionincludesssnoversion-mdmd-client-tools-using-the-setup-user-interface"></a>Instalar las Herramientas de cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando la interfaz de usuario del programa de instalación  
  
1.  Inserte el medio de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . En la carpeta de instalación raíz, haga doble clic en Setup.exe. Para realizar la instalación desde el recurso compartido de red, localice la carpeta raíz de dicho recurso y, a continuación, haga doble clic en Setup.exe.  
  
2.  En la página **Instalación**, haga clic en **Nueva instalación independiente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o agregar características a una instalación existente**. No haga clic en **Nueva instalación de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]** .  
  
3.  El comprobador de configuración del sistema comprueba el estado del sistema del equipo antes de seguir con la instalación.  
  
4.  En la página **Tipo de instalación**, haga clic en **Realizar una nueva instalación de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]** .  
  
5.  En la página **Selección de características** , seleccione las herramientas que desee instalar y siga realizando los pasos restantes del proceso de instalación.  
  
#### <a name="installing-includessnoversionincludesssnoversion-mdmd-client-tools-at-the-command-prompt"></a>Instalar las herramientas de cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando el símbolo del sistema  
  
1.  Para instalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las herramientas de cliente y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] los libros en línea, ejecute el siguiente comando: Setup.exe/q/Action=Install /Features=Tools  
  
2.  Para instalar sólo las opciones básicas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las herramientas de administración ejecutan el siguiente comando: Setup.exe/q/Action=Install Features = SSMS. De este modo se instalará la compatibilidad de [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] con [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)], [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)], la utilidad sqlcmd y el proveedor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell.  
  
3.  Para instalar la completa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] herramientas de administración, ejecute el siguiente comando: Setup.exe/q/Action=Install /Features=ADV_SSMS. Para obtener más información acerca de los valores de parámetro para las características, consulte [instalar SQL Server 2014 desde el símbolo del sistema](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
### <a name="uninstalling-includessnoversionincludesssnoversion-mdmd-client-tools"></a>Desinstalar las Herramientas de cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 Aparecen en Agregar o quitar programas en el Panel de control como **[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]** y se pueden quitar desde ahí. Si usa Quitar nodo para desinstalar una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del clúster de conmutación por error, los componentes cliente no se desinstalarán al mismo tiempo.  
  
## <a name="see-also"></a>Vea también  
 [Ver y leer los archivos de registro de instalación de SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
