---
title: IClientVirtualDeviceSet2::CreateEx
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IClientVirtualDeviceSet2::CreateEx.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 90165738dfcea8818353d602f72390bb08eea792
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847356"
---
# <a name="iclientvirtualdeviceset2createex-vdi"></a>IClientVirtualDeviceSet2::CreateEx (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La función **CreateEx** crea el conjunto de dispositivos virtuales.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IClientVirtualDeviceSet2::CreateEx (
   LPCWSTR         lpInstanceName,
   LPCWSTR         lpName,
   VDConfig*      pCfg
);
```

## <a name="parameters"></a>Parámetros

*lpInstanceName* Esta cadena identifica la instancia de SQL Server a la que se enviará el comando SQL.

*lpName* Identifica el conjunto de dispositivos virtuales. Deben seguirse las reglas para los nombres usados por CreateFileMapping(). Cualquier carácter excepto la barra diagonal inversa (puede usarse \)). Se trata de una cadena Unicode de caracteres anchos. Se recomienda agregar un prefijo a la cadena con nombre del producto o la compañía del usuario y el nombre de la base de datos.

*pCfg* Es la configuración del conjunto de dispositivos virtuales. Para más información, vea Configuración.

## <a name="return-value"></a>Valor devuelto

|Valor devuelto | Explicación |
|---|---|
| NOERROR | La función se ha realizado correctamente. |
| VD_E_NOTSUPPORTED | Uno o varios de los campos de la configuración no eran válidos o no se admiten. |
| VD_E_PROTOCOL | Se ha creado el conjunto de dispositivos virtuales. |

## <a name="remarks"></a>Notas

El método CreateEx solo se debe llamar una vez por operación BACKUP o RESTORE. Después de invocar el método Close, el cliente puede volver a usar la interfaz para crear otro conjunto de dispositivos virtuales.

El nombre de instancia debe identificar la instancia en la que se emite Transact-SQL. NULL identifica la instancia predeterminada. No se acepta el prefijo "machineName\".

Las llamadas a CreateEx (y Create) modificarán la DACL de seguridad en el identificador de proceso del proceso cliente. Por este motivo, cualquier otra modificación del identificador del proceso se debe serializar con la invocación de CreateEx. CreateEx se serializará con otras llamadas a CreateEx, pero no se puede serializar mediante procesamiento externo. Se concede acceso a la cuenta en la que se ejecuta el servicio de SQL Server.

El método CreateEx reemplaza al método Create definido en la instancia original de IClientVirtualDeviceSet. El método Create original está en desuso y no se debe usar en tareas de desarrollo futuras. El método Create original implementa una forma de compatibilidad con el nombre de instancia con la variable de entorno _VIRTUAL_SERVER_NAME_. Si esa variable se establece en el entorno, el método Create llama internamente a CreateEx, y pasa el valor de _VIRTUAL_SERVER_NAME_ como el nombre de la instancia.

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).