---
title: IServerVirtualDeviceSet2::RequestBuffers
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IServerVirtualDeviceSet2::RequestBuffers.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1b941f251c9093f10abbced8c3522f1719a1580e
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847186"
---
# <a name="iservervirtualdeviceset2requestbuffers-vdi"></a>IServerVirtualDeviceSet2::RequestBuffers (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La función **RequestBuffers** informa a VDI de que el servidor necesitará un número determinado de búferes con un requisito de tamaño y alineación determinado.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IServerVirtualDeviceSet2::RequestBuffers (
   DWORD   dwSize,
   DWORD   dwAlignment,
   DWORD   dwCount
);
```

## <a name="parameters"></a>Parámetros

*dwSize* Identifica el tamaño de cada búfer. Este tamaño solo debe incluir la región necesaria para los datos. VDI se encarga de los requisitos de alineación y prefijo.

*dwAlignment* La alineación necesaria para estos búferes. Se puede usar un valor más restrictivo que el valor de alineación básica especificado con "BeginConfiguration". Si el valor es 0, se establecerá de forma predeterminada en el valor de alineación básica.

*dwCount* El número de búferes que se solicitarán mediante "AllocateBuffer" con el tamaño y la alineación especificados.

## <a name="return-value"></a>Valor devuelto

|Valor devuelto | Explicación |
|---|---|
| NOERROR | La función se ha realizado correctamente. |
| VD_E_ABORT | Se solicitó Abort. |
| VD_E_PROTOCOL | El conjunto no se encuentra en un estado en el que se puedan declarar las asignaciones de búfer (vea la matriz de transición de estado). |
| VD_E_MEMORY | No se ha podido obtener la memoria solicitada. |

## <a name="remarks"></a>Notas

Este método se debe usar antes de que los búferes se asignen con AllocateBuffer. Los conjuntos de búferes con un tamaño y una alineación determinados se solicitan con RequestBuffers y, después, los búferes individuales se asignan con AllocateBuffer.

Durante la fase de configuración, las llamadas a RequestBuffers se "suman", de modo que en la llamada a EndConfiguration se puede usar una sola área de búfer (se asigna en ese momento). Una vez completada la configuración, cualquier llamada a RequestBuffers produce una asignación inmediata de más espacio en búfer.

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).