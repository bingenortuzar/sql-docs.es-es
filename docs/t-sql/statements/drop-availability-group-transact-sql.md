---
title: DROP AVAILABILITY GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_AVAILABILITY_GROUP_TSQL
- DROP AVAILABILITY GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], Transact-SQL statements
- DROP AVAILABILITY GROUP statement
- Availability Groups [SQL Server], dropping
ms.assetid: c1600289-c990-454a-b279-dba0ebd5d63e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 613841598b153dbe502f0267ed85197973bf706a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898293"
---
# <a name="drop-availability-group-transact-sql"></a>DROP AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Quita el grupo de disponibilidad especificado y todas sus réplicas. Si una instancia del servidor que hospeda una de las réplicas de disponibilidad está sin conexión al eliminar un grupo de disponibilidad, después de ponerse en línea, la instancia del servidor quitará la réplica de disponibilidad local. La acción de quitar un grupo de disponibilidad también elimina el agente de escucha del grupo de disponibilidad asociado, si hay alguno.  
  
> [!IMPORTANT]  
>  Si es posible, quite el grupo de disponibilidad solo mientras esté conectado a la instancia de servidor que hospeda la réplica principal. Cuando el grupo de disponibilidad se quita de la réplica principal, se permiten cambios en las bases de datos principales anteriores (sin protección de alta disponibilidad). Al eliminar un grupo de disponibilidad de una réplica secundaria, la réplica principal queda en el estado **RESTORING** y no se permiten cambios en las bases de datos.  
  
 Para obtener más información sobre formas alternativas de eliminar un grupo de disponibilidad, vea [Quitar un grupo de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP AVAILABILITY GROUP group_name   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *group_name*  
 Especifica el nombre del grupo de disponibilidad que se va a quitar.  
  
## <a name="limitations-and-recommendations"></a>Limitaciones y recomendaciones  
  
-   La ejecución de **DROP AVAILABILITY GROUP** requiere que la característica Grupos de disponibilidad AlwaysOn esté habilitada en la instancia de servidor. Para obtener más información, vea [Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   **DROP AVAILABILITY GROUP** no se puede ejecutar como parte de lotes o dentro de transacciones. Además, no se admiten expresiones ni variables.  
  
-   Puede quitar un grupo de disponibilidad de cualquier nodo de clústeres de conmutación por error de Windows Server (WSFC) que posea las credenciales de seguridad correctas para el grupo de disponibilidad. Esto permite eliminar un grupo de disponibilidad cuando ninguna de sus réplicas de disponibilidad permanece.  
  
    > [!IMPORTANT]  
    >  Evite quitar un grupo de disponibilidad cuando el clúster de Clústeres de conmutación por error de Windows Server (WSFC) no tiene quórum. Si debe quitar un grupo de disponibilidad mientras el clúster no tiene quórum, el grupo de disponibilidad de metadatos que se almacena en el clúster no se quita. Cuando el clúster recupere el quórum, necesitará volver a quitar el grupo de disponibilidad para quitarlo del clúster de WSFC.  
  
-   En una réplica secundaria, **DROP AVAILABILITY GROUP** solo se debe usar en caso de emergencia. Esto se debe a que al quitar un grupo de disponibilidad este se queda sin conexión. Si quita el grupo de disponibilidad de una réplica secundaria, la réplica principal no puede determinar si el estado **OFFLINE** se ha debido a la pérdida del quórum, a una conmutación por error forzada o a un comando **DROP AVAILABILITY GROUP**. La réplica principal cambia al estado **RESTORING** para evitar una posible situación de división de cerebro. Para más información, vea [Cómo funciona: DROP AVAILABILITY GROUP Behaviors](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Cómo funciona: comportamientos de DROP AVAILABILITY GROUP) (blog de los ingenieros de SQL Server de CSS).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Se requiere el permiso **ALTER AVAILABILITY GROUP** en el grupo de disponibilidad, el permiso **CONTROL AVAILABILITY GROUP**, el permiso **ALTER ANY AVAILABILITY GROUP** o el permiso **CONTROL SERVER**. Para quitar un grupo de disponibilidad que no se encuentre hospedado en la instancia del servidor local se necesita el permiso **CONTROL SERVER** o el permiso **CONTROL** en ese grupo de disponibilidad.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el grupo de disponibilidad `AccountsAG`.  
  
```  
DROP AVAILABILITY GROUP AccountsAG;  
```  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Cómo funciona: DROP AVAILABILITY GROUP Behaviors](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Cómo funciona: comportamientos de DROP AVAILABILITY GROUP) (blog de los ingenieros de SQL Server de CSS)  
  
## <a name="see-also"></a>Consulte también  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Quitar un grupo de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  
