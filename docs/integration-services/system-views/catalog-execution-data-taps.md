---
title: catalog.execution_data_taps | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 54226c01-5b8f-4730-8a5f-1da2613f9689
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5f3450320f28a2f0abd133c93d1b43512484d446
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296573"
---
# <a name="catalogexecution_data_taps"></a>catalog.execution_data_taps 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra información de cada derivación de datos definida en una ejecución.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|data_tap_id|**bigint**|Identificador (id.) único de la derivación de datos.|  
|execution_id|**bigint**|Identificador único (id.) de la instancia de ejecución.|  
|package_path|**nvarchar(max)**|Ruta de acceso del paquete de la tarea de flujo de datos en la que se derivan los datos.|  
|dataflow_path_id_string|**nvarchar(4000)**|Cadena de identificación de la ruta de flujo de datos.|  
|dataflow_task_guid|**uniqueidentifier**|Identificador único de la tara de flujos de datos.|  
|max_rows|**int**|Número de filas que se van a capturar. Si este valor no se especifica, se capturan todas las filas.|  
|filename|**nvarchar(4000)**|Nombre del archivo de volcado de datos. Para obtener más información, consulte [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).|  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la instancia de ejecución  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
## <a name="see-also"></a>Consulte también  
 [Generar archivos de volcado para la ejecución de paquetes](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
