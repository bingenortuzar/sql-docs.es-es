---
title: REPLACENULL (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 70db7832-b5a0-4db5-a8ad-42ad8630d8e8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 335ccdfb3857ba7d32147424a46f76bc0ccdbe17
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71288421"
---
# <a name="replacenull-ssis-expression"></a>REPLACENULL (expresión SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Devuelve el valor del parámetro de la segunda expresión si el parámetro de la primera expresión es NULL; en caso contrario, devuelve el valor de la primera expresión.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
REPLACENULL(expression 1,expression 2)  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression 1*  
 El resultado de esta expresión se comprueba con NULL.  
  
 *expression 2*  
 El resultado de esta expresión se devuelve si la primera expresión se evalúa como NULL.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Notas  
  
-   La longitud de *expression 2* puede ser cero.  
  
-   REPLACENULL devuelve un resultado NULL si alguno de los argumentos es NULL.  
  
-   Las columnas de objetos binarios (DT_TEXT, DT_NTEXT, DT_IMAGE) no se admiten en ninguno de los dos parámetros.  
  
-   Se espera que las dos expresiones devuelvan el mismo tipo de valor devuelto. Si no es así, la función intenta convertir la segunda expresión al tipo de valor devuelto de la primera expresión, lo que puede producir un error si los tipos de datos son incompatibles.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 En el siguiente ejemplo se reemplaza cualquier valor NULL de una columna de base de datos con una cadena (1900-01-01). Esta función se utiliza especialmente en los patrones de columnas derivadas comunes en los casos en los que se desee reemplazar los valores NULL por algo más.  
  
```  
REPLACENULL(MyColumn, "1900-01-01")  
```  
  
> [!NOTE]
>  En el ejemplo siguiente se muestra cómo se realizó en [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]/ [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)].  
  
```  
(DT_DBTIMESTAMP) (ISNULL(MyColumn) ? "1900-01-01" : MyColumn)   
```  
  
  
