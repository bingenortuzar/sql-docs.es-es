---
title: Otras anotaciones (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- url-encode annotation
- sql:key-fields
- use-cdata annotation
- sql:is-mapping-schema
- sql:url-encode
- sql:id-prefix
- sql:use-cdata
- key-fields annotation
- id-prefix annotation [SQLXML]
- is-mapping-schema annotation
ms.assetid: f7b4d37b-d6d3-4ac3-b2fd-a0b534a924e4
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a9a965ee5772ea3c2855a08d838c1d89da343e9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066862"
---
# <a name="annotation-interpretation---other-annotations"></a>Interpretación de anotaciones: otras anotaciones
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Además de las anotaciones descritas en los temas anteriores de esta sección, la carga masiva de XML interpreta estas otras anotaciones del modo siguiente:  
  
 **sql:id-prefix**  
 Si el esquema especifica prefijos para los datos XML, la carga masiva de XML quita los prefijos antes de enviar los datos a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **sql:use-cdata**  
 La carga masiva de XML lee el texto que está almacenado en las secciones CDATA y lo envía a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **sql:url-encode**  
 La carga masiva de XML no admite esta anotación. Por ejemplo, no puede especificar una dirección URL en la entrada de datos XML y esperar que la carga masiva de XML lea los datos de esa ubicación para almacenarlos en la base de datos.  
  
 **sql:is-mapping-schema**  
 La carga masiva de XML no admite esta anotación, ni tampoco admite **sql:id**.  
  
> [!NOTE]  
>  La carga masiva de XML no admite los esquemas de asignación insertados.  
  
 **sql:key-fields**  
 La carga masiva de XML omite siempre esta anotación.  
  
## <a name="see-also"></a>Vea también  
 [Interpretación de anotaciones &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sqlxml-4-0.md)  
  
  
