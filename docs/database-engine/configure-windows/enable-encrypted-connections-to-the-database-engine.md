---
title: Habilitar conexiones cifradas en el motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2019
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- TLS [SQL Server]
- Transport Layer Security (TLS)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
- TLS certificates
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d8135706b5fa220fa4e62bbcaf9ad677681fe029
ms.sourcegitcommit: a24f6e12357979f1134a54a036ebc58049484a4f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314497"
---
# <a name="enable-encrypted-connections-to-the-database-engine"></a>Habilitar conexiones cifradas en el motor de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo habilitar conexiones cifradas para una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] mediante la especificación de un certificado para el [!INCLUDE[ssDE](../../includes/ssde-md.md)] utilizando el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El equipo servidor debe tener un certificado y el equipo cliente debe estar configurado para confiar en la entidad de certificación raíz del certificado. La puesta en servicio es el proceso de instalar un certificado mediante su importación en Windows.  
  
> [!IMPORTANT]
> A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], ya no se incluye Capa de sockets seguros (SSL). En su lugar use Seguridad de la capa de transporte (TLS).

## <a name="transport-layer-security-tls"></a>Seguridad de la capa de transporte (TLS)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede usar Seguridad de la capa de transporte (TLS) para cifrar los datos transmitidos a través de una red entre una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y una aplicación cliente. El cifrado TLS se realiza en la capa del protocolo y está disponible para todos los clientes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admitidos.
Se puede usar TLS para la validación del servidor cuando una conexión cliente solicita cifrado. Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en un equipo al que se ha asignado un certificado emitido por una entidad de certificación pública, la identidad del equipo y de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se certifica mediante la cadena de certificados que conducen a la entidad emisora raíz de confianza. Esta validación de servidor requiere que el equipo en el que se ejecuta la aplicación cliente se configure para confiar en la entidad emisora raíz del certificado que usa el servidor. Se permite el cifrado con un certificado autofirmado y se describe en la sección siguiente, aunque este tipo de certificado solo ofrece protección limitada.
El nivel de cifrado que se usa en TLS, de 40 o 128 bits, depende de la versión del sistema operativo Microsoft Windows que se ejecute en los equipos de la aplicación y de la base de datos.

> [!WARNING]
> El uso del nivel de cifrado de 40 bits se considera no seguro.

> [!WARNING]
> Las conexiones TLS cifradas mediante un certificado autofirmado no proporcionan una gran seguridad. Son susceptibles de ataques de tipo "Man-in-the-middle". No debe confiar en TLS con certificados autofirmados en un entorno de producción ni en servidores conectados a Internet.

Al habilitar el cifrado TLS aumenta la seguridad de los datos que se transmiten a través de redes entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las aplicaciones. Pero cuando todo el tráfico entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y una aplicación cliente se cifra mediante TLS, es necesario el procesamiento adicional siguiente:
-  Se requiere un recorrido de ida y vuelta de red adicional en el momento de la conexión.
-  Los paquetes enviados desde la aplicación a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los debe cifrar la pila TLS de cliente y los debe descifrar la pila TLS de servidor.
-  Los paquetes enviados desde la aplicación a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los debe cifrar la pila TLS de servidor y los debe descifrar la pila TLS de cliente.

## <a name="remarks"></a>Notas
 El certificado debe estar emitido para la **Autenticación de servidor**. El nombre del certificado debe ser el nombre de dominio completo (FQDN) del equipo.  
  
 Los certificados se almacenan localmente para los usuarios del equipo. Para instalar un certificado para usarlo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe ejecutar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una cuenta que tenga privilegios de administrador local.

 El cliente debe ser capaz de comprobar la propiedad del certificado utilizado por el servidor. Si el cliente tiene el certificado de clave pública de la entidad de certificación que firmó el certificado del servidor, no es necesario realizar una mayor configuración. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows incluye los certificados de clave pública de muchas entidades de certificación. Si el certificado del servidor lo firmó una entidad de certificación pública o privada para la que el cliente no tiene certificado de clave pública, debe instalar el certificado de clave pública de esta entidad de certificación.  
  
> [!NOTE]  
> Si desea utilizar el cifrado con un clúster de conmutación por error, debe instalar el certificado del servidor con el nombre DNS completo del servidor virtual en todos los nodos del clúster de conmutación por error. Por ejemplo, si tiene un clúster con dos nodos cuyos nombres son ***test1.\*\<su empresa>\*.com*** y ***test2.\*\<su empresa>\*.com***, y un servidor virtual llamado ***virtsql***, tendrá que instalar un certificado para ***virtsql.\*\<su empresa>\*.com*** en los dos nodos. Puede establecer el valor de la opción **ForceEncryption** en el cuadro de propiedades **Protocolos para virtsql** de **Configuración de red de SQL Server** en **Sí**.

> [!NOTE]
> Al crear conexiones cifradas para un indexador de Azure Search en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una máquina virtual de Azure, vea [Configuración de una conexión desde un indexador de Azure Search a SQL Server en una máquina virtual de Azure](https://azure.microsoft.com/documentation/articles/search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers/). 

## <a name="certificate-requirements"></a>Requisitos de certificado
Para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cargue un certificado TLS, el certificado debe cumplir las condiciones siguientes:

- El certificado debe estar en un almacén de certificados del equipo local o en el almacén de certificados del usuario actual.

- La cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener el permiso necesario para acceder al certificado TLS.

- La hora actual del sistema debe ser posterior al valor de la propiedad **Válido desde** del certificado y anterior a la propiedad Válido hasta del certificado.

- El certificado debe estar destinado a la autenticación del servidor. Para esto es necesario que la propiedad **Uso mejorado de clave** del certificado para especificar **Autenticación del servidor (1.3.6.1.5.5.7.3.1)** .

- El certificado se debe crear mediante la opción **KeySpec** de **AT_KEYEXCHANGE**. Por lo general, la propiedad de uso de clave del certificado (**KEY_USAGE**) incluye también el cifrado de clave (**CERT_KEY_ENCIPHERMENT_KEY_USAGE**).

- La propiedad **Asunto** del certificado debe indicar que el nombre común (CN) es el mismo que el nombre del host o nombre de dominio completo (FQDN) del servidor. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en un clúster de conmutación por error, el nombre común debe coincidir con el del host o FQDN del servidor virtual, y los certificados se deben aprovisionar en todos los nodos del clúster de conmutación por error.

- [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] y [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] Native Client (SNAC) admiten los certificados comodín. SNAC ha quedado en desuso y se ha reemplazado por [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) y [Microsoft ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md). Es posible que otros clientes no admitan los certificados comodín. Para más información, vea la documentación del cliente y [KB 258858](http://support.microsoft.com/kb/258858).       
  El certificado comodín no se puede seleccionar con el Administrador de configuración de SQL Server. Para usar un certificado comodín, debe editar la clave del Registro `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQLServer\SuperSocketNetLib` y escribir la huella digital del certificado, sin espacios en blanco, en el valor **Certificado**.  

  > [!WARNING]  
  > [!INCLUDE[ssnoteregistry_md](../../includes/ssnoteregistry-md.md)]  

## <a name="to-provision-install-a-certificate-on-a-single-server"></a>Para aprovisionar (instalar) un certificado en un solo servidor  
Con [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], la administración de certificados se integra en el Administrador de configuración de SQL Server. Administrador de configuración de SQL Server para [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] se puede usar con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Vea [Administración de certificados (Administrador de configuración de SQL Server)](../../database-engine/configure-windows/manage-certificates.md) para agregar un certificado a una única instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Si usa [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], y Administrador de configuración de SQL Server para [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] no está disponible, siga estos pasos:

1. En el menú **Inicio** , haga clic en **Ejecutar**; en el cuadro **Abrir** , escriba **MMC** y haga clic en **Aceptar**.  
  
2. En el menú **Archivo** de la consola MMC, haga clic en **Agregar o quitar complemento**.  
  
3. En el cuadro de diálogo **Agregar o quitar complemento** , haga clic en **Agregar**.  
  
4. En el cuadro de diálogo **Agregar un complemento independiente** , haga clic en **Certificados**y, después, en **Agregar**.  
  
5. En el cuadro de diálogo **Complemento de certificados** , haga clic en **Cuenta de equipo**y, después, en **Finalizar**.  
  
6. En el cuadro de diálogo **Agregar un complemento independiente** , haga clic en **Cerrar.**  
  
7. En el cuadro de diálogo **Agregar o quitar complemento** , haga clic en **Aceptar**.  
  
8. En el complemento **Certificados** , expanda **Certificados**, expanda **Personal**. Tras ello, haga clic con el botón derecho en **Certificados**, seleccione **Todas las tareas**y, finalmente, haga clic en **Importar**.  

9. Haga clic con el botón derecho en el certificado importado, seleccione **Todas las tareas**y, luego, haga clic en **Administrar claves privadas**. En el cuadro de diálogo **Seguridad**, agregue el permiso de lectura para la cuenta de usuario que usa la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
10. Finalice el **Asistente para importación de certificados**para agregar un certificado al equipo y cierre la consola MMC. Para obtener más información acerca de cómo agregar un certificado a un equipo, vea la documentación de Windows.  
  
## <a name="to-provision-install-a-certificate-across-multiple-servers"></a>Para aprovisionar (instalar) un certificado en varios servidores
Con [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], la administración de certificados se integra en el Administrador de configuración de SQL Server. Administrador de configuración de SQL Server para [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] se puede usar con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Consulte [Administración de certificados (Administrador de configuración de SQL Server)](../../database-engine/configure-windows/manage-certificates.md) para agregar un certificado en una configuración de clúster de conmutación por error o de grupo de disponibilidad.

Si usa [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], y Administrador de configuración de SQL Server para no está disponible para [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], siga los pasos de la sección [Para aprovisionar (instalar) un certificado en un solo servidor](#to-provision-install-a-certificate-on-a-single-server) para cada servidor.

## <a name="to-export-the-server-certificate"></a>Para exportar el certificado del servidor  
  
1. En el complemento **Certificados** , busque el certificado en la carpeta **Certificados** / **Personal** , haga clic con el botón secundario en **Certificado**, seleccione **Todas las tareas**y, a continuación, en **Exportar**.  
  
2. Complete el **Asistente para exportación de certificados**y guarde el archivo del certificado en una ubicación adecuada.  
  
## <a name="to-configure-the-server-to-force-encrypted-connections"></a>Para configurar el servidor para forzar conexiones cifradas

> [!IMPORTANT]
> La cuenta de servicio de SQL Server debe tener permisos de lectura en el certificado que se usa para forzar el cifrado en el servidor de SQL Server. En el caso de una cuenta de servicio sin privilegios, será necesario agregar permisos de lectura al certificado. Si no lo hace, se puede producir un error en el reinicio del servicio SQL Server.
  
1. En **Administrador de configuración de SQL Server**, expanda **Configuración de red de SQL Server**, haga clic con el botón derecho en **Protocolos de** _\<instancia de servidor>_ y, después, seleccione **Propiedades**.  
  
2. En el cuadro de diálogo **Protocolos de** _\<nombre de instancia>_ **Propiedades**, en la pestaña **Certificado**, seleccione el certificado que quiera en el menú desplegable del cuadro **Certificado** y, después, haga clic en **Aceptar**.  
  
3. En la pestaña **Marcas** , en el cuadro **ForceEncryption** , seleccione **Sí**y, a continuación, haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
4. Reinicie el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

> [!NOTE]
> Para garantizar que la conectividad entre el cliente y el servidor es segura, configure el cliente para que solicite conexiones cifradas. Se explican más detalles [más adelante en este artículo](#to-configure-the-client-to-request-encrypted-connections).

## <a name="to-configure-the-client-to-request-encrypted-connections"></a>Para configurar el cliente de modo que solicite conexiones cifradas  

1. Copie el certificado original o el archivo del certificado exportado en el equipo cliente.  
  
2. En el equipo cliente, use el complemento **Certificados** para instalar el certificado raíz o el archivo del certificado exportado.  
  
3. En el Administrador de configuración de SQL Server, haga clic con el botón derecho en **Configuración de SQL Server Native Client** y, después, haga clic en **Propiedades**.  
  
4. En la página **Marcas** , en el cuadro **Forzar cifrado de protocolo** , haga clic en **Sí**.  
  
## <a name="to-encrypt-a-connection-from-sql-server-management-studio"></a>Para cifrar una conexión desde SQL Server Management Studio  
  
1. En la barra de herramientas del Explorador de objetos, haga clic en **Conectar**y, a continuación, en **Motor de base de datos**.  
  
2. En el cuadro de diálogo **Conectar al servidor** , rellene la información de conexión y, a continuación, haga clic en **Opciones**.  
  
3. En la pestaña **Propiedades de conexión** , haga clic en **Cifrar conexión**.  

## <a name="internet-protocol-security-ipsec"></a>Protocolo de seguridad de Internet (IPSec)
Los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se pueden cifrar durante la transmisión mediante IPSec. Los sistemas operativos del cliente y del servidor proporcionan IPSec, que no requiere configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información sobre IPSec, vea la documentación de Windows o de la red.

## <a name="see-also"></a>Consulte también
[Soporte de TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/kb/3135244)     
[Configuración de Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)     
[Cifrado de SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md)
