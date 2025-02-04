---
title: Administración de certificados (Administrador de configuración de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/16/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b98f52d7c8e23530c13da6ad44d90090998ac09e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68212741"
---
# <a name="certificate-management-sql-server-configuration-manager"></a>Administración de certificados (Administrador de configuración de SQL Server)

En este tema se explica cómo implementar y administrar certificados en la topología de clúster de conmutación por error o grupo de disponibilidad de SQL Server Always On.

Los certificados SSL/TLS son de uso generalizado para proteger el acceso a SQL Server. Con versiones anteriores de SQL Server, las organizaciones con grandes implementaciones de SQL Server tenían que desplegar un esfuerzo considerable para mantener su infraestructura de certificados de SQL Server, frecuentemente mediante el desarrollo de scripts y la ejecución de comandos manuales. Con SQL Server 2019, la administración de certificados está integrada en Administrador de configuración de SQL Server, lo que simplifica tareas comunes como: 

* Ver y validar certificados instalados en una instancia de SQL Server. 
* Identificar aquellos certificados a punto de expirar. 
* Implementar certificados en equipos de grupos de disponibilidad desde el nodo que contiene la réplica principal. 
* Implementar certificados en equipos que participan en una instancia de clúster de conmutación por error desde el nodo activo.

> [!NOTE]
> Puede usar la administración de certificados de Administrador de configuración de SQL Server con versiones anteriores de SQL Server, a partir de SQL Server 2008.

##  <a name="provision-single-server-cert"></a> Para instalar un certificado para una única instancia de SQL Server  
  
1. En Administrador de configuración de SQL Server, en el panel de la consola, expanda **Configuración de red de SQL Server**.  
  
2. Haga clic con el botón derecho en **Protocolos para** *&lt;nombre de instancia&gt;* y luego seleccione **Propiedades**.  
  
3. Elija la pestaña **Certificado** y luego seleccione **Importar**.  
  
4. Seleccione **Examinar** y luego el archivo del certificado.  
  
5. Seleccione **Siguiente** para validar el certificado. Si no hay ningún error, seleccione **Siguiente** para importar el certificado a la instancia local.  
  
 
##  <a name="provision-failover-cluster-cert"></a> Para instalar un certificado en una configuración de clúster de conmutación por error  
  
1. En Administrador de configuración de SQL Server, en el panel de la consola, expanda **Configuración de red de SQL Server**.
  
2. Haga clic con el botón derecho en **Protocolos para** *&lt;nombre de instancia&gt;* y luego elija **Propiedades**. 

3. Elija la pestaña **Certificado** y luego seleccione **Importar**.

4. Seleccione el tipo de certificado y si quiere importarlo solo para el nodo actual o para cada nodo de clúster individual.

5. Si va a instalar para un solo nodo, elija **Examinar** y seleccione el archivo del certificado. Luego vaya al paso 8.

6. Si va a instalar un certificado para cada nodo, seleccione **Siguiente** para ver los posibles nodos propietarios. Los posibles propietarios de la instancia de clúster de conmutación por error de SQL Server actual están preseleccionados.

7. Elija **Siguiente** para seleccionar el certificado que se va a importar.

8. Escriba la contraseña cuando se le solicite. Consulte las advertencias o errores después de la validación.

9. Seleccione **Siguiente** para importar los certificados seleccionados.

> [!NOTE]
> Siga estos pasos en el nodo activo de la instancia de clúster de conmutación por error de SQL Server. El usuario debe tener permisos de administrador en todos los nodos de clúster.

##  <a name="provision-availability-group-cert"></a>Para instalar un certificado en una configuración de grupo de disponibilidad  
  
1. En el panel de la consola de Administrador de configuración de SQL Server, expanda **Configuración de red de SQL Server**.
  
2. Haga clic con el botón derecho en **Protocolos para** *&lt;nombre de instancia&gt;* y luego seleccione **Propiedades**.  
  
3. Elija la pestaña **Certificado** y seleccione **Importar**.  
  
4. Elija el tipo de certificado y seleccione **Siguiente** para seleccionar de la lista de grupos de disponibilidad conocidos.  

5. Seleccione **Siguiente** para elegir certificados para cada nodo de réplica. Los certificados deben tener un nombre de archivo que coincida con el nombre de NetBIOS de los nodos.

6. Seleccione **Siguiente** para importar el certificado en cada nodo.


> [!NOTE]
> Siga estos pasos desde el nodo que contiene la réplica principal del grupo de disponibilidad. El usuario debe tener permisos de administrador en todos los nodos de clúster.

