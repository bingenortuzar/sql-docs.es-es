---
title: Buscar en un documento activo de forma incremental | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- Query Editor [SQL Server Management Studio], incremental search
- incremental searches [SQL Server Management Studio]
ms.assetid: 490bb36c-dd43-4219-9e2a-ff27046b9395
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ce3f1265f33da943b7db2b3f951fd9aa6504f81
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063830"
---
# <a name="search-an-active-document-incrementally"></a>Buscar en un documento activo de forma incremental
  Es posible buscar en un único documento o ventana de forma incremental mediante la especificación de texto. La operación de búsqueda destaca el primer juego de caracteres que coincide con los especificados durante la búsqueda incremental en el documento o ventana. La búsqueda incremental busca automáticamente en todo el texto de un documento o ventana, excepto el texto oculto.  
  
 Con la opción **Coincidir mayúsculas y minúsculas** , la búsqueda incremental utiliza los criterios de la búsqueda anterior. Por ejemplo, si se ha buscado en varios archivos mediante el cuadro de diálogo **Buscar en archivos** y se ha activado **Coincidir mayúsculas y minúsculas**, si la siguiente vez se busca de forma incremental, la búsqueda distinguirá entre mayúsculas y minúsculas.  
  
### <a name="to-search-incrementally"></a>Para buscar de forma incremental  
  
1.  Abra el archivo o ventana en que desea realizar la búsqueda.  
  
2.  En el menú **Editar** , elija **Avanzado**y, a continuación, haga clic en **Búsqueda incremental**.  
  
     El cursor cambia a unos prismáticos con una flecha, que indica la dirección de la búsqueda, y la barra de estado muestra "Búsqueda incremental".  
  
3.  Comience a escribir la cadena de texto.  
  
     La barra de estado muestra el texto que se está escribiendo, mientras el editor resalta la primera repetición del texto. A medida que se continúa escribiendo, el editor pasa a la siguiente coincidencia y la resalta. Si no hay coincidencias, la barra de estado muestra lo siguiente.  
  
    ```  
    Incremental Search: <text> (not found)  
    ```  
  
 Las búsquedas incrementales se llevan a cabo desde la ubicación actual en el documento hacia abajo y de izquierda a derecha. Se pueden realizar mediante métodos abreviados de teclado.  
  
> [!NOTE]  
>  Para obtener una lista completa de las teclas de método abreviado, vea [Métodos abreviados de teclado de SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md).  
  
## <a name="see-also"></a>Vea también  
 [Buscar y reemplazar](search-and-replace.md)   
 [Buscar documentos de forma interactiva](search-documents-interactively.md)   
 [Buscar en documentos mediante las listas de resultados](search-documents-using-results-lists.md)   
 [Buscar texto con caracteres comodín](search-text-with-wildcards.md)   
 [Buscar texto mediante expresiones regulares](search-text-with-regular-expressions.md)  
  
  
