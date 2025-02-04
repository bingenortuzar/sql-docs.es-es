---
title: Preparar los datos de seguimiento de entrada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: c14fd3d2-5770-47c2-a851-cc13ddbc9bf5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7af5d166ec3bc059bc2628512564d92fd4cc6cad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149989"
---
# <a name="prepare-the-input-trace-data"></a>Preparar los datos de seguimiento de entrada
  Para poder iniciar una repetición distribuida con la característica Distributed Replay de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , debe preparar la información de seguimiento de entrada iniciando la fase de preprocesamiento desde la herramienta de administración de reproducción distribuida. En la fase de preprocesamiento, el controlador de reproducción distribuida procesa la información de seguimiento y genera un archivo intermedio:  
  
 ![Fase de preproceso de Distributed replay](../../database-engine/media/preprocess.gif "fase de preproceso de Distributed replay")  
  
 Para obtener más información sobre la fase de preprocesamiento, vea [SQL Server Distributed Replay](sql-server-distributed-replay.md).  
  
> [!NOTE]  
>  Los datos de seguimiento de entrada se deben capturar en una versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatible con Distributed Replay. Los datos de seguimiento de entrada también deben ser compatibles con el servidor de destino con el que se desea reproducir los datos de seguimiento. Para obtener más información acerca de los requisitos de versión, vea [Distributed Replay Requirements](distributed-replay-requirements.md).  
  
### <a name="to-prepare-the-input-trace-data"></a>Para preparar la información de seguimiento de entrada  
  
1.  **(Opcional) Modificar opciones de configuración de preproceso**: Si desea modificar la configuración de preprocesamiento, por ejemplo, si para filtrar las sesiones del sistema o para configurar el tiempo de inactividad máximo, debe modificar el `<PreprocessModifiers>` elemento del archivo de configuración de preprocesamiento basado en XML, `DReplay.exe.preprocess.config`. Si modifica el archivo de configuración de preprocesamiento, se recomienda que modifique una copia en vez del original. Para modificar los valores de configuración, siga estos pasos:  
  
    1.  Haga una copia del archivo de configuración de preprocesamiento predeterminado, `DReplay.exe.preprocess.config`, y cambie el nombre del nuevo archivo. El archivo de configuración de preprocesamiento predeterminado se encuentra en la carpeta de instalación de la herramienta de administración.  
  
    2.  Modifique los valores de configuración de preprocesamiento en el nuevo archivo de configuración.  
  
    3.  Cuando se inicie la fase de preprocesamiento (el paso siguiente), use el parámetro *config_file* de la opción **preprocess** para especificar la ubicación del archivo de configuración modificado.  
  
     Para obtener más información sobre el archivo de configuración de preprocesamiento, vea [Configurar Distributed Replay](configure-distributed-replay.md).  
  
2.  **Iniciar la fase de preprocesamiento**: Para preparar los datos de seguimiento de entrada, debe ejecutar la herramienta de administración con el **preprocesar** opción. Para obtener más información, vea [Opción de preprocesamiento &#40;herramienta de administración Distributed Replay&#41;](preprocess-option-distributed-replay-administration-tool.md).  
  
    1.  Abra la utilidad de símbolo del sistema de Windows (`CMD.exe`) y navegue hasta la ubicación de instalación de la herramienta de administración de Distributed Replay (`DReplay.exe`).  
  
    2.  (Opcional) Use el parámetro *controller* , **-m**, para especificar el controlador, si el servicio del controlador se está ejecutando en un equipo diferente al de la herramienta de administración.  
  
    3.  Use el parámetro *input_trace_file* , **-i**, para especificar la ubicación y nombre de los archivos de seguimiento de entrada.  
  
    4.  Use el parámetro *controller_working_directory* , **-d**, para especificar dónde se debe guardar el archivo intermedio en el controlador.  
  
    5.  (Opcional) Use el parámetro *config_file* , **-c**, para especificar la ubicación del archivo de configuración de preprocesamiento. Use este parámetro para apuntar al nuevo archivo de configuración su ha modificado una copia del archivo de configuración de preprocesamiento predeterminado.  
  
    6.  (Opcional) Use el parámetro *status_interval* , **-f**, para especificar si quiere que la herramienta de administración muestre los mensajes de estado con una frecuencia distinta de 30 segundos.  
  
     Por ejemplo, al iniciar la fase de preprocesamiento en el mismo equipo que el servicio de controlador, para un archivo de seguimiento ubicado en `c:\trace1.trc`, un directorio de trabajo del controlador que se encuentra en `c:\WorkingDir` , y un mensaje de estado que se muestra en el valor predeterminado de 30 segundos, requiere la sintaxis: `dreplay preprocess -i c:\trace1.trc -d c:\WorkingDir`  
  
3.  Una vez completada la fase de preprocesamiento, el archivo intermedio se almacena en el directorio de trabajo del controlador. Para iniciar la fase de reproducción de eventos, debe ejecutar la herramienta de administración con la opción **replay** . Para obtener más información, vea [Reproducir datos de seguimiento](replay-trace-data.md).  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [Distributed Replay Requirements](distributed-replay-requirements.md)   
 [Opciones de línea de comandos de la herramienta de administración &#40;utilidad Distributed Replay&#41;](administration-tool-command-line-options-distributed-replay-utility.md)   
 [Configurar Distributed Replay](configure-distributed-replay.md)  
  
  
