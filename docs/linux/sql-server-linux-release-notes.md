---
title: Notas de la versión de SQL Server 2017 en Linux
description: Este artículo contiene las notas de la versión y las características admitidas de SQL Server 2017 ejecutándose en Linux. Se incluyen las notas de la versión más reciente y de varias versiones anteriores.
author: VanMSFT
ms.author: vanto
ms.date: 08/01/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: 93472679a524214010ccc2d10eacfd37d7e001e8
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68763148"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Notas de la versión de SQL Server 2017 en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Las siguientes notas de la versión son válidas para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] ejecutándose en Linux. Este artículo se divide en secciones para cada versión. La versión de disponibilidad general tiene compatibilidad detallada y una lista de problemas conocidos. Cada actualización acumulativa o versión de distribución general (GDR) tiene un vínculo a un artículo de soporte técnico en el que se describen los cambios en la actualización acumulativa, así como vínculos a las descargas de paquetes para Linux.

> [!TIP]
> Estas notas de la versión son específicas para versiones de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Para obtener más información sobre la nueva versión de [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], vea [Notas de la versión para la versión preliminar de SQL Server 2019 en Linux](sql-server-linux-release-notes-2019.md?view=sql-server-ver15).

## <a name="supported-platforms"></a>Plataformas compatibles

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5 o 7.6 Server | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04 LTS | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de Docker 1.8 y versiones posteriores en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obtener más información, revise los [requisitos del sistema](sql-server-linux-setup.md#system) de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux. Para acceder a la directiva de soporte técnico más reciente de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)], vea [Directiva de soporte técnico para Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Herramientas

La mayoría de las herramientas de cliente para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] también pueden usarse fácilmente para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ejecutándose en Linux. Algunas herramientas pueden tener un requisito de versión específica para funcionar correctamente con Linux. Para obtener la lista completa de herramientas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Herramientas y utilidades de SQL para SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Historial de versiones

En la tabla siguiente, se muestra la lista del historial de versiones de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)].

| Versión               | Versión       | Fecha de la versión |
|-----------------------|---------------|--------------|
| [CU16](#CU16)         | 14.0.3223.3   | 2019-08-01   |
| [CU15](#CU15)         | 14.0.3162.1   | 23-05-2019   |
| [CU14](#CU14)         | 14.0.3076.1   | 25-03-2019   |
| [CU13](#CU13)         | 14.0.3048.4   | 18-12-2018   |
| [CU12](#CU12)         | 14.0.3045.24  | 24-10-2018   |
| [CU11](#CU11)         | 14.0.3038.14  | 20-09-2018   |
| [CU10](#CU10)         | 14.0.3037.1   | 27-08-2018   |
| [CU9-GDR2](#CU9-GDR2) | 14.0.3035.2   | 18-08-2018   |
| [GDR2](#GDR2)         | 14.0.2002.14  | 18-08-2018   |
| [CU9](#CU9)           | 14.0.3030.27  | 18-07-2018   |
| [CU8](#CU8)           | 14.0.3029.16  | 21-06-2018   |
| [CU7](#CU7)           | 14.0.3026.27  | 24-05-2018   |
| [CU6](#CU6)           | 14.0.3025.34  | 19-04-2018   |
| [CU5](#CU5)           | 14.0.3023.8   | 20-03-2018   |
| [CU4](#CU4)           | 14.0.3022.28  | 20-02-2018   |
| [CU3](#CU3)           | 14.0.3015.40  | 03-01-2018   |
| [GDR1](#GDR1)         | 14.0.2000.63  | 03-01-2018   |
| [CU2](#CU2)           | 14.0.3008.27  | 28-11-2017   |
| [CU1](#CU1)           | 14.0.3006.16  | 24-10-2017   |
| [GA](#GA)             | 14.0.1000.169 | 02-10-2017   |

## <a id="cuinstall"></a> Procedimiento para instalar las actualizaciones

Si ha configurado el repositorio de actualizaciones acumulativas (**mssql-server-2017**), obtendrá la actualización acumulativa más reciente de paquetes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] al realizar nuevas instalaciones. El repositorio de actualizaciones acumulativas es el predeterminado para todos los artículos de instalación de paquetes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux. Si ha configurado el repositorio de GDR (**mssql-server-2017-gdr**), solo obtendrá actualizaciones de seguridad críticas publicadas desde la versión de disponibilidad general. Si necesita actualizaciones de GDR o actualizaciones acumulativas del contenedor de Docker, vea las imágenes oficiales para [Microsoft SQL Server en Linux para el motor de Docker](https://hub.docker.com/r/microsoft/mssql-server). Para obtener más información sobre la configuración del repositorio, vea [Configuración de repositorios para SQL Server en Linux](sql-server-linux-change-repo.md).

Si va a actualizar paquetes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] existentes, ejecute el comando de actualización adecuado para cada paquete con el fin de obtener la actualización acumulativa más reciente. Para obtener instrucciones de actualización específicas para cada paquete, vea las siguientes guías de instalación:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar la búsqueda de texto completo SQL Server en Linux](sql-server-linux-setup-full-text-search.md)
- [Instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Habilitar el Agente SQL Server](sql-server-linux-setup-sql-agent.md)

## <a id="CU16"></a> CU16 (agosto de 2019)

Esta es la versión de la actualización acumulativa 16 (CU16) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3223.3. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/en-us/help/4498951](https://support.microsoft.com/en-us/help/4498951).

### <a name="whats-new"></a>What's New

|Nueva característica o actualización | Detalles |
|:---|:---|
| Compatibilidad con MSDTC | Compatibilidad con Microsoft DTC (Coordinador de transacciones distribuidas) para SQL Server 2017. Para más información, vea [Procedimiento para configurar Microsoft DTC (Coordinador de transacciones distribuidas) en Linux](sql-server-linux-configure-msdtc.md). |

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3223.3-15 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3223.3-15.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3223.3-15.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3223.3-15.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3223.3-15 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3223.3-15.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3223.3-15.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3223.3-15.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3223.3-15 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3223.3-15_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3223.3-15_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3223.3-15_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU15"></a> CU15 (mayo de 2019)

Esta es la versión de la actualización acumulativa 15 (CU15) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3162.1. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/en-us/help/4498951](https://support.microsoft.com/en-us/help/4498951).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3162.1-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3162.1-1 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3162.1-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU14"></a> CU14 (marzo de 2019)

Esta es la versión de la actualización acumulativa 14 (CU14) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3076.1. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4484710](https://support.microsoft.com/help/4484710).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3076.1-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3076.1-2 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3076.1-2 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU13"></a> CU13 (diciembre de 2018)

Esta es la versión de la actualización acumulativa 13 (CU13) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3048.4. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4466404](https://support.microsoft.com/help/4466404).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3048.4-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3048.4-1 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3048.4-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a> CU12 (octubre de 2018)

Esta es la versión de la actualización acumulativa 12 (CU12) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3045.24. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4464082](https://support.microsoft.com/help/4464082).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3045.24-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3045.24-1 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3045.24-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a> CU11 (septiembre de 2018)

Esta es la versión de la actualización acumulativa 11 (CU11) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3038.14. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4462262](https://support.microsoft.com/help/4462262).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3038.14-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3038.14-2 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3038.14-2 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a> CU10 (agosto de 2018)

Esta es la versión de la actualización acumulativa 10 (CU10) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3037.1. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4342123](https://support.microsoft.com/help/4342123).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3037.1-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3037.1-2 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3037.1-2 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a> CU9-GDR2 (agosto de 2018)

Esta es una actualización de seguridad que también incluye la actualización acumulativa publicada anteriormente (CU9) para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3035.2. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4293805](https://support.microsoft.com/help/4293805).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3035.2-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| Paquete RPM de SLES | 14.0.3035.2-1 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3035.2-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a> GDR2 (agosto de 2018)

Esta es una actualización de seguridad que solo incluye las revisiones de seguridad de GDR2 (y GDR1) para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)].  La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.2002.14. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4293803](https://support.microsoft.com/help/4293803).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.2002.14-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.2002.14-1 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.2002.14-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a> CU9 (julio de 2018)

Esta es la versión de la actualización acumulativa 9 (CU9) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3030.27. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4341265](https://support.microsoft.com/help/4341265).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3030.27-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3030.27-1 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3030.27-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a> CU8 (julio de 2018)

Esta es la versión de la actualización acumulativa 8 (CU8) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3029.16. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4338363](https://support.microsoft.com/help/4338363).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3029.16-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3029.16-1 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3029.16-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a> CU7 (mayo de 2018)

Esta es la versión de la actualización acumulativa 7 (CU7) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3026.27. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4229789](https://support.microsoft.com/help/4229789).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3026.27-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3026.27-2 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3026.27-2 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a> CU6 (abril de 2018)

Esta es la versión de la actualización acumulativa 6 (CU6) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3025.34. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4101464](https://support.microsoft.com/help/4101464).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3025.34-3 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3025.34-3 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3025.34-3 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5 (marzo de 2018)

Esta es la versión de la actualización acumulativa 5 (CU5) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3023.8. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4092643](https://support.microsoft.com/help/4092643).

### <a name="known-upgrade-issue"></a>Problemas de actualización conocidos

Para actualizar desde una versión anterior a CU5, es posible que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no pueda iniciarse y se muestre el error siguiente:

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

Para solucionar el error, habilite el Agente SQL Server y reinicie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con los comandos siguientes:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3023.8-5 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3023.8-5 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3023.8-5 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a> CU4 (febrero de 2018)

Esta es la versión de la actualización acumulativa 4 (CU4) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3022.28. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4056498](https://support.microsoft.com/help/4056498).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

> [!NOTE]
> En CU4, el Agente SQL Server ya no se instala como un paquete separado. Se instala con el paquete del motor y es necesario habilitarlo para poder usarlo.

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3022.28-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3022.28-2 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3022.28-2 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a> GDR1 (enero de 2018)

Esta es una actualización de seguridad que solo incluye las revisiones de seguridad de GDR1 para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.2000.63. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4057122](https://support.microsoft.com/help/4057122).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.2000.63-3 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.2000.63-3 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.2000.63-3 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a> CU3 (enero de 2018)

Esta es la versión de la actualización acumulativa 3 (CU3) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3015.40. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4052987](https://support.microsoft.com/help/4052987).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3015.40-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM del Agente SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3015.40-1 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM del Agente SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3015.40-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[Paquete de Debian del Agente SQL Server](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (noviembre de 2017)

Esta es la versión de la actualización acumulativa 2 (CU2) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3008.27. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3008.27-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM del Agente SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3008.27-1 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM del Agente SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3008.27-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[Paquete de Debian del Agente SQL Server](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (octubre de 2017)

Esta es la versión de la actualización acumulativa 1 (CU1) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.3006.16. Para obtener información sobre las correcciones y mejoras de esta versión, vea [https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.3006.16-3 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM del Agente SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.3006.16-3 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM del Agente SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.3006.16-3 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[Paquete de Debian del Agente SQL Server](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> GA (octubre de 2017)

Esta es la versión de disponibilidad general de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. La versión de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] es 14.0.1000.169.

### <a name="package-details"></a>Detalles del paquete

En la tabla siguiente, se muestran los detalles del paquete y las ubicaciones de descarga de los paquetes de Debian y RPM. No es necesario que descargue directamente estos paquetes si sigue el procedimiento que se indica en las siguientes guías de instalación:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md)
- [Instalar la búsqueda de texto completo SQL Server en Linux](sql-server-linux-setup-full-text-search.md)
- [Instalar el paquete del Agente SQL Server](sql-server-linux-setup-sql-agent.md)
- [Instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM de Red Hat | 14.0.1000.169-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM del Agente SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM de SLES | 14.0.1000.169-2 | [Paquete RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM del Agente SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Paquete de Debian para Ubuntu 16.04 | 14.0.1000.169-2 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[Paquete de Debian del Agente SQL Server](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> Características y servicios no admitidos

Las siguientes características y servicios no están disponibles en Linux en el momento de la publicación de la versión de disponibilidad general. La compatibilidad de estas características se incrementará con el tiempo.

| Área | Característica o servicio no admitido |
|-----|-----|
| **Motor de base de datos** | Replicación transaccional |
| &nbsp; | Replicación de mezcla |
| &nbsp; | Captura de datos modificados (vea Agente SQL Server) |
| &nbsp; | Stretch DB |
| &nbsp; | PolyBase |
| &nbsp; | Consulta distribuida con conexiones de terceros |
| &nbsp; | Servidores vinculados a orígenes de datos distintos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | Procedimientos extendidos almacenados del sistema (XP_CMDSHELL, etc.) |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | Ensamblados de CLR con el conjunto de permisos EXTERNAL_ACCESS o UNSAFE |
| &nbsp; | Buffer Pool Extension |
| **Agente SQL Server** |  Subsistemas: CmdExec, PowerShell, Agente de lectura de cola, SSIS, SSAS, SSRS |
| &nbsp; | Trabajos |
| &nbsp; | Agente de registro del LOG |
| &nbsp; | Captura de datos modificados (CDC) |
| &nbsp; | Copia de seguridad administrada |
| **Alta disponibilidad** | Creación de reflejo de base de datos  |
| **Seguridad** | Administración extensible de claves |
| &nbsp; | Autenticación de AD para servidores vinculados | 
| &nbsp; | Autenticación de AD para grupos de disponibilidad | 
| &nbsp; | Herramientas de AD de terceros (Centrify, Vintela, PowerBroker) | 
| **Servicios** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |
| &nbsp; | Coordinador de transacciones distribuidas (DTC) |

## <a name="known-issues"></a>Problemas conocidos

En las secciones siguientes, se describen problemas conocidos con la versión de disponibilidad general de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] en Linux.

#### <a name="general"></a>General

- La longitud del nombre de host donde se instale [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ha de tener 15 caracteres o menos. 

    - **Solución:** cambie el nombre en /etc/hostname para que tenga 15 caracteres de longitud o menos.

- Al retrasar de forma manual la hora del sistema, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dejará de actualizar la hora interna del sistema en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

    - **Solución:** Reinicie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

- Solo se admiten las instalaciones de instancia única.

    - **Solución:** si tiene más de una instancia en un host específico, puede usar máquinas virtuales o contenedores de Docker. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager no puede conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux.

- El idioma predeterminado del inicio de sesión de **sa** es el inglés.

    - **Solución:** Cambie el idioma del inicio de sesión de **sa** con la instrucción **ALTER LOGIN**.

#### <a name="databases"></a>Bases de datos

- La base de datos maestra no se puede mover con la utilidad mssql-conf. Otras bases de datos del sistema se pueden mover con la utilidad mssql-conf.

- Al restaurar una base de datos cuya copia de seguridad se ha realizado en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Windows, tendrá que usar la cláusula **WITH MOVE** en la instrucción Transact-SQL.

- Las transacciones distribuidas que necesitan el servicio Microsoft DTC (Coordinador de transacciones distribuidas) no se admiten en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ejecutándose en Linux. Los servidores vinculados de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se admiten, excepto si se usa DTC. Para obtener más información, vea [Las transacciones distribuidas que necesitan el servicio Microsoft DTC (Coordinador de transacciones distribuidas) no se admiten en SQL Server ejecutándose en Linux](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/).

- Algunos algoritmos (conjuntos de cifrado) para TLS (Seguridad de la capa de transporte) no funcionan correctamente con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux. Esto causa errores de conexión al intentar conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], así como problemas al establecer conexiones entre réplicas en grupos de alta disponibilidad.

   - **Solución:** modifique el script de configuración **mssql.conf** para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux para deshabilitar los conjuntos de cifrado problemáticos; para hacerlo, siga este procedimiento:

      1. Agregue el texto siguiente a /var/opt/mssql/mssql.conf.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Reinicie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con el comando siguiente.

      ```bash
      sudo systemctl restart mssql-server
      ```

- Las bases de datos de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] en Windows que usan OLTP en memoria no se pueden restaurar en [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] en Linux. Para restaurar una base de datos de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] que use OLTP en memoria, primero actualice las bases de datos a [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] o [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] en Windows antes de moverlas a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux mediante las funciones de copia de seguridad y restauración, o asociar/desasociar.

- El permiso de usuario **ADMINISTER BULK OPERATIONS** no se admite en Linux en este momento.

#### <a name="networking"></a>Redes

Las características relacionadas con conexiones TCP salientes del proceso sqlservr, como servidores vinculados o grupos de disponibilidad, puede que no funcionen si se cumplen las condiciones siguientes:

1. El servidor de destino se especifica como un nombre de host, y no como una dirección IP.

1. La instancia de origen tiene deshabilitado IPv6 en el kernel. Para verificar si el sistema tiene IPv6 habilitado en el kernel, todas las pruebas siguientes necesitan completarse sin errores:

   - `cat /proc/cmdline` imprimirá la línea de comandos de arranque del kernel actual. El resultado no tiene que contener `ipv6.disable=1`.
   - El directorio /proc/sys/net/ipv6/ tiene que existir.
   - Un programa de C que realice una llamada a `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` tiene que ejecutarse sin errores (la llamada del sistema tiene que devolver “fd != -1” y no producir errores con EAFNOSUPPORT).

El error exacto depende de la característica. En el caso de servidores vinculados, esto se manifiesta como un error de tiempo de espera de inicio de sesión. Para los grupos de disponibilidad, el DDL `ALTER AVAILABILITY GROUP JOIN` en el servidor secundario producirá un error de tiempo de espera de configuración de descarga después de 5 minutos.

Para solucionar este problema, siga uno de estos procedimientos:

1. Use direcciones IP en lugar de nombres de host para especificar el destino de la conexión TCP.

1. Habilite IPv6 en el kernel; para hacerlo, quite `ipv6.disable=1` de la línea de comandos de arranque. Los pasos exactos dependen de la distribución de Linux y el cargador de arranque que use (por ejemplo, grub). Si no quiere deshabilitar IPv6, puede deshabilitarlo si establece `net.ipv6.conf.all.disable_ipv6 = 1` en la configuración de `sysctl` (por ejemplo, `/etc/sysctl.conf`). Esto impedirá que el adaptador de red del sistema obtenga una dirección IPv6, pero permitirá que funcionen las características de sqlservr.

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
Si usa recursos compartidos remotos de **NFS (Network File System)** en producción, tenga en cuenta los siguientes requisitos de compatibilidad:

- Use la versión de NFS **4.2 o posteriores**. Las versiones anteriores de NFS no admiten las características necesarias (como fallocate y la creación de archivos dispersos) que son comunes en los sistemas de archivos modernos.
- Busque solo los directorios **/var/opt/mssql** en el montaje NFS. Otros archivos, como los archivos binarios del sistema de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], no se admiten.
- Asegúrese de que los clientes de NFS usen la opción “nolock” al montar el recurso compartido remoto.

#### <a name="localization"></a>Localización

- Si usa una configuración regional distinta del inglés (en_us) durante la configuración, tendrá que usar la codificación UTF-8 en el terminal o en la sesión de Bash. Si usa la codificación ASCII, puede que se muestre un error parecido al siguiente:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Si no puede usar la codificación UTF-8, ejecute el programa de instalación con la variable de entorno MSSQL_LCID para especificar la opción de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Al ejecutar el programa de instalación mssql-conf y realizar una instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un idioma distinto del inglés, se muestran caracteres extendidos incorrectos después del texto localizado, “Configurando SQL Server…”. O bien, para instalaciones basadas en idiomas no latinos, puede que la frase no se muestre en absoluto. La frase que falta tendría que mostrar la siguiente cadena localizada: “El PID de licencias de proceso correctamente. La nueva edición es [Edición \<nombre\>]”. La cadena se muestra solo con fines informativos, y en la próxima actualización acumulativa de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se solucionará este problema para todos los idiomas. Esto no afecta a la instalación correcta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de ningún modo. 

#### <a name="full-text-search"></a>Búsqueda de texto completo

- No todos los filtros están disponibles en esta versión, incluidos los filtros para documentos de Office. Para obtener una lista de los filtros admitidos, vea [Instalar la búsqueda de texto completo de SQL Server en Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- El paquete **mssql-server-is** no se admite en SUSE en esta versión. Se admite actualmente en Ubuntu y en Red Hat Enterprise Linux (RHEL).

- Con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en Linux CTP 2.1 Refresh y posteriores, los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] pueden usar conexiones ODBC en Linux. Esta función se ha probado con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y los controladores ODBC de MySQL, pero también se espera que funcione con cualquier controlador ODBC de Unicode que respete la especificación de ODBC. En tiempo de diseño, puede proporcionar un DSN o una cadena de conexión para conectarse a los datos ODBC; también puede usar la autenticación de Windows. Para obtener más información, vea [la entrada de blog que anuncia la compatibilidad con ODBC en Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Las características siguientes no se admiten en esta versión al ejecutar paquetes de SSIS en Linux:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Base de datos del catálogo
  - Ejecución de paquetes programada por el Agente SQL
  - Autenticación de Windows
  - Componentes de terceros
  - Captura de datos modificados (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Escalar horizontalmente
  - Azure Feature Pack para SSIS
  - Compatibilidad con Hadoop y HDFS
  - Microsoft Connector for SAP BW

Para obtener una lista de los componentes de SSIS integrados que no se admiten actualmente, o que se admiten con determinadas limitaciones, vea [Limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md#components).

Para obtener más información sobre SSIS en Linux, vea los artículos siguientes:
-   [Entrada de blog donde se anuncia la compatibilidad de SSIS para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)
-   [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SQL Server Management Studio (SSMS)

Las siguientes limitaciones solo se aplican a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] en Windows conectado a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux.

- No se admiten los planes de mantenimiento.

- El almacén de administración de datos (MDW) y el recopilador de datos no se admiten en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. 

- Los componentes de la interfaz de usuario de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] que tienen opciones de autenticación de Windows o de registro de eventos de Windows no funcionan con Linux. Puede usar estas características con otras opciones, como inicios de sesión de SQL. 

- El número de archivos de registro que se conservarán no se puede modificar.

## <a name="next-steps"></a>Pasos siguientes

Para empezar, vea las siguientes guías de inicio rápido:

- [Instalación en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalación en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalación en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecución en Docker](quickstart-install-connect-ubuntu.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Ejecución y conexión: nube](quickstart-install-connect-clouds.md)

Para obtener respuestas a las preguntas más frecuentes, vea las [Preguntas más frecuentes sobre SQL Server en Linux](sql-server-linux-faq.md).
