---
title: Entornos multiusuario (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- users [SQL Server], multiuser environments
- conflict resolution [Visual Database Tools]
- multiple users making database changes
- multiuser environments [Visual Database Tools]
- database modifications [SQL Server]
- version control [Visual Database Tools]
- Visual Database Tools [SQL Server], multiuser environments
ms.assetid: 330bd48c-9427-4967-b58e-b7c492d5ee36
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c9053a4b6873c565320e5d8ed9664799990ebbcb
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68258443"
---
# <a name="multiuser-environments-visual-database-tools"></a>Entornos multiusuario (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Un entorno multiusuario es un entorno al que otros usuarios pueden conectarse y en el que pueden realizar cambios en la misma base de datos en la que usted está trabajando. Como resultado, es posible que varios usuarios estén trabajando con los mismos objetos de base de datos a la vez. De este modo, en un entorno multiusuario es posible que la base de datos se vea afectada por los cambios realizados por otros usuarios mientras está trabajando y viceversa.  
  
Una cuestión clave al trabajar con bases de datos en un entorno multiusuario son los permisos de acceso. Los permisos de que dispone para la base de datos determinan el alcance del trabajo que puede realizar con la base de datos. Por ejemplo, para realizar cambios en objetos en una base de datos, debe disponer de los permisos de escritura apropiados para la base de datos. Para obtener más información acerca de los permisos en la base de datos, vea la documentación de la base de datos. Para más información, consulte [Permisos y Visual Database Tools &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/permissions-and-visual-database-tools-visual-database-tools.md).  
  
Cuando guarda los cambios realizados en las tablas, el Diseñador de tablas comprueba que la base de datos no se ha modificado desde que se guardaron los cambios por última vez. Si otro usuario ha realizado cambios, se le notificará que se ha modificado la base de datos. Es posible que necesite reconciliar estos cambios. Para más información, consulte [Reconciliar los cambios realizados por varios usuarios &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/reconcile-changes-made-by-multiple-users-visual-database-tools.md).  
  
En un entorno multiusuario debe tenerse en cuenta consideraciones especiales para impedir que se produzcan conflictos en los cambios. Para más información, consulte [Problemas de evolución de bases de datos &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/issues-of-database-evolution-visual-database-tools.md).  
  
Un modo de evitar problemas es trabajar con una copia de la base de datos, como una base de datos de prueba, cuando realiza los cambios; a continuación, puede crear un script y ejecutarlo para que aplique estos cambios en la base de datos original después de solucionar los conflictos sin conexión. Para más información, consulte [Bases de datos de desarrollo, pruebas y producción &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/development-test-and-production-databases-visual-database-tools.md).  
  
