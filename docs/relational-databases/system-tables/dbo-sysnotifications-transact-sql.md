---
title: dbo.sysnotifications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysnotifications_TSQL
- sysnotifications
- sysnotifications_TSQL
- dbo.sysnotifications
dev_langs:
- TSQL
helpviewer_keywords:
- sysnotifications system table
ms.assetid: c5150d18-e8b7-48a7-ada7-77c583af6e41
author: stevestein
ms.author: sstein
ms.openlocfilehash: ef7a5456f0bae470bcbf1f12f37843aa6c311d78
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984921"
---
# <a name="dbosysnotifications-transact-sql"></a>dbo.sysnotifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada notificación.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|Id. de la alerta.|  
|**operator_id**|**int**|Id. del operador al que se debe enviar la notificación.|  
|**notification_method**|**tinyint**|Método de notificación:<br /><br /> **1** = correo electrónico<br /><br /> **2** = buscapersonas<br /><br /> **4** = **netsend**<br /><br /> **7** = all|  
  
  
