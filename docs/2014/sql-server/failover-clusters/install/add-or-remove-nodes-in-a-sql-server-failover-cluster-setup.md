---
title: Agregar o quitar nodos en un clúster de conmutación por error de SQL Server (programa de instalación) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- adding nodes
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- failover clustering [SQL Server], nodes
- deleting nodes
- cluster maintenance [SQL Server]
- removing nodes
ms.assetid: fe20dca9-a4c1-4d32-813d-42f1782dfdd3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1b6298020c1aa39f2c5c319efa492f6832c301f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63190283"
---
# <a name="add-or-remove-nodes-in-a-sql-server-failover-cluster-setup"></a>Agregar o quitar nodos en un clúster de conmutación por error de SQL Server (programa de instalación)
  Use este procedimiento para administrar los nodos de una instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existente.  
  
 Para actualizar o quitar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , es preciso ser administrador local con derecho de iniciar sesión como servicio en todos los nodos del clúster de conmutación por error. En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.  
  
 Para agregar un nodo a un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existente, debe ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el nodo que se va a agregar a la instancia del clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . No ejecute el programa de instalación en el nodo activo.  
  
 Para quitar un nodo de un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existente, debe ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el nodo que se va a quitar desde la instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Si desea ver los pasos del procedimiento para agregar o quitar nodos, seleccione una de las operaciones siguientes:  
  
-   [Agregar un nodo a un clúster de conmutación por error de SQL Server existente](#Add)  
  
-   [Quitar un nodo de un clúster de conmutación por error de SQL Server existente](#Remove)  
  
> [!IMPORTANT]  
>  La letra de unidad del sistema operativo de las ubicaciones de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debe coincidir en todos los nodos agregados al clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
##  <a name="Add"></a> Agregar nodo  
  
#### <a name="to-add-a-node-to-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>Para agregar un nodo a un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existente  
  
1.  Inserte el disco de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y, en la carpeta raíz, haga doble clic en Setup.exe. Para realizar la instalación desde un recurso compartido de red, navegue hasta la carpeta raíz de dicho recurso y, a continuación, haga doble clic en Setup.exe.  
  
2.  El Asistente para la instalación iniciará el Centro de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para agregar un nodo a una instancia en clúster de conmutación por error existente, haga clic en **Instalación** en el panel izquierdo. Luego, seleccione **Agregar nodo a clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]** .  
  
3.  El Comprobador de configuración del sistema ejecutará una operación de detección en su equipo. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
4.  En la página Selección de idioma, puede especificar el idioma para su instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] si va a realizar la instalación en un sistema operativo localizado y el medio de instalación incluye paquetes de idioma en inglés y en el idioma correspondiente al sistema operativo. Para obtener más información sobre la compatibilidad entre idiomas y las consideraciones sobre la instalación, vea [Versiones de idioma local en SQL Server](../../install/local-language-versions-in-sql-server.md).  
  
     Para continuar, haga clic en **Siguiente**.  
  
5.  En la página Clave del producto, especifique la clave de PID para una versión de producción del producto. Tenga en cuenta que la clave del producto que especifique para esta instalación debe ser para la misma edición de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que la que se encuentra instalada en el nodo activo.  
  
6.  En la página Términos de licencia, lea el contrato de licencia y active la casilla para aceptar los términos y condiciones de la licencia. Para ayudar a mejorar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], también puede habilitar la opción de uso de características y enviar informes a [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Para continuar, haga clic en **Siguiente**. Para salir del programa de instalación, haga clic en **Cancelar**.  
  
7.  El Comprobador de configuración del sistema comprobará el estado del sistema de su equipo antes de seguir con la instalación. Cuando se haya completado la comprobación, haga clic en **Siguiente** para continuar.  
  
8.  En la página Configuración de nodo de clúster, use la lista desplegable para especificar el nombre de la instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se modificará durante esta operación de instalación.  
  
9. En la página Configuración del servidor - Cuentas de servicio, especifique las cuentas de inicio de sesión para los servicios de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los servicios reales que se configuran en esta página dependen de las características que se van a instalar. En las instalaciones de clúster de conmutación por error, la información de nombre de cuenta y tipo de inicio se rellenará automáticamente en esta página en función de la configuración proporcionada para el nodo activo. Debe proporcionar contraseñas para cada cuenta. Para obtener más información, vea [Configuración del servidor - Cuentas de servicio](../../install/server-configuration-service-accounts.md) y [Configurar los permisos y las cuentas de servicio de Windows](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     **Nota de seguridad** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     Cuando termine de especificar la información de inicio de sesión para los servicios de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , haga clic en **Siguiente**.  
  
10. En la página Informes, especifique la información que le gustaría enviar a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] para mejorar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. De forma predeterminada, se habilita la opción de informe de errores.  
  
11. El Comprobador de configuración del sistema ejecutará uno o varios conjuntos de reglas para validar la configuración del equipo con las características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que ha especificado.  
  
12. La página Listo para agregar nodo muestra una vista de árbol de las opciones de instalación que se especificaron durante la instalación.  
  
13. La página Progreso de adición de nodo muestra el estado para que pueda supervisar el progreso de la instalación durante la ejecución del programa de instalación.  
  
14. Después de la instalación, la página Operación completada proporciona un vínculo al archivo de registro de resumen para la instalación y otras notas importantes. Para completar el proceso de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , haga clic en **Cerrar**.  
  
15. Si el programa indica que se reinicie el equipo, hágalo ahora. Es importante leer el mensaje del Asistente para la instalación tras completar el programa de instalación. Para obtener más información sobre los archivos de registro de instalación, vea [Ver y leer los archivos de registro de instalación de SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
##  <a name="Remove"></a> Quitar nodo  
  
#### <a name="to-remove-a-node-from-an-existing-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>Para quitar un nodo de un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existente  
  
1.  Inserte el medio de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . En la carpeta raíz, haga doble clic en setup.exe. Para realizar la instalación desde un recurso compartido de red, navegue hasta la carpeta raíz de dicho recurso y, a continuación, haga doble clic en Setup.exe.  
  
2.  El Asistente para la instalación inicia el Centro de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para quitar un nodo de una instancia en clúster de conmutación por error existente, haga clic en **Mantenimiento** en el panel izquierdo y, después, seleccione **Eliminar nodo de un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]** .  
  
3.  El Comprobador de configuración del sistema ejecutará una operación de detección en su equipo. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
4.  Después de hacer clic en la opción de instalación en la página Archivos auxiliares del programa de instalación, el Comprobador de configuración del sistema verificará el estado del equipo antes de continuar con la instalación. Cuando se haya completado la comprobación, haga clic en **Siguiente** para continuar.  
  
5.  En la página Configuración de nodo de clúster, use la lista desplegable para especificar el nombre de la instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se va a modificar durante esta operación de instalación. El nodo que se va a quitar aparece en el campo **Nombre de este nodo** .  
  
6.  La página Listo para quitar nodo muestra una vista de árbol de las opciones que se especificaron durante la instalación. Para continuar, haga clic en **Quitar**.  
  
7.  Durante la operación de eliminación, la página Progreso de eliminación de nodo muestra el estado.  
  
8.  La página Operación completada proporciona un vínculo al archivo de registro de resumen de la operación de eliminación de nodo y otras notas importantes. Para completar la eliminación del nodo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , haga clic en **Cerrar**. Para obtener más información sobre los archivos de registro de instalación, vea [Ver y leer los archivos de registro de instalación de SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="see-also"></a>Vea también  
 [Ver y leer los archivos de registro de instalación de SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
