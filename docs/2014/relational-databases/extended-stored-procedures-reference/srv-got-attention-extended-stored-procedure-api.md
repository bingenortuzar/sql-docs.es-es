---
title: srv_got_attention (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_got_attention
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_got_attention
ms.assetid: 805e68e1-d17f-41bd-8b9f-a27283bb6fbe
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1b2b13668c9402d947937b4cc7aeb581c253d6a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127297"
---
# <a name="srvgotattention-extended-stored-procedure-api"></a>srv_got_attention (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Comprueba si es necesario anular la conexión o tarea actual y devuelve TRUE si se cancela la conexión o se anula el lote.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL srv_got_attention  
(SRV_PROC *  
srvproc  
);  
  
```  
  
#### <a name="parameters"></a>Parámetros  
 *srvproc*  
 Puntero que identifica una conexión a la base de datos.  
  
## <a name="return-value"></a>Valor devuelto  
 TRUE si se cancela la conexión o se anula el lote. FALSE si la conexión o el lote están activos.  
  
## <a name="remarks"></a>Comentarios  
 Un procedimiento almacenado extendido de ejecución prolongada debe comprobar la atención del servidor al llamar periódicamente a **srv_got_attention** para que el procedimiento termine automáticamente cuando se cancele la conexión o se anule el lote.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/).  
  
  
