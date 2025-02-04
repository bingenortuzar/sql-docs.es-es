---
title: Validar la información de particiones para un suscriptor de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication data validation [SQL Server replication], partitions
- parameterized filters [SQL Server replication], validating partition information
- validating partition information
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3bada5fc49dc344510164260330699b60a3288cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63255311"
---
# <a name="validate-partition-information-for-a-merge-subscriber"></a>Validar la información de particiones para un suscriptor de mezcla
  Al definir un filtro de fila con parámetros para una publicación de combinación, se utiliza una función que hace referencia a la información del suscriptor, como el nombre de inicio de sesión del suscriptor. De manera predeterminada, la replicación valida la información del suscriptor basándose en esa función antes de cada sincronización y cada vez que se aplica una instantánea al suscriptor. El proceso de validación garantiza que los datos se dividan correctamente para cada suscriptor. El comportamiento de la validación se controla con la propiedad de publicación **validate_subscriber_info**, que se puede cambiar con [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) o en la página **Opciones de suscripción** del cuadro de diálogo **Propiedades de la publicación**. Para obtener más información acerca de cómo cambiar las propiedades de la publicación, vea [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
## <a name="how-partition-validation-works"></a>Cómo funciona la validación de particiones  
 Por ejemplo, cuando se filtra una publicación con la función **SUSER_SNAME()** , el Agente de mezcla aplica la instantánea inicial a cada suscriptor en función de datos que sean válidos para la expresión **SUSER_SNAME()** .  
  
 Si está habilitada la validación, cuando el suscriptor se vuelve a conectar al publicador para la siguiente sincronización, el Agente de mezcla valida la información en el suscriptor y garantiza que cada partición del suscriptor sea igual a la que se recibió en la instantánea inicial. En cada aplicación de mezcla o instantáneas posterior, el Agente de mezcla valida cada partición del suscriptor.  
  
 Si el Agente de mezcla detecta que la función utilizada en la expresión de filtro devuelve un valor distinto del que devolvía en la instantánea inicial, se producirá un error en la aplicación de mezcla o instantáneas, y es posible que sea necesario reinicializar esa suscripción en el suscriptor. La reinicialización puede ser necesaria para evitar problemas que pueden surgir si cambia la configuración de mezcla de un suscriptor, pero puede ser suficiente cambiar la información del suscriptor, como el nombre de inicio de sesión, al valor que tenía en el momento de la instantánea original.  
  
 Cuando el Agente de mezcla valida una partición, además de validarla por comparación con los valores devueltos por las funciones utilizadas en las expresiones de filtro, el agente también comprueba si la instantánea se generó antes que los cambios que la invalidan, como operaciones de limpieza de metadatos o cambios de esquema. Si una instantánea dividida es demasiado antigua, el Agente de mezcla devolverá un error y será necesario volver a generar una instantánea dividida para ese suscriptor, basándose en una instantánea normal actual.  
  
## <a name="see-also"></a>Vea también  
 [Preguntas más frecuentes para administradores de replicación](administration/frequently-asked-questions-for-replication-administrators.md)   
 [Best Practices for Replication Administration](administration/best-practices-for-replication-administration.md)   
 [Reinicializar suscripciones](reinitialize-subscriptions.md)   
 [Validar datos replicados](validate-data-at-the-subscriber.md)  
  
  
