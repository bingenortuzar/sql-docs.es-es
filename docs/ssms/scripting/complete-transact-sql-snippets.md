---
title: Completar fragmentos de código de Transact-SQL| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], completing snippets
- snippets [Transact-SQL], completing
- Transact-SQL snippets, completing
ms.assetid: a8316a58-bb57-485e-845f-84c23360314c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 29dd60e3cbd1591920a042a5e5d5d83ed1151a53
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68256507"
---
# <a name="complete-transact-sql-snippets"></a>Completar fragmentos de código de Transact-SQL
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Una vez insertado un fragmento de código de [!INCLUDE[tsql](../../includes/tsql-md.md)] en un script, debe modificar el contenido del fragmento para generar una instrucción completa de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
## <a name="completing-snippets"></a>Completar fragmentos de código  
 Cuando se agrega un fragmento de [!INCLUDE[tsql](../../includes/tsql-md.md)] al script, la instrucción insertada del fragmento contiene uno o más puntos de reemplazo, que aparecen resaltados. Si coloca el puntero del mouse sobre un punto de reemplazo, aparece una información sobre herramientas con una descripción del elemento de la sintaxis que se puede especificar. El Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] reconoce el fragmento como parte independiente del resto del script hasta el momento de cerrar el archivo de origen. Los puntos de reemplazo permanecen activos hasta que se cierra el archivo de origen.  
  
 También puede agregar elementos adicionales de la sintaxis al código de la plantilla insertado por un fragmento de código. Por ejemplo, la plantilla del fragmento de creación de tabla genera dos definiciones de columna; usted deberá agregar definiciones de columna adicionales para crear una tabla con más de dos columnas.  
  
#### <a name="completing-the-snippet-statement"></a>Completar la instrucción del fragmento de código  
  
1.  Utilice la tecla TAB para desplazarse desde un punto de reemplazo hasta el siguiente. Utilice MAYÚS+TAB para desplazarse hasta el punto de reemplazo anterior.  
  
2.  Haga clic en CTRL+Barra espaciadora para invocar IntelliSense.  
  
3.  Seleccione un elemento de la lista o escriba un punto de reemplazo de su elección.  
  
## <a name="see-also"></a>Consulte también  
 [Insertar fragmentos de código de Transact-SQL](../../relational-databases/scripting/insert-transact-sql-snippets.md)   
 [Insertar fragmentos de código de Transact-SQL para rodear](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  
