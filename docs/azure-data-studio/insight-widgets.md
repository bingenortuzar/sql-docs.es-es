---
title: Empleo de widgets de información en Azure Data Studio para supervisar servidores y bases de datos
titleSuffix: Azure Data Studio
description: Obtenga información sobre los widgets de información en Azure Data Studio.
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
ms.openlocfilehash: c1ab90efa97878676b1adc2a62579527407d6ba6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959524"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-includename-sosincludesname-sos-shortmd"></a>Administración de servidores y bases de datos con widgets de información en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Los widgets de información toman las consultas de Transact-SQL (T-SQL) que se usan para supervisar los servidores y las bases de datos y las convierten en visualizaciones llenas de información.

La información adopta la forma de gráficos personalizables que se agregan a los paneles de supervisión de servidores y bases de datos. Vea información rápida de los servidores y las bases de datos, profundice en más detalles e inicie las acciones de administración que defina.

Puede compilar espectaculares paneles de administración de servidores y bases de datos de forma similar al ejemplo siguiente:

![Panel de base de datos](media/insight-widgets/database-dashboard.png)


Para lanzarse y comenzar a crear distintos tipos de widgets de información, vea los siguientes tutoriales:

- [Compilación de un widget de información personalizada](tutorial-build-custom-insight-sql-server.md)
- *Habilitación de widgets de información integrados*
  - [Habilitación de la información de supervisión de rendimiento](tutorial-qds-sql-server.md)
  - [Habilitación de la información de uso de espacio de tabla](tutorial-table-space-sql-server.md)


## <a name="sql-queries"></a>Consultas SQL

[!INCLUDE[name-sos](../includes/name-sos-short.md)] intenta evitar la incorporación de otro lenguaje u otra interfaz de usuario pesada, así que intenta usar T-SQL lo máximo posible con una configuración de JSON mínima. La configuración de widgets de información con T-SQL aprovecha el incontable número de orígenes existentes de consultas de T-SQL útiles que se pueden convertir en widgets llenos de información.

Los widgets de información se componen de una o dos consultas de T-SQL:
* La *consulta de widget de información* es obligatoria y es la que devuelve los datos que aparecen en el widget.
* La *consulta de detalles de información* solo es necesaria si se va a crear una página de detalles de información.

Una consulta de widget de información define un conjunto de datos que representa un recuento o un gráfico. La consulta de detalles de información se usa para presentar información de detalles relevante en formato tabular en el panel de detalles de información. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] ejecuta consultas de widget de información y asigna el conjunto de resultados de la consulta al conjunto de datos de un gráfico que luego representa. Cuando los usuarios abren los detalles de la información, se ejecuta la consulta de detalles de información y se imprime el resultado en una vista de cuadrícula en el cuadro de diálogo.

La idea básica es escribir una consulta de T-SQL de forma que se pueda usar como conjunto de datos de un recuento, un gráfico y un widget gráfico. 

## <a name="summary"></a>Resumen

La consulta de T-SQL y su conjunto de resultados determinan el comportamiento del widget de información. La escritura de una consulta para un tipo de gráfico o la asignación de un tipo de gráfico adecuado para una consulta existente es la consideración clave para compilar un widget de información eficaz.



## <a name="additional-resources"></a>Recursos adicionales
- [Editor de consultas](tutorial-sql-editor.md)

