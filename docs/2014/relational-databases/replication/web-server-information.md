---
title: Información del servidor web | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.webserverinformation.f1
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5f5c2385b4c58447db008544124ae9048566958
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199944"
---
# <a name="web-server-information"></a>Información del servidor web
  Para usar la opción de sincronización web en la replicación de mezcla se necesita la información del servidor web. Para más información sobre cómo configurar la sincronización web, vea [Configurar la sincronización web](configure-web-synchronization.md).  
  
## <a name="options"></a>Opciones  
 **Dirección del servidor web**  
 Si se especifica una dirección de servidor web en la página **Instantánea FTP e Internet** del cuadro de diálogo **Propiedades de la publicación**, aparecerá en este cuadro de texto de forma predeterminada. Puede aceptar la dirección predeterminada o escribir una dirección completa de servidor web para el servidor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) que sincroniza la suscripción.  
  
 **¿Cómo se conectarán los suscriptores al servidor web?**  
 Especifique el tipo de autenticación usado para conectar con el servidor web. Se recomienda usar Autenticación básica para las conexiones con el servidor IIS junto con SSL (Capa de sockets seguros). Si selecciona Autenticación básica, escriba el nombre de inicio de sesión y la contraseña para conectar desde el suscriptor con el servidor IIS.  
  
## <a name="see-also"></a>Vea también  
 [Crear una suscripción de extracción](create-a-pull-subscription.md)   
 [Ver y modificar las propiedades de una suscripción de extracción](view-and-modify-pull-subscription-properties.md)   
 [Suscriptores que no son de SQL Server](non-sql/non-sql-server-subscribers.md)   
 [Suscribirse a publicaciones](subscribe-to-publications.md)   
 [Sincronización web para la replicación de mezcla](web-synchronization-for-merge-replication.md)  
  
  
