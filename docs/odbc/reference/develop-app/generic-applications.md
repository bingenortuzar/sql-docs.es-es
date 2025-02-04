---
title: Aplicaciones genéricas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6b1544f5562468db03a649c263993039a722a3c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139296"
---
# <a name="generic-applications"></a>Aplicaciones genéricas
Aplicaciones genéricas en ocasiones, realizan una tarea codificado de forma rígida, como una hoja de cálculo de recuperación de datos de una base de datos. También es posible que realizan diversas tareas definidas por el usuario, como una aplicación de consultas genérico que permite al usuario escribir y ejecutar una instrucción SQL. ¿Qué aplicaciones genéricas tienen en común es que deben trabajar con una variedad de diferentes DBMS y que el desarrollador no conoce de antemano cuál será estos DBMS.  
  
 Por lo tanto, deben ser muy interoperable aplicaciones genéricas. El desarrollador debe realizar numerosas opciones, compensando la interoperabilidad de características y debe escribir código que espera que los controladores para admitir una amplia gama de funcionalidad. Mientras las aplicaciones genéricas se podrían optimizar para trabajar con DBMS conocidos, rara vez contienen código específico del controlador o específicos para DBMS.
