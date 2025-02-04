---
title: Gramática formal de forma | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91bdf0cfbfe87075d2c9484bca7edd835a950ee6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925347"
---
# <a name="formal-shape-grammar"></a>Gramática formal de forma
Se trata de la gramática formal para crear cualquier comando shape:  
  
-   Términos gramaticales necesarios son cadenas de texto delimitadas por corchetes angulares ("<>").  
  
-   Términos opcionales están delimitados por corchetes ("[]").  
  
-   Alternativas se indican mediante una barra diagonal ("&#124;").  
  
-   Repetición alternativas se indican mediante un botón de puntos suspensivos ("...").  
  
-   *Alfa* indica una cadena de letras en orden alfabético.  
  
-   *Dígito* indica una cadena de números.  
  
-   *Unicode-dígitos* indica una cadena de dígitos unicode.  
  
 Todos los demás términos son literales.  
  
|Término|Definición|  
|----------|----------------|  
|\<shape-command>|FORMA [\<tabla exp > [[AS] \<alias >]] [\<forma Acción >]|  
|\<table-exp>|{\<provider-command-text>} &#124;<br /><br /> (\<shape-command>) &#124;<br /><br /> TABLA \<quoted-name >&#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|ANEXAR \<lista de campos de un alias >&#124;<br /><br /> PROCESO \<lista de campos de un alias > [BY \<lista de campos >]|  
|\<aliased-field-list>|\<un alias de campo > [, \<un alias de campo... >]|  
|\<aliased-field>|\<campo: exp > [[AS] \<alias >]|  
|\<field-exp>|(\<relación exp >)&#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<tabla exp > [[AS] \<alias >]<br /><br /> RELACIONAR \<relación-cond-list >|  
|\<relación-cond-list >|\<relación cond > [, \<relación cond >...]|  
|\<relación cond >|\<nombre de campo > TO \<secundarios ref >|  
|\<child-ref>|\<field-name> &#124;<br /><br /> PARÁMETRO \<-ref param >|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM (\<nombre de campo completo >)&#124;<br /><br /> AVG(\<qualified-field-name>) &#124;<br /><br /> MIN(\<qualified-field-name>) &#124;<br /><br /> MAX(\<qualified-field-name>) &#124;<br /><br /> RECUENTO (\<calificado-alias > &#124; \<calificado-name >)&#124;<br /><br /> STDEV (\<nombre de campo completo >)&#124;<br /><br /> ANY(\<qualified-field-name>)|  
|\<calculated-exp>|CALC (\<expresión >)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<QUOTED-name > [[AS] \<alias >]|  
|\<quoted-name>|"\<string>" &#124;<br /><br /> '\<string>' &#124;<br /><br /> [\<string>] &#124;<br /><br /> \<name>|  
|\<qualified-name>|alias [.alias...]|  
|\<name>|alpha [ alpha &#124; digit &#124; _ &#124; # &#124; : &#124; ...]|  
|\<number>|dígito [dígitos...]|  
|\<new-exp>|NUEVO \<tipo de campo > [(\<número > [, \<número >])]|  
|\<field-type>|Un tipo de datos OLE DB o ADO.|  
|\<string>|-char Unicode [-char unicode...]|  
|\<expression>|Un objeto Visual expresión Basic para aplicaciones cuyos operandos son otras columnas no calculadas en la misma fila.|  
  
## <a name="see-also"></a>Vea también  
 [Acceso a las filas en un conjunto de registros jerárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Información general sobre la forma de datos](../../../ado/guide/data/data-shaping-overview.md)   
 [Proveedores deseados para dar forma a datos](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND Shape](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)   
 [Cláusula COMPUTE de forma](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic para las funciones de aplicaciones](../../../ado/guide/data/visual-basic-for-applications-functions.md)
