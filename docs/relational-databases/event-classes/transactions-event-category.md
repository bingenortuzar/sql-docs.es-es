---
title: Transacciones (categoría de eventos) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Transactions event category
- event classes [SQL Server], Transactions event category
- Transactions event category [SQL Server]
ms.assetid: bfc75c5b-7115-49d8-9148-a0c84ee66a9a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5de24851562858eced26c7189fca5e786f395b94
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069652"
---
# <a name="transactions-event-category"></a>Transacciones (categoría de eventos)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Las clases de eventos **Transactions** se pueden utilizar para supervisar el estado de las transacciones. Los nombres de las clases de eventos prefijados con **TM:** se usan para realizar un seguimiento de las operaciones relacionadas con las transacciones enviadas desde la interfaz de administración de transacciones.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[DTCTransaction (clase de eventos)](../../relational-databases/event-classes/dtctransaction-event-class.md)|Realiza un seguimiento de las transacciones coordinadas por el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC). Se trata de transacciones distribuidas entre dos o más bases de datos o instancias del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[SQLTransaction (clase de eventos)](../../relational-databases/event-classes/sqltransaction-event-class.md)|Realiza un seguimiento de las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] BEGIN TRAN, COMMIT TRAN, SAVE TRAN y ROLLBACK TRAN.|  
|[TM: Begin Tran Completed, clase de eventos](../../relational-databases/event-classes/tm-begin-tran-completed-event-class.md)|Indica que se ha completado la solicitud BEGIN TRANSACTION.|  
|[TM: Begin Tran Starting, clase de eventos](../../relational-databases/event-classes/tm-begin-tran-starting-event-class.md)|Indica que se está iniciando la solicitud BEGIN TRANSACTION.|  
|[TM: Commit Tran Completed, clase de eventos](../../relational-databases/event-classes/tm-commit-tran-completed-event-class.md)|Indica que se ha completado la solicitud COMMIT TRANSACTION.|  
|[TM: Commit Tran Starting, clase de eventos](../../relational-databases/event-classes/tm-commit-tran-starting-event-class.md)|Indica que se está iniciando la solicitud COMMIT TRANSACTION.|  
|[TM: Promote Tran Completed, clase de eventos](../../relational-databases/event-classes/tm-promote-tran-completed-event-class.md)|Indica que se ha completado la solicitud PROMOTE TRANSACTION.|  
|[TM: Promote Tran Starting, clase de eventos](../../relational-databases/event-classes/tm-promote-tran-starting-event-class.md)|Indica que se está iniciando la solicitud PROMOTE TRANSACTION.|  
|[TM: Rollback Tran Completed, clase de eventos](../../relational-databases/event-classes/tm-rollback-tran-completed-event-class.md)|Indica que se ha completado la solicitud ROLLBACK TRANSACTION.|  
|[TM: Rollback Tran Starting, clase de eventos](../../relational-databases/event-classes/tm-rollback-tran-starting-event-class.md)|Indica que se está iniciando la solicitud ROLLBACK TRANSACTION.|  
|[TM: Save Tran Completed, clase de eventos](../../relational-databases/event-classes/tm-save-tran-completed-event-class.md)|Indica que se ha completado la solicitud SAVE TRANSACTION.|  
|[TM: Save Tran Starting, clase de eventos](../../relational-databases/event-classes/tm-save-tran-starting-event-class.md)|Indica que se está iniciando la solicitud SAVE TRANSACTION.|  
|[TransactionLog (clase de eventos)](../../relational-databases/event-classes/transactionlog-event-class.md)|Realiza un seguimiento cuando se escriben transacciones en el registro de transacciones de base de datos.|  
  
  
