---
title: Detección de truncamiento de datos habilitada con ExtendedAnsiSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d7fb67171a796755bf8d6229b9d562f69bd588ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096507"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Habilita la detección de truncamiento de datos utilizando ExtendedAnsiSQL
Cuando se activa la marca ExtendedAnsiSQL y la aplicación consiste en Insertar datos en un carácter o una columna binaria y se truncan los datos, se detectará el truncamiento. Cuando la marca ExtendedAnsiSQL está desactivada, los datos se truncan sin advertencia, como sucedía en versiones anteriores de los controladores de base de datos de escritorio de ODBC.
