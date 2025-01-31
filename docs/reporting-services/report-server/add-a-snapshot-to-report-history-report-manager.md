---
title: 'Agregar una instantánea al historial de informes: Reporting Services | Microsoft Docs'
ms.prod: reporting-services
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 06/26/2019
ms.openlocfilehash: 2ada64f14c3564bd1e6c9846f890fdd8b287cb6f
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68251935"
---
# <a name="add-a-snapshot-to-report-history"></a>Agregar una instantánea al historial de informes

El historial de informes es un conjunto de instantáneas de informe que se crean a lo largo del tiempo. Una instantánea de informe es un informe que contiene información de diseño y resultados de consultas que se recuperaron en un momento concreto. A diferencia de los informes a petición, que obtienen resultados de consulta actualizados cuando se seleccionan, las instantáneas de informe se procesan según una programación y luego se guardan en un servidor de informes. Al seleccionar una instantánea de informe para su visualización, el servidor de informes recupera el informe almacenado en la base de datos del servidor de informes y muestra los datos y el diseño actualizados para el informe en el momento en que se creó la instantánea.  
  
Las instantáneas de informe no se guardan con un formato de representación concreto. En su lugar, las instantáneas de informe se representan en un formato de visualización final (como HTML) solo cuando un usuario o una aplicación lo solicita. La representación aplazada hace que las instantáneas sean portátiles. El informe se puede representar con el formato correcto para el dispositivo o explorador web que lo solicita.  
  
## <a name="to-manually-add-snapshots-to-report-history"></a>Para agregar manualmente instantáneas a un historial de informe
  
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

1. En el Administrador de informes, vaya a la página **Contenido** , desplace el puntero sobre el elemento del que quiere ver el historial y haga clic en la flecha de lista desplegable.
  
2. En el menú desplegable, haga clic en **Ver historial de informes**.  
  
3. Haga clic en **Nueva instantánea**. Se crea una nueva instantánea en la columna **Cuando se ejecuta** .  
    > [!NOTE]
    > Para habilitar la creación de instantáneas, el administrador debe configurar el historial del informe para **permitir que el historial se cree manualmente**. Para obtener más información, vea [Limitar el historial de informe &#40;Administrador de informes&#41;](../reports/limit-report-history-report-manager.md).

4. Haga clic en **Aplicar**.
  
## <a name="to-automatically-add-all-snapshots-to-report-history"></a>Para agregar automáticamente todas las instantáneas al historial de informes  
  
1. Para un informe que ya está configurado para ejecutarse como una instantánea de ejecución de informes, puede establecer propiedades adicionales para guardar una copia de la instantánea en el historial del informe cada vez que se actualiza la instantánea.  
  
2. En el Administrador de informes, vaya a la página **Contenido** , desplace el puntero sobre el elemento del que quiere ver el historial y haga clic en la flecha de lista desplegable.  
  
3. En el menú desplegable, haga clic en **Administrar**.  
  
4. Haga clic en **Opciones de instantánea**.  
  
5. Active la casilla correspondiente a **Almacenar todas las instantáneas de ejecución de informes en el historial**.  
  
6. Haga clic en **Aplicar**.  
  
## <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>Para agregar automáticamente instantáneas al historial del informe basándose en una programación  
  
1. En el Administrador de informes, vaya a la página **Contenido** , desplace el puntero sobre el elemento del que quiere ver el historial y haga clic en la flecha de lista desplegable.  
  
2. En el menú desplegable, haga clic en **Administrar**.  
  
3. Haga clic en **Opciones de instantánea**.  
  
4. Active la casilla correspondiente a **Utilizar la siguiente programación para agregar instantáneas al historial de informe**. Realice una de las siguientes acciones:  
  
    - Seleccione **Programación específica del informe**. Rellene los detalles de la programación, seleccione las fechas de inicio y fin de la programación y, por último, haga clic en **Aceptar**.  

    - Seleccione **Programación compartida**. En la lista, seleccione la programación que prefiera.  

5. Haga clic en **Aplicar**.  
  
## <a name="see-also"></a>Vea también

- [Configurar las propiedades de ejecución de un informe &#40;Administrador de informes&#41;](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)
- [Limitar el historial de informe &#40;Administrador de informes&#41;](../../reporting-services/reports/limit-report-history-report-manager.md)
- [Programaciones](../../reporting-services/subscriptions/schedules.md)   
- [Administrador de informes &#40;Modo nativo de SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="to-manually-add-snapshots-to-report-history"></a>Para agregar manualmente instantáneas a un historial de informe
  
1. En el portal web, navegue hasta el elemento para el que desea ver el historial y haga clic con el botón secundario en él.  
  
2. En el menú desplegable, seleccione **Administrar**.  
  
3. Seleccione la pestaña instantáneas del **historial** .  
  
4. En la página instantáneas del **historial** , seleccione la **nueva instantánea del historial**. Se crea una instantánea nueva que aparece a continuación con la fecha y hora actuales en la columna **creada** .  
  
    > [!NOTE]
    > Para habilitar la creación de instantáneas, el administrador debe configurar el historial del informe para **permitir que el historial se cree manualmente**. Para obtener más información, vea [limitar el historial de informes (portal web)](../../reporting-services/reports/limit-report-history-report-manager.md).

## <a name="to-add-snapshots-via-a-schedule-to-report-history"></a>Para agregar instantáneas mediante una programación al historial de informes

1. En el portal web, navegue hasta el elemento para el que desea ver el historial y haga clic con el botón secundario en él.  
  
2. En el menú desplegable, seleccione **Administrar**.  
  
3. Seleccione la pestaña instantáneas del **historial** .  
  
4. En la página instantáneas del **historial** , seleccione el botón **programación y configuración** .  
  
5. En la sección **programación** , seleccione una o ambas de las opciones siguientes si no se ha seleccionado al menos una opción:
    - **Crear instantáneas del historial en un programa**.  
    - **Permitir que los usuarios puedan crear instantáneas de forma manual**.  
  
6. En la sección **Opciones avanzadas** , seleccione **conservar todas las instantáneas del historial**.  
  
7. Opcionalmente, active la casilla **Guardar instantáneas de caché también en el historial de informes**.  
  
8.  Seleccione **Aplicar** para guardar la configuración.  

    > [!NOTE]  
    > Para habilitar la creación de instantáneas, el administrador debe configurar el historial del informe para **permitir que el historial se cree manualmente**. Para obtener más información, vea [limitar el historial de informes (portal web)](../../reporting-services/reports/limit-report-history-report-manager.md).

9.  Haga clic en **Aplicar**.

## <a name="to-automatically-add-all-snapshots-to-report-history"></a>Para agregar automáticamente todas las instantáneas al historial de informes  
  
1. Para un informe que ya está configurado para ejecutarse como una instantánea de ejecución de informes, puede establecer propiedades adicionales para guardar una copia de la instantánea en el historial del informe cada vez que se actualiza la instantánea.  
  
2. En el portal web, navegue hasta el elemento para el que desea ver el historial y haga clic con el botón secundario en él.  
  
3. En el menú desplegable, seleccione **Administrar**.  
  
4. Seleccione la pestaña instantáneas del **historial** .  
  
5. En la página instantáneas del **historial** , seleccione el botón **programación y configuración** .  
  
6. En la sección **programación** , seleccione una o ambas de las opciones siguientes si no se ha seleccionado al menos una opción:
    - **Crear instantáneas del historial en un programa**.  
    - **Permitir que los usuarios puedan crear instantáneas de forma manual**.  
  
7. En la sección **Opciones avanzadas** , seleccione **conservar todas las instantáneas del historial**.  
  
8. Opcionalmente, active la casilla **Guardar instantáneas de caché también en el historial de informes**.  
  
9. Seleccione **Aplicar** para guardar la configuración.  
  
## <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>Para agregar automáticamente instantáneas al historial del informe basándose en una programación  
  
1. En el portal web, navegue hasta el elemento para el que desea ver el historial y haga clic con el botón secundario en él.  
  
2. En el menú desplegable, seleccione **Administrar**.  
  
3. Seleccione la pestaña instantáneas del **historial** .  
  
4. En la página instantáneas del **historial** , seleccione el botón **programación y configuración** .  
  
5. Active la casilla correspondiente a **Utilizar la siguiente programación para agregar instantáneas al historial de informe**. Realice una de las siguientes acciones:  
  
    - Seleccione **Programación específica del informe**. Rellene los detalles de la programación, seleccione las fechas de inicio y fin de la programación y, por último, haga clic en **Aceptar**.  

    - Seleccione **Programación compartida**. En la lista, seleccione la programación que prefiera.  

5. Haga clic en **Aplicar**.  
  
## <a name="see-also"></a>Vea también

- [Configuración de las propiedades de ejecución de un informe (portal web)](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)
- [Limitar el historial de informes (portal web)](../../reporting-services/reports/limit-report-history-report-manager.md)
- [Programaciones](../../reporting-services/subscriptions/schedules.md)   
- [Portal web &#40;modo nativo de SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)

::: moniker-end