---
title: MSSQLSERVER_3176 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3176 (Database Engine error)
ms.assetid: 4be24c64-2d52-4cb4-b4d7-36efbe4555b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a4117013b671ee9c5d5acf1fcde94ab382468dc4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914483"
---
# <a name="mssqlserver3176"></a>MSSQLSERVER_3176
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|3176|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LDDB_FILE_CLAIM|  
|Texto del mensaje|El archivo '%ls' fue reclamado por '%ls'(%d) y '%ls'(%d). Se puede utilizar la cláusula WITH MOVE para cambiar la ubicación de uno o más archivos.|  
  
## <a name="explanation"></a>Explicación  
 Se ha intentado utilizar un archivo para más de un propósito.  
  
### <a name="possible-causes"></a>Posibles causas  
 Otra base de datos ya está utilizando el nombre de archivo.  
  
## <a name="user-action"></a>Acción del usuario  
 Restaure los archivos de la base de datos en otra ubicación. En una instrucción RESTORE, utilice una cláusula WITH MOVE para mover cada archivo. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], cambie las ubicaciones de los archivos en la cuadrícula **Restaurar los archivos de base de datos como** del cuadro de diálogo **Opciones de Restaurar base de datos**.  
  
## <a name="see-also"></a>Vea también  
 [Restaurar una base de datos a una nueva ubicación &#40;SQL Server&#41;](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [Restaurar archivos en una nueva ubicación &#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
