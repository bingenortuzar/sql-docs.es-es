---
title: Habilitar un publicador remoto en un distribuidor (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- remote Distributors [SQL Server replication]
- Publishers [SQL Server replication]
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: ccf53893db8de9e80a1c8545dfe7a5af1819a6a7
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768529"
---
# <a name="enable-a-remote-publisher-at-a-distributor-sql-server-management-studio"></a>Habilitar un publicador remoto en un distribuidor (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Habilite un publicador para utilizar un distribuidor remoto en la página **Publicadores** . Esta página está disponible en el Asistente para configurar la distribución y en el cuadro de diálogo **Propiedades del distribuidor: \<Distribuidor>** . Para obtener más información sobre el uso del asistente y el acceso al cuadro de diálogo, consulte [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md) y [Ver y modificar propiedades del distribuidor y el publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-enable-a-publisher-in-the-configure-distribution-wizard"></a>Para habilitar un publicador en el Asistente para configurar la distribución  
  
1.  En la página **Publicadores** del Asistente para configurar la distribución, haga clic en **Agregar**.  
  
2.  Haga clic en **Agregar publicador de SQL Server**. Para obtener información acerca de cómo habilitar un publicador de Oracle para utilizar un distribuidor, vea [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  En el cuadro de diálogo **Conectar al servidor** , especifique la información de conexión con el publicador que utilizará el distribuidor remoto y, a continuación, haga clic en **Conectar**.  
  
4.  En la página **Contraseña del distribuidor** , en los cuadros de texto **Contraseña** y **Confirmar contraseña** , especifique una contraseña segura para la cuenta **distributor_admin** , que la replicación utiliza para conectar del publicador al distribuidor y realizar las tareas administrativas.  
  
5.  Para ver y modificar la configuración de un publicador, haga clic en el botón de propiedades ( **...** ).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

### <a name="to-enable-a-publisher-in-the-distributor-properties-dialog-box"></a>Para habilitar un publicador en el cuadro de diálogo Propiedades del distribuidor  
  
1.  En la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor: \<Distribuidor>** , haga clic en **Agregar**.  
  
2.  Haga clic en **Agregar publicador de SQL Server**. Para obtener información acerca de cómo habilitar un publicador de Oracle para utilizar un distribuidor, vea [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  En el cuadro de diálogo **Conectar al servidor** , especifique la información de conexión con el publicador que utilizará el distribuidor remoto y, a continuación, haga clic en **Conectar**.  
  
4.  En la página **Publicadores** , en los cuadros de texto **Contraseña** y **Confirmar contraseña** , especifique una contraseña segura para la cuenta **distributor_admin** , que la replicación utiliza para conectar del publicador al distribuidor y realizar las tareas administrativas.  
  
5.  Para ver y modificar la configuración de un publicador, haga clic en el botón de propiedades ( **...** ).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)   
 [Proteger el distribuidor](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  
