---
title: Copia de seguridad y la carga de hardware - almacenamiento de datos paralelos
description: Para implementar los datos de extremo a otro con el almacenamiento de datos paralelos (PDW) de la solución en Analytics Platform System (APS) de almacenamiento, deberá crear un plan de copia de seguridad del almacenamiento de datos y cargar los datos. Use esta guía para adquirir y configurar los servidores de carga y copia de seguridad que satisfacen sus requisitos empresariales.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 90f142a8bb86f99ed5cf5d9ff926bdf849060324
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961414"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>Copia de seguridad y la carga de información general de hardware: almacenamiento de datos paralelos
Para implementar los datos de extremo a otro con el almacenamiento de datos paralelos (PDW) de la solución en Analytics Platform System (APS) de almacenamiento, deberá crear un plan de copia de seguridad del almacenamiento de datos y cargar los datos. Use esta guía para adquirir y configurar los servidores de carga y copia de seguridad que satisfacen sus requisitos empresariales.  
  
## <a name="acquire-and-configure-backup-servers"></a>Adquirir y configurar servidores de copia de seguridad  
![Proceso de copia de seguridad](media/backup-process.png "proceso de copia de seguridad")  
  
Para una base de datos PDW de copia de seguridad, necesita uno o más servidores de copia de seguridad. Puede usar su propio hardware existente o adquirir nuevo hardware. Para obtener más información, consulte [adquirir y configurar un servidor de copia de seguridad](acquire-and-configure-backup-server.md). Estas instrucciones incluyen un [hoja de planificación de capacidad de servidor de copia de seguridad](backup-capacity-planning-worksheet.md) le ayudará a planear la solución adecuada para la copia de seguridad.  
  
## <a name="acquire-and-configure-loading-servers"></a>Adquirir y configurar servidores de carga  
![Proceso de carga](media/loading-process.png "proceso de carga")  
  
Para cargar datos, necesita uno o más servidores de carga. Puede usar su propio ETL existente u otros servidores, o puede comprar nuevos servidores. Para obtener más información, consulte [adquirir y configurar un servidor de carga](acquire-and-configure-loading-server.md). Estas instrucciones incluyen un [al cargar la hoja de cálculo de planeación de capacidad servidor](loading-server-capacity-planning-worksheet.md) le ayudará a planear la solución adecuada para la carga.  
  
## <a name="see-also"></a>Vea también  
[Información general de copia de seguridad y restauración](backup-and-restore-overview.md)  
[Información general de carga](load-overview.md)  
  
