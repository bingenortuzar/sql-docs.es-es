---
title: Objeto Property (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Property object [ADOX]
ms.assetid: 6a56def6-dbe6-4ccc-a491-8d076889f019
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b7911608970e9860d7eddcf3e83156ac99645c3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965392"
---
# <a name="property-object-adox"></a>Objeto Property (ADOX)
Representa una característica de un objeto ADOX.  
  
## <a name="remarks"></a>Comentarios  
 Objetos ADOX tienen dos tipos de propiedades: integradas y dinámicas.  
  
 Las propiedades integradas son aquellas propiedades inmediatamente disponibles para cualquier objeto nuevo, utilizando la sintaxis MyObject.Property. No aparecen como objetos de propiedad en un objeto [colección de propiedades](../../../ado/reference/ado-api/properties-collection-ado.md), por lo que aunque se pueden cambiar sus valores, no se puede modificar sus características.  
  
 Propiedades dinámicas se definen mediante el proveedor de datos subyacente y aparecen en la colección de propiedades para el objeto ADOX apropiado.  Pueden hacer referencia a las propiedades dinámicas sólo a través de la colección, utilizando la sintaxis MyObject.Properties(0) o MyObject.Properties.  
  
 No se puede eliminar cualquier tipo de propiedad.  
  
 Un objeto dinámico de la propiedad tiene cuatro propiedades integradas de su propio:  
  
 El [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad es una cadena que identifica la propiedad.  
  
 El [tipo](../../../ado/reference/ado-api/type-property-ado.md) propiedad es un entero que especifica el tipo de datos de propiedad.  
  
 El [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad es una variante que contiene el valor de propiedad. Valor es la propiedad predeterminada para un objeto de propiedad.  
  
 El [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad es un valor long que indica características de la propiedad específica del proveedor.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Property (ADOX)](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)
