---
title: Validar todas las suscripciones | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.allsubscriptions.f1
helpviewer_keywords:
- Validate All Subscriptions dialog box
ms.assetid: 32e31469-36e4-42d9-a57a-12388bfd229d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: fc99c6f1325fc5f3a5ba5e9a64fb25fcd81430f7
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769279"
---
# <a name="validate-all-subscriptions"></a>Validar todas las suscripciones
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Use el cuadro de diálogo **Validar todas las suscripciones** para especificar que todas las suscripciones a una publicación de combinación deben validarse la próxima vez que se ejecute el Agente de mezcla para cada suscripción. El resultado de la validación se muestra en el Monitor de replicación. Para más información, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
 También puede validar una sola suscripción si hace clic con el botón secundario en una suscripción en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y hace clic en **Validar suscripción**.  
  
## <a name="options"></a>Opciones  
 **Solo comprobar recuentos de filas**  
 Seleccione esta opción para validar si la tabla del suscriptor tiene el mismo número de filas que la tabla del publicador. Este método no valida si el contenido de las filas coincide. La validación del recuento de filas proporciona una idea sobre validación que puede ponerle al corriente de problemas con los datos.  
  
 **Comprobar los recuentos de filas y comparar las sumas de comprobación para comprobar los datos de las filas**  
 Además de llevar a cabo un recuento de filas en el publicador y en el suscriptor, se calcula una suma de comprobación de todos los datos utilizando el algoritmo binario de suma de comprobación. Si el número de filas da un error, no se lleva a cabo la suma de comprobación. Esta opción no es válida para [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Validar datos replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
