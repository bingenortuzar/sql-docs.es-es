---
title: MSSQLSERVER_3151 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 068f4737a3367acdd01862cc800a4255a472c843
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001910"
---
# <a name="mssqlserver3151"></a>MSSQLSERVER_3151
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3151|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LDDB_MASTER_LOAD_FAILED|  
|Texto del mensaje|No se pudo restaurar la base de datos maestra. Cerrando SQL Server. Compruebe los registros de errores y vuelva a generar la base de datos maestra. Para obtener más información acerca de cómo volver a crear la base de datos maestra, vea los Libros en pantalla de SQL Server.|  
  
## <a name="explanation"></a>Explicación  
Se trata de un mensaje de error general que indica diversos problemas con la base de datos **maestra**.  
  
## <a name="user-action"></a>Acción del usuario  
Consulte los registros de errores para obtener más información. Para crear una base de datos **maestra** utilizable, ejecute Setup.exe con la opción REBUILDDATABASE. Para obtener más información, vea "Procedimientos: Instalar SQL Server desde el símbolo del sistema" en los Libros en pantalla de SQL Server.  
  
