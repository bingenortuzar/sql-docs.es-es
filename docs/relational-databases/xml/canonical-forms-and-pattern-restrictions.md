---
title: Formas canónicas y restricciones de patrón | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- pattern restrictions
- canonical forms
ms.assetid: 088314ec-7d0b-4a05-8a33-f35da5bfe59c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fcabc89e268e9ce5ed93211ccf89eed53e245c07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029349"
---
# <a name="canonical-forms-and-pattern-restrictions"></a>Formas canónicas y restricciones de patrón
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  La faceta de patrón XSD permite la restricción del espacio léxico de tipos simples. Cuando se aplica una restricción de patrón en un tipo para el cual existen varias representaciones léxicas posibles, algunos valores pueden provocar un comportamiento inesperado en el momento de la validación.  
  
 Este comportamiento se produce porque las representaciones léxicas de estos valores no se almacenan en la base de datos. Por tanto, los valores se convierten en sus representaciones canónicas cuando se serializan como salida. Si un documento contiene un valor cuya forma canónica no cumple la restricción de patrón de su tipo, el documento se rechaza si un usuario intenta volver a insertarlo.  
  
 Para evitar este problema, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rechazará los documentos XML que contengan valores que no se pueden volver a insertar, puesto que sus formas canónicas infringen las restricciones de patrón. Por ejemplo, el valor "33,000" no se valida con un tipo derivado de **xs:decimal** con una restricción de patrón de "33\\,0+". Aunque "33.000" cumple este patrón, la forma canónica, "33", no lo cumple.  
  
 Por ello, es preciso tener cuidado al aplicar facetas de patrón a los tipos derivados de los tipos primitivos siguientes: **boolean**, **decimal**, **float**, **double**, **dateTime**, **time**, **date**, **hexBinary**y **base64Binary**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra una advertencia si agrega alguno de esos componentes a una colección de esquemas.  
  
 La serialización imprecisa de valores de coma o punto flotante tiene un problema similar. Puesto que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]usa un algoritmo de serialización de coma flotante, los valores similares pueden compartir la misma forma canónica. Cuando se serializa un valor de coma flotante y a continuación se vuelve a insertar, puede que su valor cambie ligeramente. En casos excepcionales, puede obtenerse un valor que infrinja alguna de las siguientes facetas para este tipo en la reinserción: **enumeration**, **minInclusive**, **minExclusive**, **maxInclusive**o **maxExclusive**. Para evitarlo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rechaza los valores de tipos derivados de `xs:float` o `xs:double` que no se pueden serializar y volver a insertar.  
  
## <a name="see-also"></a>Consulte también  
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
