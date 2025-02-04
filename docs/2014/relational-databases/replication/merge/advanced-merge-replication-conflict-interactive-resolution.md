---
title: Resolución interactiva de conflictos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- interactive conflict resolution [SQL Server replication]
- interactive resolver [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 172c60c7-f605-4eb5-b185-54ae9e9d3c60
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 43347190c53331d0a30ba0f29d795cce981eec34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245117"
---
# <a name="interactive-conflict-resolution"></a>Interactive Conflict Resolution
  La replicación de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona una Resolución interactiva que permite solucionar conflictos manualmente durante la sincronización a petición en el Administrador de sincronización de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. El Solucionador interactivo es una interfaz gráfica que se activa en tiempo de ejecución y muestra datos para cada fila en conflicto; ofrece opciones para ver y modificar los datos en conflicto y solucionar cada conflicto individualmente.  
  
 El Solucionador interactivo es similar al Visor de conflictos. Sin embargo, el Visor de conflictos muestra los resultados de los conflictos ya resueltos después de la sincronización de mezcla; el Solucionador interactivo muestra cada conflicto antes de la resolución, lo que permite determinar el resultado de cada conflicto durante la sincronización de mezcla. Debe haber una persona disponible para supervisar el Solucionador interactivo en el momento en que se produzca un conflicto.  
  
> [!NOTE]  
>  La Resolución interactiva requiere el Administrador de sincronización de Windows. Si se realiza una sincronización fuera del Administrador de sincronización de Windows (por ejemplo, una sincronización programada o una sincronización a petición en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o en el Monitor de replicación), los conflictos se resuelven automáticamente sin intervención del usuario, según la resolución especificada para el artículo. Los conflictos que implican registros lógicos no se muestran en el Solucionador interactivo. Para ver información acerca de estos conflictos, utilice procedimientos almacenados de replicación. Para obtener más información, consulte [Ver información de conflictos para publicaciones de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../view-conflict-information-for-merge-publications.md).  
  
## <a name="article-resolvers-and-the-interactive-resolver"></a>Solucionadores de artículos y el Solucionador interactivo  
 Los solucionadores de conflictos (ya sea el solucionador predeterminado, un controlador de lógica de negocios o un solucionador personalizado) se asignan a artículos específicos cuando se crea una publicación y utilizan un conjunto de reglas para determinar qué conjunto de datos debe utilizarse cuando se incluyen datos de filas en conflicto. El Solucionador interactivo no es un solucionador de conflictos independiente con reglas para determinar los ganadores y los perdedores de los conflictos, sino una herramienta que se utiliza junto con los solucionadores predeterminados y personalizados. El solucionador de artículos continúa determinando la fila ganadora y la perdedora, pero el Solucionador interactivo permite que intervenga el usuario para aceptar, rechazar o modificar los resultados.  
  
 Para utilizar el Solucionador interactivo, este debe estar habilitado para cada artículo y suscripción que lo necesite. Después de habilitarla para uno o varios artículos y suscripciones, el Solucionador interactivo se utiliza cuando se detectan conflictos durante la sincronización de mezcla.  
  
 Para usar la resolución interactiva, consulte [Especificar la resolución interactiva de conflictos para artículos de mezcla](..//publish/specify-merge-replication-properties.md#interactive-conflict-resolution) y [Sincronizar una suscripción mediante el Administrador de sincronización de Windows &#40;Administrador de sincronización de Windows&#41;](../synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
## <a name="see-also"></a>Vea también  
 [Replicación de mezcla avanzada: detección y resolución de conflictos](advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
