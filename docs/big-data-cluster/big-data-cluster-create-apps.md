---
title: Implementación de aplicaciones mediante azdata
titleSuffix: SQL Server big data clusters
description: Implemente un script de Python o R como una [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]aplicación en.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 93c94b8ca5688bd5c67369849094e20d1dae697e
ms.sourcegitcommit: 77293fb1f303ccfd236db9c9041d2fb2f64bce42
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929720"
---
# <a name="how-to-deploy-an-app-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Cómo implementar una aplicación en[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo implementar y administrar scripts de R y Python como una aplicación dentro de un clúster de macrodatos SQL Server 2019.

## <a name="whats-new-and-improved"></a>Novedades y mejoras

- Una única utilidad de línea de comandos para administrar el clúster y la aplicación.
- Implementación simplificada de aplicaciones al tiempo que se proporciona un control granular sobre los archivos de especificación.
- Compatibilidad con el hospedaje de tipos de aplicación adicionales: SSIS y MLeap (novedad en CTP 2,3).
- [Visual Studio Code extensión](app-deployment-extension.md) para administrar la implementación de aplicaciones.

Las aplicaciones se implementan y administran mediante la utilidad de línea de comandos `azdata`. En este artículo se proporcionan ejemplos de cómo implementar aplicaciones desde la línea de comandos. Para obtener información sobre cómo usar esto en Visual Studio Code consulte [extensión de Visual Studio Code](app-deployment-extension.md).

Se admiten los siguientes tipos de aplicaciones:
- Aplicaciones de R y Python (funciones, modelos y aplicaciones)
- MLeap Serving
- SQL Server Integration Services (SSIS)

## <a name="prerequisites"></a>Requisitos previos

- [Clústeres de macrodatos de SQL Server 2019](deployment-guidance.md)
- [Utilidad de línea de comandos azdata](deploy-install-azdata.md)

## <a name="capabilities"></a>Capabilities

En SQL Server 2019 (versión preliminar), puede crear, eliminar, describir, inicializar, enumerar, ejecutar y actualizar la aplicación. En la tabla siguiente se describen los comandos de implementación de aplicaciones que puede usar con **azdata**.

|Comando |Descripción |
|:---|:---|
|`azdata login` | Iniciar sesión en un clúster de macrodatos SQL Server |
|`azdata app create` | Crear aplicación |
|`azdata app delete` | Eliminar aplicación |
|`azdata app describe` | Describir aplicación |
|`azdata app init` | Comenzar el esqueleto de una aplicación nueva |
|`azdata app list` | Enumerar aplicaciones |
|`azdata app run` | Ejecutar aplicación |
|`azdata app update`| Actualizar aplicación |

Puede obtener ayuda con el parámetro `--help`, como en el ejemplo siguiente:

```bash
azdata app create --help
```

En las siguientes secciones se describen estos comandos con más detalle.

## <a name="sign-in"></a>Iniciar sesión

Antes de implementar aplicaciones o interactuar con ellas, primero inicie sesión en el clúster de macrodatos de SQL Server con el comando `azdata login`. Especifique la dirección IP externa del servicio `controller-svc-external` (por ejemplo: `https://ip-address:30080`) junto con el nombre de usuario y la contraseña para el clúster.

```bash
azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
```

## <a name="aks"></a>AKS

Si usa AKS, debe ejecutar el siguiente comando en una ventana de bash o CMD para obtener la dirección IP del servicio `controller-svc-external`:


```bash
kubectl get svc controller-svc-external -n <name of your big data cluster>
```

## <a name="kubeadm-or-minikube"></a>Kubeadm o Minikube

Si usa Kubeadm o Minikube, ejecute el siguiente comando para obtener la dirección IP en la que iniciar sesión en el clúster.

```bash
kubectl get node --selector='node-role.kubernetes.io/master'
```

## <a name="create-an-app"></a>Crear una aplicación

Para crear una aplicación, use `azdata` con el comando `app create`. Estos archivos residen localmente en el equipo desde el que va a crear la aplicación.

Use la sintaxis siguiente para crear una nueva aplicación en el clúster de macrodatos:

```bash
azdata app create --spec <directory containing spec file>
```

El comando siguiente muestra un ejemplo de cómo podría ser este comando:

```bash
azdata app create --spec ./addpy
```

Se supone que la aplicación está almacenada en la carpeta `addpy`. Esta carpeta también debe contener un archivo de especificación para la aplicación, denominado `spec.yaml`. Consulte [la página de implementación de la aplicación](concept-application-deployment.md) para obtener `spec.yaml` más información sobre el archivo.

Para implementar esta aplicación de ejemplo, cree los archivos siguientes en un directorio denominado `addpy`:

- `add.py` Copie el siguiente código de Python en este archivo:
   ```py
   #add.py
  def add(x, y):
    result = x+y
    return result
  result=add(x,y)
   ```
- `spec.yaml` Copie el siguiente código en este archivo:
   ```yaml
   #spec.yaml
   name: add-app #name of your python script
   version: v1  #version of the app
   runtime: Python #the language this app uses (R or Python)
   src: ./add.py #full path to the location of the app
   entrypoint: add #the function that will be called upon execution
   replicas: 1  #number of replicas needed
   poolsize: 1  #the pool size that you need your app to scale
   inputs:  #input parameters that the app expects and the type
     x: int
     y: int
   output: #output parameter the app expects and the type
     result: int
   ```

A continuación, ejecute el siguiente comando:

```bash
azdata app create --spec ./addpy
```

Para comprobar si la aplicación se ha implementado, use el comando list:

```bash
azdata app list
```

Si la implementación no se ha completado, `state` debería mostrar `WaitingforCreate` como en el ejemplo siguiente:

```json
[
  {
    "name": "add-app",
    "state": "WaitingforCreate",
    "version": "v1"
  }
]
```

Una vez que la implementación se realiza correctamente, `state` debería cambiar al estado `Ready`:

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="list-an-app"></a>Enumerar una aplicación

El comando `app list` enumera las aplicaciones que se crearon correctamente.

El comando siguiente muestra todas las aplicaciones disponibles en el clúster de macrodatos:

```bash
azdata app list
```

Si especifica un nombre y una versión, se muestra la aplicación específica y su estado: Creating (en creación) o Ready (lista).

```bash
azdata app list --name <app_name> --version <app_version>
```

El ejemplo siguiente demuestra este comando:

```bash
azdata app list --name add-app --version v1
```

Debería ver una salida similar al ejemplo siguiente:

```json
[
  {
    "name": "add-app",
    "state": "Ready",
    "version": "v1"
  }
]
```

## <a name="run-an-app"></a>Ejecutar una aplicación

Si la aplicación está en un estado `Ready` y quiere usarla, puede ejecutar los parámetros de entrada especificados. Use la sintaxis siguiente para ejecutar una aplicación:

```bash
azdata app run --name <app_name> --version <app_version> --inputs <inputs_params>
```

El siguiente comando de ejemplo muestra el comando ejecutar:

```bash
azdata app run --name add-app --version v1 --inputs x=1,y=2
```

Si la ejecución se realiza correctamente, deberá ver la salida que se especificó al crear la aplicación. A continuación se muestra un ejemplo.

```json
{
  "changedFiles": [],
  "consoleOutput": "",
  "errorMessage": "",
  "outputFiles": {},
  "outputParameters": {
    "result": 3
  },
  "success": true
}
```

## <a name="create-an-app-skeleton"></a>Crear un esqueleto de aplicación

El comando init proporciona un scaffolding con los artefactos pertinentes necesarios para implementar una aplicación. En el ejemplo siguiente se crea Hello. Puede hacerlo con el siguiente comando.

```bash
azdata app init --name hello --version v1 --template python
```

Se creará una carpeta denominada Hello.  Puede usar el proceso `cd` en el directorio e inspeccionar los archivos generados en la carpeta. Spec. yaml define la aplicación, como el nombre, la versión y el código fuente. Puede editar las especificaciones para cambiar el nombre, la versión, la entrada y las salidas.

Este es un ejemplo de salida del comando init que verá en la carpeta:

```
hello.py
run-spec.yaml
spec.yaml
```

## <a name="describe-an-app"></a>Describir una aplicación

El comando describe proporciona información detallada sobre la aplicación, incluido el punto de conexión del clúster. Este comando lo suelen usar los desarrolladores de aplicaciones para compilar una aplicación con el cliente de Swagger y con el servicio WebService para interactuar con la aplicación de manera RESTful. Vea [Consumo de aplicaciones en clústeres de macrodatos](big-data-cluster-consume-apps.md) para obtener más información.

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30080/api/app/add-app/v1",
    "swagger": "https://10.1.1.3:30080/api/app/add-app/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

## <a name="delete-an-app"></a>Eliminar una aplicación

Para eliminar una aplicación del clúster de macrodatos, use la sintaxis siguiente:

```bash
azdata app delete --name add-app --version v1
```

## <a name="next-steps"></a>Pasos siguientes

Consulte cómo integrar aplicaciones implementadas [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en en sus propias aplicaciones en [consumir aplicaciones en clústeres de macrodatos](big-data-cluster-consume-apps.md) para obtener más información. También puede ver otros ejemplos en [Ejemplos de implementación de aplicaciones](https://aka.ms/sql-app-deploy).

Para obtener más información [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]acerca de, vea [¿Qué es [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
