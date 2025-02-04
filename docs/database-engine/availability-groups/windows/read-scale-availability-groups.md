---
title: Uso de escalado de lectura con grupos de disponibilidad
description: 'Una descripción de cómo conseguir el escalado de lectura cuando se usan grupos de disponibilidad Always On. '
ms.custom: seodec18
ms.date: 10/24/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: ''
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: edf98113b435cafd9f6552643e6a8a1ba4316982
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014458"
---
# <a name="use-read-scale-with-always-on-availability-groups"></a>Uso de escalado de lectura con grupos de disponibilidad Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Un grupo de disponibilidad es una solución integral que ofrece funcionalidades de alta disponibilidad para SQL Server, así como soluciones de escalado integradas. En una aplicación de base de datos típica, varios clientes ejecutan varios tipos de cargas de trabajo. En ocasiones, se pueden desarrollar cuellos de botella debido a las restricciones de recursos. Puede liberar recursos y así lograr un mayor rendimiento de la carga de trabajo de OLTP. También puede proporcionar mayor rendimiento y escalabilidad en las cargas de trabajo de solo lectura. Aproveche la tecnología de replicación más rápida de SQL Server y cree un grupo de bases de datos replicadas para descargar cargas de trabajo de informes y análisis en réplicas de solo lectura.

Con los grupos de disponibilidad, se pueden configurar una o varias réplicas secundarias para admitir el acceso de solo lectura a las bases de datos secundarias.

Las aplicaciones cliente que ejecutan cargas de trabajo de informes o análisis pueden conectarse directamente a las bases de datos secundarias. También puede configurar una lista de enrutamiento de solo lectura y conectarse a la base de datos principal. A continuación, se reenvía la solicitud de conexión a cada una de las réplicas secundarias de la lista de enrutamiento en modo round-robin.

## <a name="read-scale-availability-groups-without-cluster"></a>Grupos de disponibilidad de escalado de lectura sin clúster

En [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] y versiones anteriores, todos los grupos de disponibilidad requerían un clúster. Ese clúster proporcionaba alta disponibilidad y recuperación ante desastres (HADR) para respaldar la continuación del negocio. Además, las réplicas secundarias se configuraban para operaciones de lectura. Si la alta disponibilidad no era el objetivo, se invertía una sobrecarga operativa considerable en configurar y usar un clúster. SQL Server 2017 incluye los grupos de disponibilidad de escalado de lectura sin un clúster. 

Si lo que necesita su negocio es conservar los recursos de cara a las cargas de trabajo críticas que se ejecutan en la réplica principal, puede usar enrutamiento de solo lectura o conectarse directamente a las réplicas secundarias legibles. No es necesario depender de la integración con ninguna tecnología de agrupación en clústeres. Estas nuevas funciones están disponibles en sistemas SQL Server 2017 que se ejecutan en plataformas tanto Windows como Linux.

>[!IMPORTANT]
>Esto no es una configuración de alta disponibilidad; no hay ninguna infraestructura que supervise y coordine la detección de errores y la conmutación automática por error. Sin un clúster, SQL Server no puede proporcionar el objetivo de tiempo de recuperación (RTO) bajo que ofrece una solución de alta disponibilidad automatizada. Si necesita funcionalidades de alta disponibilidad, use un administrador de clústeres (clústeres de conmutación por error de Windows Server o Pacemarker en Linux).
>
>El grupo de disponibilidad de escalado de lectura puede proporcionar la capacidad de recuperación ante desastres. Cuando las réplicas de solo lectura están en modo de confirmación sincrónica, proporcionan un objetivo de punto de recuperación (RPO) de cero. Para conmutar por error un grupo de disponibilidad de escalado de lectura, consulte [Conmutación por error de la réplica principal en un grupo de disponibilidad de escalado de lectura](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md#ReadScaleOutOnly).

## <a name="use-distributed-availability-groups-for-geographic-read-scale"></a>Usar grupos de disponibilidad distribuidos de escalado de lectura geográfico

Las soluciones separadas geográficamente pueden implementar soluciones de escalado de lectura con grupos de disponibilidad distribuidos. Puede usarlas para descargar las cargas de trabajo de lectura de la réplica principal a las réplicas secundarias en sitios que están más cerca del origen de las cargas de trabajo de lectura. Los grupos de disponibilidad distribuidos reducen la utilización de los recursos en la réplica principal. También ayudan al rendimiento de lectura ya que reducen la latencia de red y a sacar partido de los recursos dedicados.

Un único grupo de disponibilidad distribuido puede tener hasta 17 réplicas secundarias legibles. Para incrementar la capacidad de escalado, cree una cadena de margarita con varios grupos de disponibilidad para aumentar más aún el número de réplicas legibles. También puede implementar dos grupos de disponibilidad distribuidos desde el mismo grupo de disponibilidad para las lecturas de baja latencia en entornos geográficamente dispersos.




## <a name="next-steps"></a>Pasos siguientes

[Configurar un grupo de disponibilidad de escalado de lectura en Linux](../../../linux/sql-server-linux-availability-group-configure-rs.md)

[Configurar un grupo de disponibilidad de escalado de lectura en Windows](../../../database-engine/availability-groups/windows/configure-read-scale-availability-groups.md)

## <a name="see-also"></a>Vea también

 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
