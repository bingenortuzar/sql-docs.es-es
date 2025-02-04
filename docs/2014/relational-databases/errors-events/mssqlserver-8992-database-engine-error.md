---
title: MSSQLSERVER_8992 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8992 (Database Engine error)
ms.assetid: 68467e6a-09d8-478f-8bd9-3bb09453ada3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ad75e136c4bef59f24b451b84f03e06d71a32ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912549"
---
# <a name="mssqlserver8992"></a>MSSQLSERVER_8992
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|8992|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC3_CHECK_CATALOG|  
|Texto del mensaje|Comprobación de catálogo mensaje ERROR nivel LEVEL estado STATE: MENSAJE.|  
  
## <a name="explanation"></a>Explicación  
 DBCC CHECKCATALOG o DBCC CHECKDB encontró una incoherencia en las tablas de metadatos de sistema para el objeto especificado. Es decir, hay una incoherencia entre el identificador de objeto registrado y el objeto especificado en el mensaje de error.  
  
 Este error se puede producir cuando una o más tablas del sistema se han actualizado manualmente de una manera que crea una incoherencia en los metadatos del sistema. Por ejemplo, un usuario puede haber eliminado de forma manual un objeto de la tabla **sysobjects** sin quitar las filas asociadas de otras tablas como **sysindexes** y **syscolumns**.  
  
 Este error se puede producir al ejecutar DBCC CHECKDB contra una base de datos actualizada de SQL Server 2000 a SQL Server 2005 o posterior. En SQL Server 2000, DBCC CHECKDB no incluía la funcionalidad de DBCC CHECKCATALOG, de modo que el error no se detectara antes de la actualización a menos que DBCC CHECKCATALOG se ejecutara específicamente contra la base de datos en SQL Server 2000.  
  
 Puede ver alguno de los errores siguientes junto con el error 8992:  
  
 Msg 3851 - Se encontró una fila no válida (%ls) en la tabla del sistema sys.%ls%ls.  
  
 Msg 3852 - La fila (%ls) de sys.%ls%ls no tiene una fila coincidente (%ls) en sys.%ls%ls.  
  
 3853 - El atributo (%ls) de la fila (%ls) de sys.%ls%ls no tiene una fila coincidente (%ls) en sys.%ls%ls.  
  
 3854 - El atributo (%ls) de la fila (%ls) de sys.%ls%ls tiene una fila coincidente (%ls) en sys.%ls%ls que no es válida.  
  
 3855 - El atributo (%ls) existe sin una fila (%ls) in sys.%ls%ls.  
  
 3856 - El atributo (%ls) existe (aunque no debería) para una fila (%ls) de sys.%ls%ls.  
  
 3857 - El atributo (%ls) requerido falta en una fila (%ls) de sys.%ls%ls.  
  
 3858 - El atributo (%ls) de la fila (%ls) de sys.%ls%ls tiene un valor no válido.  
  
## <a name="user-action"></a>Acción del usuario  
  
### <a name="drop-and-re-create-the-specified-object"></a>Quite y vuelva a crear el objeto especificado  
 Si es posible, quite y vuelva a crear el objeto especificado. Por ejemplo, si el objeto es un procedimiento almacenado o un tipo definido por el usuario, al volver a crearlo, puede que se resuelva el problema.  
  
### <a name="restore-from-backup"></a>Restaure mediante la copia de seguridad  
 Si el problema no está relacionado con el hardware y tiene una copia de seguridad limpia disponible, úsela para restaurar la base de datos. Esta acción solo es aplicable si la copia de seguridad no contiene el error de los metadatos.  
  
### <a name="export-the-data-to-a-new-database"></a>Exporte los datos a una nueva base de datos  
 Si la copia de seguridad también contiene la incoherencia de metadatos, debe crear una nueva base de datos y exportar el contenido de la base de datos existente a la nueva.  
  
### <a name="dbcc-checkdb-cannot-repair-this-error"></a>DBCC CHECKDB no puede reparar este error  
 Este error no se puede reparar.  Si no puede restaurar la base de datos a partir de una copia de seguridad, póngase en contacto con el servicio de soporte técnico y atención al cliente (CSS) de [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
### <a name="do-not-manually-update-system-tables"></a>No actualice manualmente las tablas del sistema  
 No realice actualizaciones manuales de las tablas del sistema. SQL Server no admite los cambios manuales en las bases de datos del sistema. Si actualiza una tabla del sistema de una base de datos de SQL Server, se registran dos eventos (identificadores de evento 17659 y 3859). Para obtener más información, vea el artículo 2688307 de KB, "Se registran los identificadores de evento 17659 y 3859 al actualizar tablas del sistema en una base de datos de SQL Server".  
  
## <a name="see-also"></a>Vea también  
 [Se registran los identificadores de evento 17659 y 3859 al actualizar tablas del sistema en una base de datos de SQL Server](https://support.microsoft.com/kb/2688307/EN-US)  
  
  
