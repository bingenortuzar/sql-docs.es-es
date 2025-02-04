---
title: Extensión de implementación de aplicaciones
titleSuffix: SQL Server big data clusters
description: Implemente un script de Python o R como una [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] aplicación en (versión preliminar).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 49a59650c406e3b48394da45ad0eeb4589fc4374
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653622"
---
# <a name="how-to-use-visual-studio-code-to-deploy-applications-to-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Cómo usar Visual Studio Code para implementar aplicaciones en[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo implementar aplicaciones en un SQL Server clúster de macrodatos con Microsoft Visual Studio código con la extensión de implementación de la aplicación. Esta capacidad se ha presentado en CTP 2.3. 

## <a name="prerequisites"></a>Requisitos previos

- [Visual Studio Code](https://code.visualstudio.com/)
- [SQL Server clúster de Big Data](big-data-cluster-overview.md) CTP 2,3 o posterior

## <a name="capabilities"></a>Capabilities

Esta extensión admite las siguientes tareas en Visual Studio Code:

- Autenticar en el clúster de macrodatos de SQL Server.
- Recuperar una plantilla de aplicación desde el repositorio de GitHub para la implementación de runtime admitidos.
- Administrar plantillas de aplicación abiertas actualmente en el área de trabajo del usuario.
- Implementar una aplicación mediante una especificación en formato YAML.
- Administrar aplicaciones implementadas en un clúster de macrodatos de SQL Server.
- Ver todas las aplicaciones que se han implementado en la barra lateral con información adicional.
- Generar una especificación de ejecución para consumir la aplicación o eliminarla del clúster.
- Consumir aplicaciones implementadas a través de una especificación de ejecución YAML.

En las secciones siguientes se explica el proceso de instalación y se proporciona información general sobre el funcionamiento de la extensión. 

### <a name="install"></a>Install

En primer lugar, instale la extensión de implementación de aplicaciones en Visual Studio Code:

1. Descargue la [extensión de implementación](https://aka.ms/app-deploy-vscode) de la aplicación para instalar la extensión como parte de Visual Studio Code.

1. Inicie Visual Studio Code y navegue hasta la barra lateral de extensiones.

1. Haga clic en el menú contextual `…` de la parte superior de la barra lateral y seleccione `Install from vsix`.

   ![Instalación de VSIX](media/vs-extension/install_vsix.png)

1. Busque el archivo `sqlservbdc-app-deploy.vsix` que ha descargado y selecciónelo para instalarlo.

Una vez instalada la extensión de implementación de la aplicación de clúster de Big Data SQL Server, se le pedirá que vuelva a cargar Visual Studio Code. Ahora debería ver el SQL Server el explorador de aplicaciones de BDC en la barra lateral Visual Studio Code.

### <a name="app-explorer"></a>Explorador de aplicaciones

Haga clic en la extensión de la barra lateral para cargar un panel lateral que muestra el explorador de aplicaciones. En la siguiente captura de pantalla de ejemplo del explorador de aplicaciones no se muestra ninguna aplicación ni especificación de aplicación como disponible:

![Explorador de aplicaciones](media/vs-extension/app_explorer.png)

#### <a name="connect-to-cluster"></a>Conexión al clúster

Para conectarse al punto de conexión del clúster, use uno de los métodos siguientes:

- Haga clic en la barra de estado de la parte inferior que indica `SQL Server BDC Disconnected`.
- O haga clic en el botón `Connect to Cluster` de la parte superior con la flecha que apunta a una puerta.

Visual Studio Code solicita el extremo, el nombre de usuario y la contraseña adecuados.

El extremo que se va a `Cluster Management Service` conectar es el punto de conexión con el puerto 30080.

También puede buscar este punto de conexión desde la línea de comandos hasta 

```
azdata bdc endpoint list
```

Una de las otras formas de obtener esta información es hacer clic con el botón secundario en **administrar** en el servidor en Azure Data Studio donde encontrará los puntos de conexión de los servicios enumerados.

![Punto final de ADS](media/vs-extension/ads_end_point.png)

Una vez que haya encontrado el extremo que se va a usar, conéctese al clúster.

![Nueva conexión](media/vs-extension/connect_to_cluster.png)

 Si tiene las credenciales correctas y el punto de conexión de la aplicación, Visual Studio Code le notifica que se ha conectado al clúster y que verá todas las aplicaciones implementadas que se hayan rellenado en la barra lateral. Si se conecta correctamente, el punto de conexión y el nombre de usuario se guardan en `./sqldbc` como parte del perfil de usuario. Nunca se guardan contraseñas ni tokens. Al volver a iniciar sesión, el símbolo del sistema se rellena previamente con el host y el nombre de usuario guardados, pero siempre hay que escribir una contraseña. Si quiere conectarse a otro punto de conexión del clúster, simplemente vuelva a hacer clic en `New Connection`. La conexión se cerrará automáticamente si cierra Visual Studio Code o si abre otro área de trabajo y necesita volver a conectarse.

### <a name="app-template"></a>Plantilla de aplicación

Debe abrir el *área de trabajo* en Visual Studio Code donde va a guardar los artefactos de la aplicación.

Para implementar una nueva aplicación a partir de alguna de las plantillas, haga clic en el botón `New App Template` del panel `App Specifications`, donde se le pide el nombre, el runtime y la ubicación en la que quiere colocar la nueva aplicación en el equipo local. El nombre y la versión que proporcione deben ser una etiqueta de DNS-1035 y deben constar de caracteres alfanuméricos en minúsculas o '-', empezar con un carácter alfabético y terminar con un carácter alfanumérico.

Se recomienda colocarlo en el área de trabajo Visual Studio Code actual para que pueda usar la funcionalidad completa de la extensión, pero puede colocarlo en cualquier lugar del sistema de archivos local.

![Plantilla de nueva aplicación](media/vs-extension/new_app_template.png)

Una vez hecho, se aplica scaffolding a una plantilla de nueva aplicación en la ubicación especificada y la implementación `spec.yaml` se abre en el área de trabajo. Si el directorio seleccionado está en el área de trabajo, también debería verse en el panel `App Specifications`:

![Plantilla de aplicación cargada](media/vs-extension/loading_app_template.png)

La plantilla es una aplicación `helloworld` sencilla que se dispone como se indica a continuación en el panel especificaciones de la aplicación:

- **spec.yaml**
   - Indica al clúster cómo implementar la aplicación
- **run-spec.yaml**
   - Indica al clúster cómo quiere denominar a la aplicación

El código fuente de la aplicación se encontraba en la carpeta del área de trabajo.

- **nombre del archivo de origen**
   - Este es el archivo de código fuente especificado por `src` en `spec.yaml`
   - Tiene una función denominada `handler` que se considera el `entrypoint` de la aplicación, como se muestra en `spec.yaml`. Toma una entrada de cadena denominada `msg` y devuelve una salida de cadena de nombre `out`. Se especifican en los elementos `inputs` y `outputs` de `spec.yaml`.

Si no quiere una plantilla con scaffolding y prefiere simplemente un `spec.yaml` para la implementación de una aplicación que ya ha compilado, haga clic en el botón `New Deploy Spec` situado junto al botón `New App Template` y siga el mismo proceso, aunque solo recibe el `spec.yaml`, que puede modificar como prefiera.

### <a name="deploy-app"></a>Implementar aplicación

Puede implementar esta aplicación al instante mediante el CodeLens `Deploy App` de `spec.yaml` o presionar el botón de carpeta de relámpago junto al archivo `spec.yaml` en el menú Especificaciones de la aplicación. La extensión descomprime todos los archivos del directorio donde se encuentra `spec.yaml` e implementa la aplicación en el clúster. 

>[!NOTE]
>Asegúrese de que todos los archivos de la aplicación están en el mismo directorio que `spec.yaml`. `spec.yaml` debe estar en el nivel raíz del directorio de código fuente de la aplicación. 

![Botón Implementar aplicación](media/vs-extension/deploy_app_lightning.png)

![CodeLens Implementar aplicación](media/vs-extension/deploy_app_codelens.png)

Se le notifica cuando la aplicación está lista para su consumo en función del estado de la aplicación en la barra lateral:

![Aplicación implementada](media/vs-extension/app_deploy.png)

![Barra lateral Aplicación lista](media/vs-extension/app_ready_side_bar.png)

![Notificación Aplicación lista](media/vs-extension/app_ready_notification.png)

En el panel lateral puede ver lo siguiente disponible:

Puede ver todas las aplicaciones que ha implementado en la barra lateral con la siguiente información:

- state
- version
- parámetros de entrada
- parámetros de salida
- vínculos
  - swagger
  - detalles

Si hace clic `Links`en, verá que puede acceder a la `swagger.json` aplicación implementada, para que pueda escribir sus propios clientes que llamen a la aplicación:

![Swagger](media/vs-extension/swagger.png)

Vea [Consumo de aplicaciones en clústeres de macrodatos](big-data-cluster-consume-apps.md) para obtener más información.

### <a name="app-run"></a>Ejecución de aplicación

Una vez que la aplicación esté lista, llámela con el `run-spec.yaml` proporcionado como parte de la plantilla de aplicación:

![Especificación de ejecución](media/vs-extension/run_spec.png)

Especifique cualquier cadena que quiera en lugar de `hello` y ejecútela de nuevo a través del vínculo de CodeLens o el botón de relámpago de la barra lateral junto a `run-spec.yaml`. Si, por algún motivo, no tiene una especificación de ejecución, genere una desde la aplicación implementada en el clúster:

![Obtención de especificación de ejecución](media/vs-extension/get_run_spec.png)

Una vez que tenga una y la haya editado a su entera satisfacción, ejecútela. Visual Studio Code devuelve la información adecuada cuando la aplicación ha terminado de ejecutarse:

![Salida de aplicación](media/vs-extension/app_output.png)

Como puede ver arriba, la salida se proporciona en un archivo `.json` temporal en el área de trabajo. Si quiere conservar esta salida, no dude en guardarla; de lo contrario, se elimina al cerrar. Si la aplicación no tiene ninguna salida para imprimir en un archivo, solo se obtiene la notificación `Successful App Run` en la parte inferior. Si no se ha producido una ejecución correcta, se recibe un mensaje de error adecuado que ayuda a determinar lo que está mal.

Al ejecutar una aplicación, hay varias maneras de pasar parámetros:

Puede especificar todas las entradas necesarias a través de un `.json`, es decir:

- `inputs: ./example.json`

Al llamar a una aplicación implementada, si algún parámetro de entrada es intrínseco de la aplicación o el usuario especificados y ese parámetro de entrada concreto es distinto de un primitivo, como una matriz, un vector, un dataframe, un JSON complejo, etc., especifique el tipo de parámetro directamente en línea cuando llame a la aplicación, es decir:

- Vector
    - `inputs:`
        - `x: [1, 2, 3]`
- Matriz
    - `inputs:`
        - `x: [[A,B,C],[1,2,3]]`
- Object
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

O proporcione una cadena como ruta de acceso de archivo relativa o absoluta a un `.txt`, `.json` o `.csv` que proporcione la entrada necesaria en el formato que requiera la aplicación. El análisis de archivos se basa en `Node.js Path library`, donde una ruta de acceso de archivo se define como `string that contains a / or \ character`.

Si el parámetro de entrada no se proporciona según lo necesario, se muestra un mensaje de error adecuado con la ruta de acceso de archivo incorrecta si se ha especificado una ruta de acceso de archivo de cadena o que indica que ese parámetro no es válido. La responsabilidad de asegurarse de que entiende los parámetros que define es del creador de la aplicación.

Para eliminar una aplicación, simplemente haga clic en el botón de papelera que se encuentra junto a la aplicación en el panel lateral `Deployed Apps`.

## <a name="next-steps"></a>Pasos siguientes

Consulte cómo integrar aplicaciones implementadas [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en en sus propias aplicaciones en [consumir aplicaciones en clústeres](big-data-cluster-consume-apps.md) de macrodatos para obtener más información. También puede ver los ejemplos adicionales de [Ejemplos de implementación de aplicaciones](https://aka.ms/sql-app-deploy) para probar la extensión.

Para obtener más información [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]acerca de, vea [¿Qué es [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).


Nuestro objetivo es que esta extensión le resulte útil y le agradecemos sus comentarios. Envíelos al [equipo de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](https://aka.ms/sqlfeedback).
