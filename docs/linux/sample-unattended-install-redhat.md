---
title: Instalación desatendida para SQL Server en Red Hat Enterprise Linux
titleSuffix: SQL Server
description: 'Ejemplo de script de SQL Server: instalación desatendida en Red Hat Enterprise Linux'
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 696ba88a9f2d5f29de8dc3afb45af8c392f2de68
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "67910446"
---
# <a name="sample-unattended-sql-server-installation-script-for-red-hat-enterprise-linux"></a>Ejemplo: Script de instalación desatendida de SQL Server para Red Hat Enterprise Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este script de Bash de ejemplo instala SQL Server 2017 en Red Hat Enterprise Linux (RHEL) sin entrada interactiva. Proporciona ejemplos de instalación del motor de base de datos, las herramientas de línea de comandos de SQL Server, el Agente SQL Server y realiza los pasos posteriores a la instalación. Opcionalmente, puede instalar la búsqueda de texto completo y crear un usuario administrativo.

> [!TIP]
> Si no necesita un script de instalación desatendida, la manera más rápida de instalar SQL Server es seguir la [guía de inicio rápido para Red Hat.](quickstart-install-connect-red-hat.md) Para obtener más información sobre la instalación, consulte la [guía de instalación de SQL Server en Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Prerequisites

- Necesita al menos 2 GB de memoria para ejecutar SQL Server en Linux.
- El sistema de archivos debe ser **XFS** o **EXT4**. No se admiten otros sistemas de archivos, como **BTRFS**.
- Para conocer otros requisitos del sistema, consulte [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a name="sample-script"></a>Script de ejemplo
Guarde el script de ejemplo en un archivo y, después, para personalizarlo, reemplace los valores de las variables en el script. También puede establecer cualquiera de las variables de scripting como variables de entorno, siempre que las quite del archivo de script.

```bash
#!/bin/bash -e

# Use the following variables to control your install:

# Password for the SA user (required)
MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'

# Product ID of the version of SQL server you're installing
# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key
# Defaults to developer
MSSQL_PID='evaluation'

# Install SQL Server Agent (recommended)
SQL_ENABLE_AGENT='y'

# Install SQL Server Full Text Search (optional)
# SQL_INSTALL_FULLTEXT='y'

# Create an additional user with sysadmin privileges (optional)
# SQL_INSTALL_USER='<Username>'
# SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'

if [ -z $MSSQL_SA_PASSWORD ]
then
  echo Environment variable MSSQL_SA_PASSWORD must be set for unattended install
  exit 1
fi

echo Adding Microsoft repositories...
sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo

echo Installing SQL Server...
sudo yum install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y yum install -y mssql-tools unixODBC-devel

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc

# Optional Enable SQL Server Agent :
if [ ! -z $SQL_ENABLE_AGENT ]
then
  echo Enable SQL Server Agent...
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo yum install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring firewall to allow traffic on port 1433...
sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
sudo firewall-cmd --reload

# Example of setting post-installation configuration options
# Set trace flags 1204 and 1222 for deadlock tracing:
#echo Setting trace flags...
#sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

# Restart SQL Server after making configuration changes:
echo Restarting SQL Server...
sudo systemctl restart mssql-server

# Connect to server and get the version:
counter=1
errstatus=1
while [ $counter -le 5 ] && [ $errstatus = 1 ]
do
  echo Waiting for SQL Server to start...
  sleep 5s
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "SELECT @@VERSION" 2>/dev/null
  errstatus=$?
  ((counter++))
done

# Display error if connection failed:
if [ $errstatus = 1 ]
then
  echo Cannot connect to SQL Server, installation aborted
  exit $errstatus
fi

# Optional new user creation:
if [ ! -z $SQL_INSTALL_USER ] && [ ! -z $SQL_INSTALL_USER_PASSWORD ]
then
  echo Creating user $SQL_INSTALL_USER
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "CREATE LOGIN [$SQL_INSTALL_USER] WITH PASSWORD=N'$SQL_INSTALL_USER_PASSWORD', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=ON, CHECK_POLICY=ON; ALTER SERVER ROLE [sysadmin] ADD MEMBER [$SQL_INSTALL_USER]"
fi

echo Done!
```

## <a name="running-the-script"></a>Ejecución del script

Para ejecutar el script

1. Pegue el ejemplo en el editor de texto que prefiera y guárdelo con un nombre fácil de recordar, como `install_sql.sh`.

1. Personalice `MSSQL_SA_PASSWORD`, `MSSQL_PID` y cualquiera de las demás variables que quiera cambiar.

1. Marque el script como ejecutable.

   ```bash
   chmod +x install_sql.sh
   ```

1. Ejecute el script.

   ```bash
   ./install_sql.sh
   ```

## <a name="understanding-the-script"></a>Descripción del script

Lo primero que hace el script de Bash es establecer algunas variables.  Pueden ser variables de scripting, como en el ejemplo, o variables de entorno.  La variable `MSSQL_SA_PASSWORD` es **necesaria** para la instalación de SQL Server, las demás son variables personalizadas creadas para el script.  Este script de ejemplo realiza los siguientes pasos:

1. Importar las claves públicas de Microsoft GPG

1. Registrar los repositorios de Microsoft para SQL Server y las herramientas de línea de comandos

1. Actualizar los repositorios locales

1. Instalar SQL Server

1. Configurar SQL Server con ```MSSQL_SA_PASSWORD``` y aceptar automáticamente el contrato de licencia para el usuario final

1. Aceptar automáticamente el contrato de licencia para el usuario final para las herramientas de línea de comandos de SQL Server, instalarlas e instalar el paquete unixODBC-dev

1. Agregar las herramientas de línea de comandos de SQL Server a la ruta de acceso para facilitar su uso

1. Instalar el Agente SQL Server si se establece la variable de scripting ```SQL_INSTALL_AGENT```, activada de forma predeterminada

1. Opcionalmente, instalar Búsqueda de texto completo de SQL Server, si está establecida la variable ```SQL_INSTALL_FULLTEXT```

1. Desbloquear el puerto 1433 para TCP en el firewall del sistema, necesario para conectarse a SQL Server desde otro sistema

1. Opcionalmente, establecer marcas de seguimiento para el seguimiento del interbloqueo (requiere quitar marca de comentario de las líneas)

1. SQL Server ya está instalado; para que sea operativo, reinicie el proceso.

1. Compruebe que SQL Server está instalado correctamente y oculte los mensajes de error.

1. Cree un nuevo usuario de administrador del servidor si están establecidos ```SQL_INSTALL_USER``` y ```SQL_INSTALL_USER_PASSWORD```.

## <a name="next-steps"></a>Pasos siguientes

Simplifique varias instalaciones desatendidas y cree un script de Bash independiente que establezca las variables de entorno adecuadas.  Puede quitar cualquiera de las variables que usa el script de ejemplo y colocarlas en su propio script de Bash.

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

Después, ejecute el script de Bash de la siguiente manera:
```bash
. ./my_script_name.sh
```

Para obtener más información sobre SQL Server en Linux, vea [Introducción a SQL Server en Linux](sql-server-linux-overview.md).
