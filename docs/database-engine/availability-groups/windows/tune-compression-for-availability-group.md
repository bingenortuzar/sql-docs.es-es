---
title: Optimizar la compresión en los grupos de disponibilidad | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 7632769c-b246-4766-886f-7c60ec540be8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3891d30ef5bfffb19ca1d4bfcaab290e3903816b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013668"
---
# <a name="tune-compression-for-availability-group"></a>Tune compression for availability group (Optimizar la compresión para los grupos de disponibilidad)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
De forma predeterminada, SQL Server comprime flujos de datos cuando sea apropiado para los grupos de disponibilidad. La compresión reduce el tráfico de red, aumenta la carga de CPU y puede inducir la latencia. Para habilitar la compresión, debe ser miembro del rol fijo de servidor sysadmin. En la siguiente tabla se muestra cuándo SQL Server usa la compresión para las secuencias de registro de los grupos de disponibilidad:

| Escenario | Configuración de compresión
| ---- | ----
| Réplica de confirmación sincrónica | No comprimida
| Réplicas de confirmación asincrónica | Compressed
| Durante la propagación automática | No comprimida

## <a name="trace-flags-for-availability-group-compression"></a>Marcas de seguimiento de la compresión de los grupos de disponibilidad 

Para la mayoría de los escenarios, Microsoft no recomienda cambiar esta configuración. Puede usar marcas de seguimiento globales para probar a cambiar esta configuración. SQL Server aplica marcas de seguimiento globales a toda la instancia. Todos los grupos de disponibilidad de la instancia se verán afectados por esta configuración.  

En la siguiente tabla se muestran las marcas de seguimiento que modificarán el comportamiento de compresión predeterminado para SQL Server. 

marca de seguimiento | Descripción
------------- | -------------
1462          | Deshabilita la compresión de secuencias de registro para los grupos de disponibilidad con réplicas asincrónicas. Esta característica está habilitada de forma predeterminada en las réplicas asincrónicas para optimizar el ancho de banda de red.
9567          | Habilita la compresión del flujo de datos para los grupos de disponibilidad durante la propagación automática. Durante la propagación automática, la compresión puede reducir significativamente el tiempo de transferencia y aumentará la carga del procesador.
9592          | Habilita la compresión de secuencias de registro para los grupos de disponibilidad AlwaysOn con réplicas sincrónicas. Esta característica está deshabilitada de forma predeterminada en las réplicas sincrónicas porque la compresión agrega latencia. La compresión de secuencias de registro está habilitada de forma predeterminada para las réplicas asincrónicas.


## <a name="resources"></a>Recursos


[Opciones de inicio del servicio de motor de base de datos](../../../database-engine/configure-windows/database-engine-service-startup-options.md)

[Propagación automática](https://msdn.microsoft.com/library/mt735149(SQL.130).aspx)

[Requisitos previos de AlwaysOn](prereqs-restrictions-recommendations-always-on-availability.md) 
