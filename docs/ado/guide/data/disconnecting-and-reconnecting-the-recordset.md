---
title: Desconectar y volver a conectar el conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9829ddfd7e625941c97bd3b2027c328a1fba93d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925511"
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>Desconectar y volver a conectar el conjunto de registros
Una de las características más eficaces de ADO es la capacidad de abrir un conjunto de registros de cliente desde un origen de datos y, a continuación, desconecte el conjunto de registros del origen de datos. Una vez que se ha desconectado el conjunto de registros, se puede cerrar la conexión al origen de datos, con lo que se liberan los recursos en el servidor utilizado para mantenerlo. Puede seguir ver y editar los datos del conjunto de registros mientras está desconectado y volver a conectarse al origen de datos y enviar las actualizaciones en modo por lotes.  
  
 Para desconectar un conjunto de registros, ábralo con una ubicación del cursor de adUseClient y, a continuación, establezca la propiedad ActiveConnection igual a Nothing. (Los usuarios de C++ deben establecer que ActiveConnection igual en NULL para desconectar).  
  
 Usaremos un conjunto de registros desconectado más adelante en esta sección cuando se hable de la persistencia de conjunto de registros para solucionar un escenario en el que se necesita para que los datos en un conjunto de registros disponible para una aplicación mientras el equipo cliente no está conectado a una red.  
  
## <a name="see-also"></a>Vea también  
 [Modo por lotes](../../../ado/guide/data/batch-mode.md)
