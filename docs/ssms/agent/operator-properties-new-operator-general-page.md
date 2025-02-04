---
title: Propiedades del operador - Nuevo operador (página General) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.operator.general.f1
ms.assetid: c036d1c9-83d1-4a95-b67e-29d283b1a046
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6ce0287cb4c1e56ba5ce50a91838367b3b1791ff
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260211"
---
# <a name="operator-properties---new-operator-general-page"></a>Propiedades del operador - Nuevo operador (página General)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Utilice esta página para ver y modificar las propiedades generales de los operadores del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
**Nombre**  
Cambie el nombre del operador.  
  
**Enabled**  
Habilite el operador. Si no se hablita, no se le envía ninguna notificación.  
  
**Nombre de correo electrónico**  
Especifica la dirección de correo electrónico del operador.  
  
**Dirección de NET SEND**  
Especifique la dirección que se va a usar para **net send**.  
  
**Correo electrónico del buscapersonas**  
Especifica la dirección de correo electrónico que debe utilizarse para el buscapersonas del operador.  
  
**Programación de buscapersonas en servicio**  
Establece las horas a las que el buscapersonas está activo.  
  
**Lunes - Viernes**  
Seleccione los días en los que el buscapersonas está activo.  
  
**Inicio del día laborable**  
Seleccione la hora del día a partir de la cual el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envía mensajes al buscapersonas.  
  
**Fin del día laborable**  
Seleccione la hora del día a partir de la cual el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deja de enviar mensajes al buscapersonas.  
  
## <a name="see-also"></a>Consulte también  
[Operadores](../../ssms/agent/operators.md)  
  
