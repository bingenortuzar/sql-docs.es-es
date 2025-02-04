---
title: Puntuación en tiempo real mediante el procedimiento almacenado sp_rxPredict
description: Generar predicciones mediante sp_rxPredict, puntuar las entradas de datos en un modelo entrenado previamente escrito en R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/26/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 26701ac6e538d195a5a85ad66af9578848889d23
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715646"
---
# <a name="real-time-scoring-with-sprxpredict-in-sql-server-machine-learning"></a>Puntuación en tiempo real con sp_rxPredict en SQL Server machine learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La puntuación en tiempo real usa el procedimiento almacenado del sistema [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) y las capacidades de extensión de CLR en SQL Server para las predicciones o puntuaciones de alto rendimiento en las cargas de trabajo de predicción. La puntuación en tiempo real es independiente del lenguaje y se ejecuta sin dependencias en los tiempos de ejecución de R o Python. Suponiendo que un modelo se ha creado y entrenado con las funciones de Microsoft y, a continuación, se ha serializado a un formato binario en SQL Server, puede usar la puntuación en tiempo real para generar resultados previstos en nuevas entradas de datos en SQL Server instancias que no tienen el complemento de R o Python instalación.

## <a name="how-real-time-scoring-works"></a>Cómo funciona la puntuación en tiempo real

La puntuación en tiempo real se admite en tipos de modelo específicos basados en funciones RevoScaleR o MicrosoftML como [rxLinMod (RevoScaleR)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)[rxNeuralNet (MicrosoftML)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet). Usa bibliotecas nativas C++ para generar puntuaciones, en función de la entrada del usuario que se proporciona a un modelo de aprendizaje automático almacenado en un formato binario especial.

Dado que un modelo entrenado se puede usar para puntuar sin tener que llamar a un entorno de tiempo de ejecución de lenguaje externo, se reduce la sobrecarga de varios procesos. Esto admite un rendimiento de predicción mucho más rápido para escenarios de puntuación de producción. Dado que los datos nunca salen SQL Server, los resultados se pueden generar e insertar en una nueva tabla sin ninguna conversión de datos entre R y SQL.

La puntuación en tiempo real es un proceso de varios pasos:

1. El procedimiento almacenado que realiza la puntuación debe habilitarse en cada base de datos.
2. Cargue el modelo previamente entrenado en formato binario.
3. Se proporcionan nuevos datos de entrada que se van a puntuar, ya sea tabular o filas individuales, como entrada para el modelo.
4. Para generar puntuaciones, llame al procedimiento almacenado [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) .

## <a name="prerequisites"></a>Requisitos previos

+ [Habilitar la integración de CLR SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ [Habilitar la puntuación en tiempo real](#bkmk_enableRtScoring).

+ El modelo se debe entrenar de antemano con uno de los algoritmos **RX** admitidos. Para R, la puntuación en tiempo real `sp_rxPredict` con funciona con [algoritmos compatibles con RevoScaleR y MicrosoftML](#bkmk_rt_supported_algos). Para Python, consulte [algoritmos admitidos de revoscalepy y microsoftml](#bkmk_py_supported_algos)

+ Serialice el modelo con [rxSerialize](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) para R y [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para Python. Estas funciones de serialización se han optimizado para admitir la puntuación rápida.

+ Guarde el modelo en la instancia del motor de base de datos de la que desea llamarlo. No es necesario que esta instancia tenga la extensión en tiempo de ejecución de R o Python.

> [!Note]
> La puntuación en tiempo real está optimizada actualmente para predicciones rápidas en conjuntos de datos más pequeños, que van desde unas pocas filas hasta cientos de miles de filas. En los grandes conjuntos de datos, el uso de [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) puede ser más rápido.

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>Algoritmos admitidos

### <a name="python-algorithms-using-real-time-scoring"></a>Algoritmos de Python con puntuación en tiempo real

+ modelos revoscalepy

  + [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  Los modelos marcados con \* también admiten la puntuación nativa con la función PREDICT.

+ modelos microsoftml

  + [rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ Transformaciones proporcionadas por microsoftml

  + [featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash)


<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>Algoritmos de R con puntuación en tiempo real

+ Modelos RevoScaleR

  + [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  Los modelos marcados con \* también admiten la puntuación nativa con la función PREDICT.

+ Modelos MicrosoftML

  + [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ Transformaciones proporcionadas por MicrosoftML

  + [featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>Tipos de modelo no admitidos

La puntuación en tiempo real no utiliza un intérprete; por lo tanto, no se admiten las funciones que puedan requerir un intérprete durante el paso de puntuación.  Entre ellas se incluyen:

  + No se admiten `rxNaiveBayes` los modelos que usan los `rxGlm` algoritmos o.

  + Los modelos que usan una función de transformación o una fórmula que contiene <code>A ~ log(B)</code> una transformación, como, no se admiten en la puntuación en tiempo real. Para usar un modelo de este tipo, se recomienda realizar la transformación en los datos de entrada antes de pasar los datos a la puntuación en tiempo real.


## <a name="example-sprxpredict"></a>Ejemplo: sp_rxPredict

En esta sección se describen los pasos necesarios para configurar la predicción en **tiempo real** y se ofrece un ejemplo de cómo llamar a la función desde T-SQL.

<a name ="bkmk_enableRtScoring"></a> 

### <a name="step-1-enable-the-real-time-scoring-procedure"></a>Paso 1. Habilitar el procedimiento de puntuación en tiempo real

Debe habilitar esta característica para cada base de datos que desee usar para la puntuación. El administrador del servidor debe ejecutar la utilidad de línea de comandos, RegisterRExt. exe, que se incluye con el paquete RevoScaleR.

> [!NOTE]
> Para que la puntuación en tiempo real funcione, debe habilitarse la funcionalidad de SQL CLR en la instancia de; Además, la base de datos debe estar marcada como de confianza. Al ejecutar el script, estas acciones se realizan automáticamente. Sin embargo, tenga en cuenta las implicaciones de seguridad adicionales antes de hacerlo.

1. Abra un símbolo del sistema con privilegios elevados y navegue hasta la carpeta donde se encuentra RegisterRExt. exe. La siguiente ruta de acceso se puede usar en una instalación predeterminada:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Ejecute el siguiente comando, sustituyendo el nombre de la instancia de y la base de datos de destino donde desea habilitar los procedimientos almacenados extendidos:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Por ejemplo, para agregar el procedimiento almacenado extendido a la base de datos CLRPredict en la instancia predeterminada, escriba:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    El nombre de instancia es opcional si la base de datos está en la instancia predeterminada. Si usa una instancia con nombre, debe especificar el nombre de la instancia.

3. RegisterRExt. exe crea los siguientes objetos:

    + Ensamblados de confianza
    + El procedimiento almacenado`sp_rxPredict`
    + Un nuevo rol de base `rxpredict_users`de datos,. El administrador de bases de datos puede usar este rol para conceder permiso a los usuarios que usan la funcionalidad de puntuación en tiempo real.

4. Agregue los usuarios que necesiten ejecutar `sp_rxPredict` al nuevo rol.

> [!NOTE]
> 
> En SQL Server 2017, se aplican medidas de seguridad adicionales para evitar problemas con la integración de CLR. Estas medidas imponen restricciones adicionales sobre el uso de este procedimiento almacenado. 

### <a name="step-2-prepare-and-save-the-model"></a>Paso 2. Preparar y guardar el modelo

El formato binario requerido por\_SP rxPredict es el mismo que el formato necesario para utilizar la función PREDICT. Por lo tanto, en el código de R, incluya una llamada a [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)y asegúrese de `realtimeScoringOnly = TRUE`especificar, como en este ejemplo:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>Paso 3. Llamar a sp_rxPredict

Llame a SP\_rxPredict como lo haría con cualquier otro procedimiento almacenado. En la versión actual, el procedimiento almacenado solo toma dos parámetros:  _\@el modelo_ del modelo en formato binario y  _\@inputData_ para los datos que se van a usar en la puntuación, definidos como una consulta SQL válida.

Dado que el formato binario es el mismo que utiliza la función PREDICT, puede usar los modelos y la tabla de datos del ejemplo anterior.

```sql
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> Se produce un error\_en la llamada a SP rxPredict si los datos de entrada para la puntuación no incluyen columnas que coincidan con los requisitos del modelo. Actualmente, solo se admiten los siguientes tipos de datos de .NET: Double, Float, Short, ushort, Long, ulong y String.
> 
> Por lo tanto, es posible que tenga que filtrar los tipos no admitidos en los datos de entrada antes de usarlo para la puntuación en tiempo real.
> 
> Para obtener información sobre los tipos SQL correspondientes, consulte [asignación de tipos de SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [asignación de datos de parámetros CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-real-time-scoring"></a>Deshabilitar la puntuación en tiempo real

Para deshabilitar la funcionalidad de puntuación en tiempo real, abra un símbolo del sistema con privilegios elevados y ejecute el siguiente comando:`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la puntuación en SQL Server, consulte [Cómo generar predicciones en SQL Server machine learning](r/how-to-do-realtime-scoring.md).
