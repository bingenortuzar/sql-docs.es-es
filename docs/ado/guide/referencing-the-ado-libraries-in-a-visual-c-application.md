---
title: Hacer referencia a las bibliotecas de ADO en una aplicación de Visual C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual C++ application[ADO]
- ADO, libraries
ms.assetid: d3ea12ec-bca8-48c3-af57-ce14576108c9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 62fb1b89299af1f466e446c8adba422a841f0196
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923025"
---
# <a name="referencing-the-ado-libraries-in-a-visual-c-application"></a>Hacer referencia a las bibliotecas de ADO en una aplicación de Visual C++
Para usar la versión más reciente de ADO en una aplicación de Visual C++, use el siguiente `#import` directiva:  
  
```cpp
#import "msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
```  
  
 Para utilizar ADO MD o ADOX, debe importar *msadomd.dll* o *msadox.dll*, utilizando la sintaxis anterior.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 Para usar versiones anteriores de ADO, reemplace *msado15.dll* anteriormente con una de las siguientes bibliotecas de tipos.  
  
-   *msado27.tlb*, biblioteca de tipos de 2,7 ADO  
  
-   *msado26.tlb*, biblioteca de tipos de 2,6 ADO  
  
-   *msado25.tlb*, biblioteca de tipos de 2,5 ADO  
  
-   *MSADO21*, biblioteca de tipos 2.1 de ADO  
  
-   *msado20.tlb*, biblioteca de tipos 2.0 ADO
