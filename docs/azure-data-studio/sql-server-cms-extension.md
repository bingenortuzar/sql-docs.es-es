---
title: Extensión Servidores de administración central de SQL Server
titleSuffix: Azure Data Studio
description: Instalación y uso de la extensión Servidores de administración central de SQL Server (versión preliminar) para Azure Data Studio
ms.custom: seodec18
ms.date: 06/06/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 03edfc5b6d95c5cd6497d96d7014641f3032fb84
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959202"
---
# <a name="sql-server-central-management-servers-extension-preview"></a>Extensión Servidores de administración central de SQL Server (versión preliminar)
La extensión Servidores de administración central permite a los usuarios almacenar una lista de instancias de SQL Server organizadas en uno o más grupos. Las acciones que se llevan a cabo mediante un servidor de administración central (CMS) actúan en todos los servidores del grupo.

Esta experiencia está actualmente en su versión preliminar inicial. Puede notificar cualquier problema y solicitar nuevas características [aquí](https://github.com/microsoft/azuredatastudio/issues).

![Extensión CMS](media/sql-server-cms-extension/cms-list.png)

## <a name="install-the-sql-server-central-management-servers-extension"></a>Instalación de la extensión Servidores de administración central de SQL Server

1. Para abrir el administrador de extensiones y acceder a las extensiones disponibles, seleccione el icono extensiones, o bien seleccione **Extensiones** en el menú **Ver**.
2. Seleccione una extensión disponible para ver sus detalles.
1. Seleccione la extensión que desee (Servidores de administración central de SQL Server) y seleccione **Instalar**.

### <a name="how-do-i-start-central-management-servers"></a>¿Cómo se inicia Servidores de administración central?
 Para ver Servidores de administración central, haga clic en el icono Conexiones (Ctrl/CMD + G). La primera vez que se descarga la extensión, la vista de CMS aparece minimizada; para abrirla, haga clic en **Servidores de administración central**.

## <a name="next-steps"></a>Pasos siguientes
[Aquí puede leer más información](https://docs.microsoft.com/sql/ssms/register-servers/create-a-central-management-server-and-server-group) sobre los conceptos de Servidores de administración central.


