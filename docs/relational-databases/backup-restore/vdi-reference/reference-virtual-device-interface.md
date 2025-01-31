---
title: Referencia de interfaces de dispositivo virtual
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona información general sobre la referencia de las interfaces de dispositivo virtual para la copia de seguridad de SQL Server.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2b4556734044ad5bd688f8d5b286885450897b42
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847156"
---
# <a name="virtual-device-interface-vdi-reference"></a>Referencia de interfaces de dispositivo virtual (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta sección contiene las especificaciones para interfaces de programación de aplicaciones SQL Server diseñadas para su uso por parte de proveedores de software de copia de seguridad de terceros.

## <a name="overview"></a>Información general

La interfaz de dispositivo virtual (VDI) proporciona el mayor rendimiento de copias de seguridad en línea con una degradación mínima para la carga de trabajo de transacciones, así como los tiempos de restauración más rápidos posibles. Permite a los proveedores de terceros lograr las mismas características de rendimiento que la copia de seguridad o restauración nativas de SQL Server, y hace que toda la gama de funciones de copia de seguridad y restauración esté disponible. VDI se presentó en SQL Server 7.0 y se admite y mejora en las versiones posteriores.

VDI admite dos tipos principales de tecnologías de copia de seguridad:

- Copias de seguridad en línea convencionales en las que se lee todo el contenido del conjunto de copia de seguridad y se transfiere al medio de copia de seguridad.

- Copias de seguridad de instantáneas en las que se usa la tecnología subyacente de reflejo dividido o de copia en escritura.

Las copias de seguridad en línea convencionales realizadas a través de VDI pueden aprovechar toda la gama de características de copia de seguridad y restauración de SQL Server. Las copias de seguridad de instantáneas se limitan únicamente a las copias de seguridad completas y de archivos o grupos de archivos. Pero las copias de seguridad de instantáneas se pueden aplicar con copias de seguridad diferenciales de base de datos, de archivos y del registro de transacciones convencionales.

## <a name="next-steps"></a>Pasos siguientes

Revise la documentación de referencia de VDI de esta sección.

Descargue la especificación completa y los archivos de código fuente auxiliares:

[Especificación de la interfaz de dispositivo de copia de seguridad virtual (VDI) de SQL Server 2005](https://www.microsoft.com/download/details.aspx?id=17282)