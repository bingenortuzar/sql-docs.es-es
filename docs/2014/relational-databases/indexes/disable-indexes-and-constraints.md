---
title: Deshabilitar índices y restricciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.disableindexes.f1
helpviewer_keywords:
- disabled indexes [SQL Server], index operations
- nonclustered indexes [SQL Server], disabling
- disabled indexes [SQL Server], guidelines
- clustered indexes, disabling
- constraints [SQL Server], disabling
- disabled indexes [SQL Server], viewing
- FOREIGN KEY constraints, disabling
- statistical information [SQL Server], indexes
- index disabling [SQL Server]
- indexed views [SQL Server], disabled indexes
ms.assetid: 2198f1af-fa44-47e9-92df-f4fde322ba18
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 047fffdc729b276979720e9d245862a692a86be0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162404"
---
# <a name="disable-indexes-and-constraints"></a>Deshabilitar índices y restricciones
  En este tema se describe cómo deshabilitar un índice o restricciones en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Al deshabilitar un índice, se impide que el usuario pueda tener acceso al mismo y, en el caso de los índices clúster, a los datos de la tabla subyacente. La definición del índice se conserva en los metadatos y las estadísticas de índice se mantienen en índices no clúster. La deshabilitación de un índice clúster o no clúster en una vista elimina físicamente los datos del índice. Al deshabilitar un índice clúster en una tabla, se impide el acceso a los datos, que siguen en la tabla pero dejan de estar disponibles para las operaciones de lenguaje de manipulación de datos (DML) hasta que se quite o recompile el índice.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para deshabilitar un índice, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El índice no se mantiene mientras está deshabilitado.  
  
-   El optimizador de consultas no tiene en cuenta el índice deshabilitado a la hora de crear planes de ejecución de consultas. Además, las consultas que hacen referencia al índice deshabilitado con una sugerencia de tabla generan un error.  
  
-   No puede crear un índice que use el mismo nombre que un índice existente deshabilitado.  
  
-   Se puede quitar un índice deshabilitado.  
  
-   Al deshabilitar un índice único, también se deshabilitan la restricción PRIMARY KEY o UNIQUE y todas las restricciones FOREIGN KEY que hacen referencia a las columnas indizadas de otras tablas. Al deshabilitar un índice clúster, se deshabilitan también todas las restricciones FOREIGN KEY entrantes y salientes de la tabla subyacente. Los nombres de las restricciones se enumeran en un mensaje de advertencia cuando se deshabilita el índice. Después de recompilar el índice, se deben habilitar todas las restricciones manualmente mediante la instrucción ALTER TABLE CHECK CONSTRAINT.  
  
-   Los índices no clúster se deshabilitan automáticamente cuando se deshabilita el índice clúster asociado. No se pueden habilitar hasta que se habilita el índice clúster en la tabla o vista, o bien hasta que se quita el índice clúster en la tabla. Los índices no clúster deben habilitarse de forma explícita, a no ser que el índice clúster se haya habilitado mediante la instrucción ALTER INDEX ALL REBUILD.  
  
-   La instrucción ALTER INDEX ALL REBUILD vuelve a generar y habilita todos los índices deshabilitados de la tabla, excepto los índices deshabilitados en las vistas. Los índices en las vistas deben habilitarse en una instrucción ALTER INDEX ALL REBUILD independiente.  
  
-   Al deshabilitar un índice clúster en una tabla también se deshabilitan todos los índices clúster y no clúster en las vistas que hacen referencia a esa tabla. Estos índices deben volverse a generar como los de la tabla a la que se hace referencia.  
  
-   No se puede tener acceso a las filas de datos del índice clúster deshabilitado excepto para quitar o volver a generar el índice clúster.  
  
-   Se puede recompilar un índice no clúster deshabilitado en línea cuando la tabla no tenga un índice clúster deshabilitado. Sin embargo, siempre debe volver a generar un índice clúster deshabilitado sin conexión si utiliza la instrucción ALTER INDEX REBUILD o CREATE INDEX WITH DROP_EXISTING. Para obtener más información sobre las operaciones de índices en línea, vea [Realizar operaciones de índice en línea](perform-index-operations-online.md).  
  
-   La instrucción CREATE STATISTICS no se puede ejecutar correctamente en una tabla que tenga un índice clúster deshabilitado.  
  
-   La opción de base de datos AUTO_CREATE_STATISTICS crea estadísticas en una columna cuando el índice está deshabilitado y existen las condiciones siguientes:  
  
    -   AUTO_CREATE_STATISTICS está establecido en ON.  
  
    -   No hay estadísticas existentes para la columna.  
  
    -   Las estadísticas son obligatorias durante la optimización de consultas.  
  
-   Si un índice clúster está deshabilitado, [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) no puede devolver información acerca de la tabla subyacente; en su lugar, la instrucción indica que el índice clúster está deshabilitado. [DBCC INDEXDEFRAG](/sql/t-sql/database-console-commands/dbcc-indexdefrag-transact-sql) no se puede usar para desfragmentar un índice deshabilitado; la instrucción genera un mensaje de error. Puede usar [DBCC DBREINDEX](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql) para recompilar un índice deshabilitado.  
  
-   Al crear un nuevo índice clúster se habilitan los índices no clúster deshabilitados previamente. Para obtener más información, consulte [Enable Indexes and Constraints](enable-indexes-and-constraints.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para ejecutar ALTER INDEX, se necesita, como mínimo, el permiso ALTER en la tabla o en la vista.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-disable-an-index"></a>Para deshabilitar un índice  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir la base de datos que contiene la tabla en la que desea deshabilitar un índice.  
  
2.  Haga clic en el signo más para expandir la carpeta **Tablas** .  
  
3.  Haga clic en el signo más para expandir la tabla en la que desea deshabilitar un índice.  
  
4.  Haga clic en el signo más para expandir la carpeta **Índices** .  
  
5.  Haga clic con el botón derecho en el índice que quiera deshabilitar y seleccione **Deshabilitar**.  
  
6.  En el cuadro de diálogo **Deshabilitar índices** , compruebe que el índice correcto se encuentra en la cuadrícula **Índices que va a deshabilitar** y haga clic en **Aceptar**.  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>Para deshabilitar todos los índices de una tabla  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir la base de datos que contiene la tabla en la que desea deshabilitar los índices.  
  
2.  Haga clic en el signo más para expandir la carpeta **Tablas** .  
  
3.  Haga clic en el signo más para expandir la tabla en la que desea deshabilitar los índices.  
  
4.  Haga clic con el botón derecho en la carpeta **Índices** y seleccione **Deshabilitar todo**.  
  
5.  En el cuadro de diálogo **Deshabilitar índices** , compruebe que los índices correctos se encuentran en la cuadrícula **Índices que va a deshabilitar** y haga clic en **Aceptar**. Para quitar un índice de la cuadrícula **Índices que va a deshabilitar** , seleccione el índice y, a continuación, presione la tecla SUPRIMIR.  
  
 La siguiente información está disponible en el cuadro de diálogo **Deshabilitar índices** :  
  
 **Nombre de índice**  
 Muestra el nombre del índice. Durante la ejecución, esta columna también muestra un icono que representa el estado.  
  
 **Nombre de tabla**  
 Muestra el nombre de la tabla o vista en la que se ha creado el índice.  
  
 **Tipo de índice**  
 Muestra el tipo del índice: **Clúster**, **Nonclustered**, **espacial**, o **XML**.  
  
 **Estado**  
 Muestra el estado de la operación de deshabilitación. Los valores posibles tras la ejecución son:  
  
-   En blanco  
  
     Antes de la ejecución, el **Estado** permanece en blanco.  
  
-   **En curso**  
  
     La deshabilitación de los índices se ha iniciado, pero no ha finalizado.  
  
-   **Success**  
  
     La operación de deshabilitación ha finalizado correctamente.  
  
-   **Error**  
  
     Se ha encontrado un error durante la operación de deshabilitación de índices; la operación no ha finalizado correctamente.  
  
-   **Detenido**  
  
     La deshabilitación del índice no ha finalizado correctamente porque el usuario ha detenido la operación.  
  
 **de mensaje**  
 Proporciona el texto de los mensajes de error durante la operación de deshabilitación. Durante la ejecución, los errores aparecen como hipervínculos. El texto de los hipervínculos describe el cuerpo del error. La columna **Mensaje** pocas veces es lo suficientemente ancha para poder leer el texto completo del mensaje. Hay dos maneras de leer el texto completo:  
  
-   Mueva el puntero sobre la celda del mensaje para que aparezca la información sobre herramientas con el texto de error.  
  
-   Haga clic en el hipervínculo para mostrar un cuadro de diálogo con el error completo.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-disable-an-index"></a>Para deshabilitar un índice  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- disables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    DISABLE;  
    ```  
  
#### <a name="to-disable-all-indexes-on-a-table"></a>Para deshabilitar todos los índices de una tabla  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Disables all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    DISABLE;  
    ```  
  
 Para obtener más información, vea [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
  
  
