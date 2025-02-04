---
title: Buscar frases clave en documentos con la búsqueda semántica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], key phrase queries
ms.assetid: 6ee3676e-ed5d-43ec-aeca-1eed78967111
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cfb769db0de0e962c52d042e19134b849b3c1c3d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011346"
---
# <a name="find-key-phrases-in-documents-with-semantic-search"></a>Buscar frases clave en documentos con la búsqueda semántica
  Describe cómo buscar las frases clave en documentos o columnas de texto configurados para la indización semántica estadística.  
  
##  <a name="BasicsQueryKey"></a> Buscar frases clave en documentos  
  
###  <a name="howtofind"></a> Procedimientos para: Buscar las frases clave en documentos con SEMANTICKEYPHRASETABLE  
 Para identificar las frases clave de documentos específicos o para identificar documentos que contengan frases clave específicas, consulte la función [semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql).  
  
 SEMANTICKEYPHRASETABLE devuelve una tabla con cero, una o más filas para las frases clave asociadas con las columnas de la tabla especificada. Se puede hacer referencia a esta función de conjunto de filas en la cláusula FROM de una instrucción SELECT como si fuese un nombre de tabla normal.  
  
> [!NOTE]  
>  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], solo las palabras individuales se indizan para la búsqueda semánticas; las frases de múltiples palabras (ngrams) no se indizan. Además, las distintas formas de la misma palabra se indizan por separado; por ejemplo, "equipo" y "equipos" se indizan por independientemente.  
  
 Para obtener información detallada sobre los parámetros requeridos por la función SEMANTICKEYPHRASETABLE y sobre la tabla de resultados que devuelve, vea [semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql).  
  
> [!IMPORTANT]  
>  Las columnas de destino deben tener habilitada la indización de texto completo y semántica.  
  
###  <a name="HowToTopPhrases"></a> Ejemplo 1: Buscar las frases clave principales de un documento determinado  
 En el ejemplo siguiente se recuperan las 10 frases clave principales del documento especificado por la variable @DocumentId en la columna Document de la tabla Production.Document de la base de datos de ejemplo AdventureWorks. La variable @DocumentId representa un valor de la columna de clave del índice de texto completo.  
  
```sql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
GO  
```  
  
 La función **SEMANTICKEYPHRASETABLE** recupera estos resultados eficazmente mediante una búsqueda de índice en vez de un recorrido de tabla.  
  
###  <a name="HowToTopDocuments"></a> Ejemplo 2: Buscar los documentos principales que contienen una frase clave específica  
 En el ejemplo siguiente se recuperan los 25 primeros documentos que contengan la palabra clave "Bracket" de la columna Document de la tabla Production.Document de la base de datos de ejemplo AdventureWorks.  
  
```sql  
SELECT TOP (25) DOC_TBL.DocumentID, DOC_TBL.DocumentSummary  
FROM Production.Document AS DOC_TBL  
    INNER JOIN SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document  
    ) AS KEYP_TBL  
ON DOC_TBL.DocumentID = KEYP_TBL.document_key  
WHERE KEYP_TBL.keyphrase = 'Bracket'  
ORDER BY KEYP_TBL.Score DESC;  
GO  
```  
  
  
