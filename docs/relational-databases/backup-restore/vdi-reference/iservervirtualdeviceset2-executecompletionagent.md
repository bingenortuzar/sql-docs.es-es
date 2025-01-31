---
title: IServerVirtualDeviceSet2::ExecuteCompletionAgent
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IServerVirtualDeviceSet2::ExecuteCompletionAgent.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2ad094794b5115aa4593f918de442798445e2b79
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847296"
---
# <a name="iservervirtualdeviceset2executecompletionagent-vdi"></a>IServerVirtualDeviceSet2::ExecuteCompletionAgent (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La función **ExecuteCompletionAgent** se usa para implementar el bucle principal del agente de finalización.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IServerVirtualDeviceSet2::ExecuteCompletionAgent ();
```

## <a name="return-value"></a>Valor devuelto

Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de NOERROR indica que la llamada al método se ha realizado correctamente. Un valor distinto de cero indica que se ha producido un error.

## <a name="remarks"></a>Notas

El agente de finalización proporciona un mecanismo a través del cual SQL Server se puede sincronizar con las finalizaciones de comandos del dispositivo virtual. Debe estar activo antes de que se puedan emitir comandos y debe permanecer activo hasta que se cierren todos los dispositivos.

Como es posible que SQL Server tenga que realizar una inicialización de subproceso especial, esta interfaz no inicia un nuevo subproceso de control. En su lugar, SQL Server configura un subproceso y, después, pasa el control a esta rutina. El subproceso se debe poder bloquear en los mecanismos de comunicación entre procesos (IPC) de Windows NT y ser capaz de llamar a cualquiera de las funciones de devolución de llamada que se proporcionan con los comandos enviados a través de IServerVirtualDevice::SendCommand.

Esta función no devolverá un valor hasta que se invoque IServerVirtualDeviceSet2::Close o SignalAbort.

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).