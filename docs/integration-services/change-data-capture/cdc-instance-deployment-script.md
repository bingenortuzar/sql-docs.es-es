---
title: Script de implementación de instancia CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8fa82822-ac99-48ef-a18d-f4f3a77105b4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 595af36a5eb19ff6fd019df8a2b9203537350c5a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298907"
---
# <a name="cdc-instance-deployment-script"></a>Script de implementación de instancia CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El cuadro de diálogo Script de implementación de instancia CDC muestra el script de implementación de la instancia CDC. Este script se puede usar para volver a crear la base de datos CDC con todos sus artefactos en otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente.  
  
 Al completarse el script de implementación, debe asegurarse de lo siguiente:  
  
-   El script de implementación da por supuesto que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino se preparó para CDC de Oracle mediante la Consola de configuración del servicio CDC de Oracle o mediante el **script de preparación** que el programa crea.  
  
-   La parte del script que se emplea para habilitar la base de datos para CDC debe ejecutarla un `sysadmin`.  
  
-   El script no conserva la contraseña de minería de registros de Oracle. Es necesario establecerla manualmente después de que se ejecute el script y se inicie el servicio CDC de Oracle.  
  
 Seleccione las opciones siguientes en el cuadro de diálogo **Script de implementación de instancia CDC** .  
  
 **Guardar como**  
 Guarda el script en un archivo de texto que puede guardar en cualquier ubicación que desee. Puede copiar el archivo con el script a cualquier otro servidor para ejecutarlo en él.  
  
 **Copiar**  
 Copia el script en el Portapapeles. Puede pegar el script en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o en cualquier editor de texto para ejecutar los scripts posteriormente.  
  
## <a name="see-also"></a>Consulte también  
 [Preparar SQL Server para CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
