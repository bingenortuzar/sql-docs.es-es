---
title: Unión de SQL Server en Linux a Active Directory
titleSuffix: SQL Server
description: ''
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: d5cd6356f4bc691518f11e1e6fb00add527cc595
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68027343"
---
# <a name="join-sql-server-on-a-linux-host-to-an-active-directory-domain"></a>Unión de SQL Server en un host de Linux a un dominio de Active Directory

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se proporcionan instrucciones generales para unir un equipo host de Linux de SQL Server a un dominio de Active Directory (AD). Hay dos métodos: usar un paquete SSSD integrado o emplear proveedores ajenos de Active Directory. Ejemplos de productos de unión a dominio ajenos son [PowerBroker Identity Services (PBIS)](https://www.beyondtrust.com/), [One Identity](https://www.oneidentity.com/products/authentication-services/) y [Centrify](https://www.centrify.com/). En esta guía se incluyen los pasos necesarios para comprobar la configuración de Active Directory, aunque no está concebida para proporcionar instrucciones sobre cómo unir un equipo a un dominio cuando se usan utilidades de terceros.

## <a name="prerequisites"></a>Prerequisites

Antes de configurar la autenticación de Active Directory, debe configurar un controlador de dominio de Active Directory, Windows, en la red. Luego, una el host de SQL Server en Linux a un dominio de Active Directory.

> [!IMPORTANT]
> Los pasos de ejemplo de este artículo sirven solo como orientación. Los pasos reales pueden diferir ligeramente en cada entorno en función de cómo esté configurado el entorno global. Póngase en contacto con los administradores del sistema y del dominio del entorno para obtener información concreta de configuración, de personalización y de solución de problemas necesaria.

## <a name="check-the-connection-to-a-domain-controller"></a>Comprobación de la conexión a un controlador de dominio

Compruebe que puede ponerse en contacto con el controlador de dominio con los nombres corto y completo del dominio:

```bash
ping contoso
ping contoso.com
```

> [!TIP]
> En este tutorial se usan **contoso.com** y **CONTOSO.COM** como nombres de ejemplo de dominio y de dominio Kerberos, respectivamente. También se usa **DC1.CONTOSO.COM** como nombre de dominio completo de ejemplo del controlador de dominio. Debe reemplazar estos nombres por sus propios valores.

Si se produce un error en cualquiera de estas comprobaciones de nombre, actualice la lista de búsqueda de dominios. En las secciones siguientes se proporcionan instrucciones para Ubuntu, Red Hat Enterprise Linux (RHEL) y SUSE Linux Enterprise Server (SLES), respectivamente.

### <a name="ubuntu"></a>Ubuntu

1. Edite el archivo **/etc/network/interfaces** para que el dominio de Active Directory esté en la lista de búsqueda de dominios:

   ```/etc/network/interfaces
   # The primary network interface
   auto eth0
   iface eth0 inet dhcp
   dns-nameservers **<AD domain controller IP address>**
   dns-search **<AD domain name>**
   ```

   > [!NOTE]
   > La interfaz de red, `eth0`, puede diferir en los distintos equipos. Para averiguar cuál es la que está usando, ejecute **ifconfig**. Luego, copie la interfaz que tiene una dirección IP y bytes transmitidos y recibidos.

1. Después de editar este archivo, reinicie el servicio de red:

   ```bash
   sudo ifdown eth0 && sudo ifup eth0
   ```

1. Luego, compruebe que el archivo **/etc/resolv.conf** contiene una línea similar a la del ejemplo siguiente:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="rhel"></a>RHEL

1. Edite el archivo **/etc/sysconfig/network-scripts/ifcfg-eth0** para que el dominio de Active Directory esté en la lista de búsqueda de dominios. O bien edite otro archivo de configuración de interfaz según corresponda:

   ```/etc/sysconfig/network-scripts/ifcfg-eth0
   PEERDNS=no
   DNS1=**<AD domain controller IP address>**
   DOMAIN="contoso.com com"
   ```

1. Después de editar este archivo, reinicie el servicio de red:

   ```bash
   sudo systemctl restart network
   ```

1. Ahora compruebe que el archivo **/etc/resolv.conf** contiene una línea similar a la del ejemplo siguiente:

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

1. Si todavía no puede hacer ping al controlador de dominio, busque el nombre de dominio completo y la dirección IP del controlador de dominio. Un nombre de dominio de ejemplo es **DC1.CONTOSO.COM**. Agregue la siguiente entrada a **/etc/hosts**:

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

### <a name="sles"></a>SLES

1. Edite el archivo **/etc/sysconfig/network/config** para que la dirección IP del controlador de dominio de Active Directory se use para las consultas de DNS y el dominio de Active Directory esté en la lista de búsqueda de dominios:

   ```/etc/sysconfig/network/config
   NETCONFIG_DNS_STATIC_SEARCHLIST=""
   NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
   ```

1. Después de editar este archivo, reinicie el servicio de red:

   ```bash
   sudo systemctl restart network
   ```

1. Luego, compruebe que el archivo **/etc/resolv.conf** contiene una línea similar a la del ejemplo siguiente:

   ```/etc/resolv.conf
   search contoso.com com
   nameserver **<AD domain controller IP address>**
   ```

## <a name="join-to-the-ad-domain"></a>Unión al dominio de AD

Una vez comprobada la configuración básica y la conectividad con el controlador de dominio, existen dos opciones para unir un equipo host de Linux de SQL Server al controlador de dominio de Active Directory:

- [Opción 1: usar un paquete SSSD](#option1)
- [Opción 2: usar utilidades de proveedor de openldap de terceros](#option2)

### <a id="option1"></a> Opción 1: usar un paquete SSSD para unir a dominio de AD

Este método une el host de SQL Server a un dominio de AD mediante paquetes **realmd** y **sssd**.

> [!NOTE]
> Este es el método preferido para unir un host de Linux a un controlador de dominio de AD.

Siga los pasos siguientes para unir un host de SQL Server a un dominio de Active Directory:

1. Use [realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join) para unir el equipo host al dominio de AD. Primero debe instalar los paquetes de cliente **realmd** y Kerberos en el equipo host de SQL Server mediante el administrador de paquetes de la distribución de Linux:

   **RHEL:**

   ```base
   sudo yum install realmd krb5-workstation
   ```

   **SUSE:**

   ```bash
   sudo zypper install realmd krb5-client
   ```

   **Ubuntu:**

   ```bash
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. Si la instalación del paquete de cliente Kerberos solicita un nombre de dominio Kerberos, escriba el nombre de dominio en mayúsculas.

1. Después de confirmar que el DNS está configurado correctamente, una al dominio al ejecutar el siguiente comando. Debe autenticarse con una cuenta de AD que tenga privilegios suficientes en AD para unir un nuevo equipo al dominio. Este comando crea una nueva cuenta de equipo en AD, crea el archivo keytab de host **/etc/krb5.keytab**, configura el dominio en **/etc/sssd/sssd.conf** y actualiza **/etc/krb5.conf**.

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   ```

   Debería ver el mensaje: `Successfully enrolled machine in realm`.

   En la tabla siguiente se indican algunos mensajes de error que podría recibir, así como sugerencias para resolverlos:

   | Mensaje de error | Recomendación |
   |---|---|
   | `Necessary packages are not installed` | Instale esos paquetes mediante el administrador de paquetes de la distribución de Linux antes de volver a ejecutar el comando de unión de dominio Kerberos. |
   | `Insufficient permissions to join the domain` | Confirme con un administrador de dominio que dispone de permisos suficientes para unir equipos Linux al dominio. |
   | `KDC reply did not match expectations` | Es posible que no haya especificado el nombre de dominio Kerberos correcto del usuario. Los nombres de dominio Kerberos distinguen mayúsculas de minúsculas, normalmente mayúsculas, y se pueden identificar con el comando realm discover contoso.com. |

   SQL Server usa SSSD y NSS para asignar cuentas de usuario y grupos a identificadores de seguridad (SID). SSSD se debe configurar y ejecutar para que SQL Server cree inicios de sesión de AD correctamente. Normalmente, **realmd** lo hace automáticamente como parte de la unión al dominio, pero en algunos casos se debe hacer por separado.

   Para obtener más información, vea la [configuración manual de SSSD](https://access.redhat.com/articles/3023951) y la [configuración de NSS para funcionar con SSSD](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options).

1. Compruebe que ahora puede recopilar información sobre un usuario del dominio y que puede adquirir un vale Kerberos como ese usuario. En el ejemplo siguiente se usan los comandos **id**, [kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html) y [klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html) para eso.

   ```bash
   id user@contoso.com

   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM

   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   ```

   > [!NOTE]
   > - Si **id user@contoso.com** devuelve `No such user`, asegúrese de que el servicio SSSD se ha iniciado correctamente mediante la ejecución del comando `sudo systemctl status sssd`. Si el servicio se está ejecutando y sigue viendo el error, intente habilitar el registro detallado para SSSD. Para obtener más información, vea la documentación de Red Hat para [solucionar problemas de SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting).
   >
   > - Si **kinit user@CONTOSO.COM** devuelve `KDC reply did not match expectations while getting initial credentials`, asegúrese de que ha especificado el dominio Kerberos en mayúsculas.

Para obtener más información, vea la documentación de Red Hat para [detectar y unir dominios de identidad](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html).

### <a id="option2"></a> Opción 2: usar utilidades de proveedor de openldap de terceros

Puede usar utilidades de terceros como [PBIS](https://www.beyondtrust.com/), [VAS](https://www.oneidentity.com/products/authentication-services/) o [Centrify](https://www.centrify.com/). En este artículo no se consignan los pasos para cada utilidad individual. Antes de continuar, debe usar una de estas utilidades para unir el host de Linux para SQL Server al dominio.  

SQL Server no usa el código ni la biblioteca del integrador de terceros para las consultas relacionadas con AD. SQL Server siempre consulta AD mediante llamadas a la biblioteca openldap directamente en esta configuración. Los integradores de terceros solo se usan para unir el host de Linux al dominio de AD; SQL Server no tiene ninguna comunicación directa con estas utilidades.

> [!IMPORTANT]
> Vea las recomendaciones sobre el uso de la opción de configuración **mssql-conf** `network.disablesssd` en la sección **Opciones de configuración adicionales** del artículo [Usar la autenticación de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md#additionalconfig).

Compruebe que **/etc/krb5.conf** se ha configurado correctamente. En el caso de la mayoría de los proveedores de Active Directory ajenos, esta configuración se realiza automáticamente. No obstante, busque los siguientes valores en **/etc/krb5.conf** para evitar problemas futuros:

```/etc/krb5.conf
[libdefaults]
default_realm = CONTOSO.COM

[realms]
CONTOSO.COM = {
}

[domain_realm]
contoso.com = CONTOSO.COM
.contoso.com = CONTOSO.COM
```

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>Comprobar que el DNS inverso se ha configurado correctamente

El siguiente comando debe devolver el nombre de dominio completo (FQDN) del host que ejecuta SQL Server. Un ejemplo es **SqlHost.contoso.com**.

```bash
host **<IP address of SQL Server host>**
```

La salida de este comando debe ser similar a `**<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com`. Si este comando no devuelve el FQDN del host, o si el FQDN es incorrecto, agregue una entrada DNS inversa para el host de SQL Server en Linux al servidor DNS.

## <a name="next-steps"></a>Pasos siguientes

En este artículo se habla sobre el requisito previo de configurar una instancia de SQL Server en un equipo host de Linux con autenticación de Active Directory. Para terminar de configurar SQL Server en Linux de forma que admita cuentas de Active Directory, siga las instrucciones de [Usar la autenticación de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md).