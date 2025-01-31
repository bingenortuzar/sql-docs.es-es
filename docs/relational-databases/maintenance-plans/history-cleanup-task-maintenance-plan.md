---
title: Tarea Limpieza de historial (Plan de mantenimiento) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.historycleanup.f1
helpviewer_keywords:
- History Cleanup Task dialog box
ms.assetid: 66bb6c39-958c-4053-a27f-b1118d2567f5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.openlocfilehash: 37841e848aab5ff991741e5d460500834c9185e6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115793"
---
# <a name="history-cleanup-task-maintenance-plan"></a>Tarea Limpieza de historial (Plan de mantenimiento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice el cuadro de diálogo **Tarea Limpieza de historial** para descartar la antigua información histórica de las tablas de la base de datos msdb. Esta tarea admite la eliminación del historial de copias de seguridad y restauración, del historial de trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y del historial del plan de mantenimiento.  
  
 Esta instrucción usa las instrucciones **sp_purge_jobhistory** y **sp_delete_backuphistory** .  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Conexión**  
 Seleccione la conexión al servidor que va a utilizar para la realización de esta tarea.  
  
 **Nueva**  
 Cree una nueva conexión de servidor que utilizará al realizar esta tarea. El cuadro de diálogo **Nueva conexión** se describe posteriormente.  
  
 **Historial de copias de seguridad y restauración**  
 Conservar los registros de creación de las copias de seguridad recientes puede ser útil para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cree un plan de recuperación cuando desee restaurar una base de datos. El periodo de conservación debe tener, al menos, la frecuencia de las copias de seguridad completas de la base de datos.  
  
 **Historial de trabajos del Agente SQL Server**  
 Este historial puede ser útil para solucionar errores de los trabajos o para determinar las causas de las acciones de la base de datos.  
  
 **Historial del plan de mantenimiento**  
 Este historial puede ser útil para solucionar errores de los trabajos del plan de mantenimiento o para determinar las causas de las acciones de la base de datos.  
  
 **Quitar datos históricos anteriores a**  
 Especifique la antigüedad de los elementos que desea eliminar.  
  
 **Ver T-SQL**  
 Muestra las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] realizadas en el servidor para esta tarea, en función de las opciones seleccionadas.  
  
> [!NOTE]  
>  Si el número de objetos afectados es elevado, es posible que deba esperar un rato hasta que se muestren.  
  
## <a name="new-connection-dialog-box"></a>Cuadro de diálogo Nueva conexión  
 **Nombre de conexión**  
 Escriba un nombre para la nueva conexión.  
  
 **Seleccionar o especificar un nombre de servidor**  
 Seleccione un servidor al que conectarse cuando se realice esta tarea.  
  
 **Actualizar**  
 Actualiza la lista de servidores disponibles.  
  
 **Especificar información para iniciar sesión en el servidor**  
 Especifica el modo de autenticación en el servidor.  
  
 **Usar seguridad integrada de Windows NT**  
 Se conecta a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] de SQL Server con la autenticación de Microsoft Windows.  
  
 **Utilizar un nombre de usuario y una contraseña específicos**  
 Se conecta a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] de SQL Server utilizando la autenticación de SQL Server. Esta opción no está disponible.  
  
 **User name**  
 Proporcione un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la autenticación. Esta opción no está disponible.  
  
 **Contraseña**  
 Proporcione una contraseña para que se utilice en la autenticación. Esta opción no está disponible.  
  
## <a name="see-also"></a>Consulte también  
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [sp_delete_backuphistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)  
  
  
