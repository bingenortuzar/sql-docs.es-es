---
title: Contenido del dispositivo (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.bnrdevicecontents.f1
ms.assetid: 95e1902e-8c7a-4830-bdf9-1a6aca414a24
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ecddec60e1a0fd30d28bfae52a5fef29a6425fbf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068489"
---
# <a name="device-contents-sql-server"></a>Contenido del dispositivo (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice este cuadro de diálogo para ver la información de copia de seguridad. Esta información describe el dispositivo, el medio, el conjunto de medios y los conjuntos de copias de seguridad.  
  
 **Para utilizar SQL Server Management Studio a fin de ver el contenido de un dispositivo de copia de seguridad**  
  
-   [Ver el contenido de una cinta o un archivo de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opciones  
 **Multimedia**  
 Disco o conjunto de cintas donde se almacena la información de la copia de seguridad.  
  
 **Secuencia del medio**  
 Proporciona el número de secuencia del medio, el número de secuencia de la familia y el identificador del reflejo, si existe alguno. El medio físico de copia de seguridad se etiqueta con un número de secuencia que indica el orden en el que se utilizó el medio. El medio de copia de seguridad inicial se etiqueta con 1, el segundo (la primera cinta de continuación) se etiqueta con 2, y así sucesivamente. Cuando restaure el conjunto de copias de seguridad, asegúrese de que el operador que restaura la copia de seguridad coloca los medios correctos en el orden correcto.  
  
 **Creado el**  
 Muestra la fecha de los medios.  
  
 **Conjunto de medios**  
 Un conjunto de medios es una colección ordenada de medios de copia de seguridad en la que se han grabado una o más operaciones de copia de seguridad mediante un número constante de dispositivos pertinentes.  
  
 **Nombre**  
 Muestra el nombre del conjunto de medios.  
  
 **Descripción**  
 Muestra la descripción del conjunto de medios.  
  
 **Recuento de la familia de medios**  
 Muestra el recuento de la familia de medios. Cada conjunto de medios es una colección de una o más familias de medios. Toda la salida a un único dispositivo de copia de seguridad determinado (o grupo de dispositivos de copia de seguridad reflejados) forma una única familia de medios. Cada conjunto de medios contiene una familia de medios por dispositivo (o grupo de dispositivos reflejados); por ejemplo, si un conjunto de medios utiliza dos dispositivos de copia de seguridad no reflejados, el conjunto de medios contiene dos familias de medios.  
  
 **Conjuntos de copia de seguridad**  
 Muestra la información acerca del conjunto o conjuntos de copia de seguridad que contiene el medio. Un conjunto de copia de seguridad es el resultado de una operación de copia de seguridad correcta, cuyo contenido se distribuye entre los medios del conjunto de dispositivos de copia de seguridad.  
  
|Encabezado|Valores|  
|------------|------------|  
|**Nombre**|Nombre del conjunto de copia de seguridad.|  
|**Tipo**|Tipo de copia de seguridad realizada: Completa, Diferencial o Registro de transacciones.|  
|**Componente**|Componente del que se ha realizado una copia de seguridad: Base de datos, Archivo o en *\<blanco>* (para registros de transacciones).|  
|**Server**|Nombre de la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que realizó la operación de copia de seguridad.|  
|**Base de datos**|Nombre de la base de datos de la que se realizó la copia de seguridad.|  
|**Posición**|Posición del conjunto de copias de seguridad en el volumen.|  
|**Date**|Fecha y hora en la que finalizó la operación de copia de seguridad, presentadas en la configuración regional del cliente.|  
|**Tamaño**|Tamaño del conjunto de copias de seguridad, en bytes.|  
|**Nombre de usuario**|Nombre del usuario que realizó la operación de copia de seguridad.|  
|**Expiración**|Fecha y hora de expiración del conjunto de copias de seguridad.|  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
