---
title: Administración de SQL Server en Linux
description: En este artículo se proporcionan vínculos a herramientas y tareas de administración comunes para SQL Server en Linux.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.openlocfilehash: e38e51eb1db6c335175b2fc55636532df88ac27d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000058"
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>Selección de la herramienta adecuada para administrar SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Hay varias maneras de administrar SQL Server en Linux. En la siguiente sección se proporciona una introducción rápida a las distintas herramientas y técnicas de administración con referencias a más recursos.

## <a name="mssql-conf"></a>mssql-conf 

La herramienta **mssql-conf** configura SQL Server en Linux. Para obtener más información, consulte [Configurar SQL Server en Linux con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="transact-sql"></a>Transact-SQL

Casi todo lo que puede hacer en una herramienta de cliente también se puede llevar a cabo con instrucciones Transact-SQL. SQL Server proporciona [vistas de administración dinámica (DMV)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) que consultan el estado y la configuración de SQL Server. También hay [comandos Transact-SQL](../t-sql/language-reference.md) para las tareas de administración de bases de datos. Puede ejecutar estos comandos en cualquier herramienta cliente que admita la conexión a SQL Server y la ejecución de consultas Transact-SQL, por ejemplo, [sqlcmd](sql-server-linux-setup-tools.md) o [Visual Studio Code](sql-server-linux-develop-use-vscode.md).

## <a name="azure-data-studio"></a>Azure Data Studio

Azure Data Studio es una nueva herramienta multiplataforma para administrar SQL Server. Para obtener más información, vea [¿Qué es Azure Data Studio?](../azure-data-studio/what-is.md)

## <a name="sql-server-management-studio-on-windows"></a>SQL Server Management Studio en Windows

SQL Server Management Studio (SSMS) es una aplicación Windows que proporciona una interfaz gráfica de usuario para administrar SQL Server. Aunque actualmente solo se ejecuta en Windows, puede usarlo para conectarse de forma remota a instancias de SQL Server de Linux. Para obtener más información sobre el uso de SSMS para administrar SQL Server, vea [Usar SQL Server Management Studio para administrar SQL Server en Linux](sql-server-linux-manage-ssms.md).

## <a name="mssql-cli-preview"></a>mssql-cli (versión preliminar)

Microsoft ha lanzado una nueva herramienta de scripting multiplataforma para SQL Server: [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/). Esta herramienta está actualmente en versión preliminar.

## <a name="powershell"></a>PowerShell

PowerShell proporciona un entorno de línea de comandos enriquecido para administrar SQL Server en Linux. Para obtener más información, consulte [Uso de PowerShell para administrar SQL Server en Linux](sql-server-linux-manage-powershell.md).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre SQL Server en Linux, vea [SQL Server en Linux](sql-server-linux-overview.md).
