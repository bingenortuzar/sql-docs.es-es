---
title: Cuadro de diálogo Guardar (no se permite) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.table.tablerecreatenosave.f1
ms.assetid: 7efda8e3-739f-4c97-a497-b8808a0acbea
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 84cfbc428c617126c3e895b4dafc65c816b386e0
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266893"
---
# <a name="save-not-permitted-dialog-box"></a>Guardar (no se permite), (cuadro de diálogo)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
El cuadro de diálogo **Guardar** (no se permite) advierte de que no se permite guardar cambios porque los cambios realizados requieren que se quiten y se vuelvan a crear las tablas enumeradas.  
  
Las acciones siguientes pueden requerir que se vuelva a crear una tabla:  
  
-   Agregar una nueva columna en la mitad de la tabla  
  
-   Quitar una columna  
  
-   Cambiar la nulabilidad de columnas  
  
-   Cambiar el orden de las columnas  
  
-   Cambiar el tipo de datos de una columna  
  
Cambiar esta opción, en el menú **Herramientas** , haga clic en **Opciones**, expanda **Diseñadores**y, a continuación, haga clic en **Diseñadores de tablas y bases de datos**. Active o desactive la casilla **Impedir guardar cambios que requieran volver a crear tablas** .  
  
