---
title: Movimiento de una base de datos protegida por TDE a otra instancia de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption, moving
- TDE, moving a database
ms.assetid: fb420903-df54-4016-bab6-49e6dfbdedc7
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 42027a48803cd5269d5ab2d69452352bdbe62bc5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63012055"
---
# <a name="move-a-tde-protected-database-to-another-sql-server"></a>Mover una base de datos protegida por TDE a otra instancia de SQL Server
  En este tema se describe cómo proteger una base de datos mediante el uso del cifrado de datos transparente (TDE) y, a continuación, mover la base de datos a otra instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. TDE realiza el cifrado y descifrado de E/S en tiempo real de los datos y los archivos de registro. El cifrado utiliza una clave de cifrado de la base de datos (DEK), que está almacenada en el registro de arranque de la base de datos para que esté disponible durante la recuperación. DEK es una clave simétrica protegida mediante un certificado almacenado en la base de datos maestra (`master`) del servidor o una clave asimétrica protegida por un módulo EKM.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear una base de datos protegida por el cifrado de datos transparente, utilizando:**  
  
     [SQL Server Management Studio](#SSMSCreate)  
  
     [Transact-SQL](#TsqlCreate)  
  
-   **Para mover una base de datos, utilizando:**  
  
     [SQL Server Management Studio](#SSMSMove)  
  
     [Transact-SQL](#TsqlMove)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Cuando se mueve una base de datos protegida por TDE, también debe mover el certificado o la clave asimétrica que se usan para abrir DEK. El certificado o clave asimétrica debe instalarse en el `master` base de datos del servidor de destino, por lo que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede tener acceso a los archivos de base de datos. Para obtener más información, vea [Cifrado de datos transparente &#40;TDE&#41;](transparent-data-encryption.md).  
  
-   Debe conservar copias tanto del archivo de certificado como del archivo de clave privada para recuperar el certificado. No es necesario que la contraseña de la clave privada sea la misma que la contraseña de la clave maestra de la base de datos.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] almacena los archivos creados aquí en **C:\Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA** de forma predeterminada. Los nombres de los archivos y las ubicaciones pueden ser distintos.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
  
-   Requiere `CONTROL DATABASE` permiso en el `master` base de datos para crear la clave maestra de base de datos.  
  
-   Requiere `CREATE CERTIFICATE` permiso en el `master` base de datos para crear el certificado que protege DEK.  
  
-   Requiere el permiso `CONTROL DATABASE` para la base de datos cifrada y el permiso `VIEW DEFINITION` para el certificado o la clave asimétrica usados para cifrar la clave de cifrado de la base de datos.  
  
##  <a name="SSMSProcedure"></a> Para crear una base de datos protegida por el cifrado de datos transparente  
  
###  <a name="SSMSCreate"></a> Usar SQL Server Management Studio  
  
1.  Cree una clave maestra de base de datos y un certificado en el `master` base de datos. Para obtener más información, vea **Usar Transact-SQL** más adelante.  
  
2.  Crear una copia de seguridad del certificado del servidor en el `master` base de datos. Para obtener más información, vea **Usar Transact-SQL** más adelante.  
  
3.  En el Explorador de objetos, haga clic con el botón derecho en la carpeta **Bases de datos** y seleccione **Nueva base de datos**.  
  
4.  En el cuadro de diálogo **Nueva base de datos** , en el cuadro **Nombre de la base de datos** , escriba el nombre de la nueva base de datos.  
  
5.  En el cuadro **Propietario** , escriba el nombre del propietario de la nueva base de datos. Como alternativa, haga clic en los puntos suspensivos **(...)** para abrir el cuadro de diálogo **Seleccionar propietario de base de datos**. Para obtener más información sobre la creación de una nueva base de datos, vea [Create a Database](../../databases/create-a-database.md).  
  
6.  En el Explorador de objetos, haga clic en el signo más para expandir la carpeta **Bases de datos** .  
  
7.  Haga clic con el botón derecho en la base de datos que creó, seleccione **Tareas**y **Administrar cifrado de base de datos**.  
  
     En el cuadro de diálogo **Administrar cifrado de base de datos** están disponibles las siguientes opciones.  
  
     **Algoritmo de cifrado**  
     Muestra o establece el algoritmo que se debe utilizar para el cifrado de la base de datos. `AES128` es el algoritmo predeterminado. Este campo no puede estar vacío. Para obtener más información sobre algoritmos de cifrado, vea [Choose an Encryption Algorithm](choose-an-encryption-algorithm.md).  
  
     **Usar certificado de servidor**  
     Establece que el cifrado se proteja mediante un certificado. Seleccione uno de la lista. Si no tiene el permiso `VIEW DEFINITION` para los certificados de servidor, esta lista estará vacía. Si se selecciona un método de cifrado de certificado, este valor no puede estar vacío. Para obtener más información acerca de los certificados, vea [SQL Server Certificates and Asymmetric Keys](../sql-server-certificates-and-asymmetric-keys.md).  
  
     **Usar clave asimétrica de servidor**  
     Establece que el cifrado se proteja mediante una clave asimétrica. Solo se muestran las claves asimétricas disponibles. Solo una clave asimétrica protegida por un módulo EKM puede cifrar una base de datos mediante TDE.  
  
     **Activar cifrado de base de datos**  
     Modifica la base de datos para habilitar (activada) o deshabilitar (sin activar) TDE.  
  
8.  Cuando termine, haga clic en **Aceptar**.  
  
###  <a name="TsqlCreate"></a> Usar Transact-SQL  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Create a database master key and a certificate in the master database.  
    USE master ;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    CREATE CERTIFICATE TestSQLServerCert   
    WITH SUBJECT = 'Certificate to protect TDE key'  
    GO  
    -- Create a backup of the server certificate in the master database.  
    -- The following code stores the backup of the certificate and the private key file in the default data location for this instance of SQL Server   
    -- (C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA).  
  
    BACKUP CERTIFICATE TestSQLServerCert   
    TO FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Create a database to be protected by TDE.  
    CREATE DATABASE CustRecords ;  
    GO  
    -- Switch to the new database.  
    -- Create a database encryption key, that is protected by the server certificate in the master database.   
    -- Alter the new database to encrypt the database using TDE.  
    USE CustRecords;  
    GO  
    CREATE DATABASE ENCRYPTION KEY  
    WITH ALGORITHM = AES_128  
    ENCRYPTION BY SERVER CERTIFICATE TestSQLServerCert;  
    GO  
    ALTER DATABASE CustRecords  
    SET ENCRYPTION ON;  
    GO  
    ```  
  
 Para obtener más información, vea:  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)  
  
-   [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-certificate-transact-sql)  
  
-   [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
-   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
##  <a name="TsqlProcedure"></a> Para mover una base de datos  
  
###  <a name="SSMSMove"></a> Usar SQL Server Management Studio  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la base de datos que cifró anteriormente, seleccione **Tareas** y **Separar...**.  
  
     En el cuadro de diálogo **Separar base de datos** están disponibles las siguientes opciones.  
  
     **Bases de datos que se van a separar**  
     Enumera las bases de datos que se van a separar.  
  
     **Database Name**  
     Muestra el nombre de la base de datos que se va a separar.  
  
     **Quitar conexiones**  
     Desconecta las conexiones a la base de datos especificada.  
  
    > [!NOTE]  
    >  No puede separar una base de datos con conexiones activas.  
  
     **Actualizar estadísticas**  
     De forma predeterminada, la operación de separación conserva las estadísticas de optimización obsoletas al separar la base de datos; para actualizar las estadísticas de optimización existentes, haga clic en esta casilla.  
  
     **Mantener catálogos de texto completo**  
     De forma predeterminada, la operación de separación conserva los catálogos de texto completo asociados a la base de datos. Para quitarlos, desactive la casilla **Mantener catálogos de texto completo** . Esta opción solo aparece cuando se está actualizando una base de datos desde [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
     **Estado**  
     Muestra uno de los siguientes estados: **Listo** o **No está listo**.  
  
     **de mensaje**  
     En la columna **Mensaje** puede aparecer información sobre la base de datos, tal y como se indica a continuación:  
  
    -   Cuando una base de datos está implicada en una replicación, el **Estado** es **No está listo** y la columna **Mensaje** muestra **Base de datos replicada**.  
  
    -   Cuando una base de datos tiene una o más conexiones activas, el **estado** es **no está listo** y **mensaje** columna muestra _< número_de_conexiones_activas >_**Conexiones activas** , por ejemplo: **1 conexión activa**). Antes de separar la base de datos, debe desconectar todas las conexiones activas seleccionando **Quitar conexiones**.  
  
     Para obtener más información acerca de un mensaje, haga clic en el texto con hipervínculo para abrir el Monitor de actividad.  
  
2.  Haga clic en **Aceptar**.  
  
3.  Con el Explorador de Windows, mueva o copie los archivos de la base de datos desde el servidor de origen a la misma ubicación en el servidor de destino.  
  
4.  Con el Explorador de Windows, mueva o copie la copia de seguridad del certificado del servidor y el archivo de clave privada desde el servidor de origen a la misma ubicación del servidor de destino.  
  
5.  Cree una clave maestra de la base de datos en la instancia de destino de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, vea **Usar Transact-SQL** más adelante.  
  
6.  Vuelva a crear el certificado del servidor mediante el archivo de copia de seguridad del certificado del servidor original. Para obtener más información, vea **Usar Transact-SQL** más adelante.  
  
7.  En el Explorador de objetos, en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en la carpeta **Bases de datos** y, después, seleccione **Adjuntar...**.  
  
8.  En el cuadro de diálogo **Adjuntar bases de datos** , en **Bases de datos que se van a adjuntar**, haga clic en **Agregar**.  
  
9. En el **buscar archivos de base de datos -**_nombre_servidor_ cuadro de diálogo, seleccione la base de datos de archivo para adjuntar al nuevo servidor y haga clic en **Aceptar**.  
  
     En el cuadro de diálogo **Adjuntar bases de datos** están disponibles las siguientes opciones.  
  
     **Bases de datos que se van a adjuntar**  
     Muestra información sobre las bases de datos seleccionadas.  
  
     \<no column header>  
     Muestra un icono que indica el estado de la operación de adjuntar. Los iconos posibles se indican en la descripción de **Estado** , que encontrará más adelante.  
  
     **Ubicación del archivo MDF**  
     Muestra la ruta de acceso y el nombre del archivo MDF seleccionado.  
  
     **Database Name**  
     Muestra el nombre de la base de datos.  
  
     **Adjuntar como**  
     Opcionalmente, especifica un nombre distinto con el que se debe adjuntar la base de datos.  
  
     **Propietario**  
     Ofrece una lista desplegable de los posibles propietarios de base de datos desde los que opcionalmente puede seleccionarse otro propietario.  
  
     **Estado**  
     Muestra el estado de la base de datos de acuerdo con la tabla siguiente.  
  
    |Icono|Texto de estado|Descripción|  
    |----------|-----------------|-----------------|  
    |(Sin icono)|(Sin texto)|La operación de adjuntar no se ha iniciado o puede estar pendiente para este objeto. Es la opción predeterminada al abrir el diálogo.|  
    |Triángulo verde hacia la derecha|En curso|La operación de adjuntar se ha iniciado, pero no ha finalizado.|  
    |Marca de verificación verde|Correcto|El objeto se ha adjuntado correctamente.|  
    |Círculo rojo con una cruz blanca|Error|La operación de adjuntar ha detectado un error y no ha finalizado correctamente.|  
    |Círculo con dos cuadrantes negros (a la izquierda y la derecha) y dos cuadrantes blancos (en la parte superior e inferior)|Detenido|La operación de adjuntar no ha finalizado correctamente porque el usuario la ha detenido.|  
    |Círculo con una flecha curvada que apunta hacia la izquierda|Revertido|La operación de adjuntar se ha ejecutado correctamente, pero se ha revertido debido a un error al adjuntar otro objeto.|  
  
     **de mensaje**  
     Muestra un mensaje en blanco o un hipervínculo que indica "Archivo no encontrado".  
  
     **Agregar**  
     Busca los archivos de base de datos principales necesarios. Si el usuario selecciona un archivo .mdf, la información pertinente se llena automáticamente en los respectivos campos de la cuadrícula **Bases de datos que se van a adjuntar** .  
  
     **Quitar**  
     Quita el archivo seleccionado de la cuadrícula **Bases de datos que se van a adjuntar** .  
  
     **"** _<database_name>_ **" detalles de la base de datos**  
     Muestra los nombres de los archivos que se van a adjuntar. Para comprobar o cambiar el nombre de la ruta de acceso de un archivo, haga clic en el botón **Examinar** (**...**).  
  
    > [!NOTE]  
    >  Si un archivo no existe, la columna **Mensaje** muestra "No se encontró". Si un archivo de registro no se encuentra, indica que se halla en otro directorio o que se ha eliminado. En tal caso, debe actualizar la ruta de acceso del archivo en la cuadrícula **Detalles de la base de datos** para que señale la ubicación correcta o eliminar el archivo de registro de la cuadrícula. Si un archivo de datos .ndf no se encuentra, debe actualizar su ruta de acceso en la cuadrícula para que señale la ubicación correcta.  
  
     **Nombre del archivo original**  
     Muestra el nombre del archivo adjunto que pertenece a la base de datos.  
  
     **Tipo de archivo**  
     Indica el tipo de archivo, que puede ser de **datos** o de **registro**.  
  
     **Ruta de acceso del archivo actual**  
     Muestra la ruta de acceso del archivo de base de datos seleccionado. La ruta de acceso puede modificarse manualmente.  
  
     **de mensaje**  
     Muestra un mensaje en blanco o un hipervínculo que indica "**Archivo no encontrado**".  
  
###  <a name="TsqlMove"></a> Usar Transact-SQL  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Detach the TDE protected database from the source server.   
    USE master ;  
    GO  
    EXEC master.dbo.sp_detach_db @dbname = N'CustRecords';  
    GO  
    -- Move or copy the database files from the source server to the same location on the destination server.   
    -- Move or copy the backup of the server certificate and the private key file from the source server to the same location on the destination server.   
    -- Create a database master key on the destination instance of SQL Server.   
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '*rt@40(FL&dasl1';  
    GO  
    -- Recreate the server certificate by using the original server certificate backup file.   
    -- The password must be the same as the password that was used when the backup was created.  
  
    CREATE CERTIFICATE TestSQLServerCert   
    FROM FILE = 'TestSQLServerCert'  
    WITH PRIVATE KEY   
    (  
        FILE = 'SQLPrivateKeyFile',  
        DECRYPTION BY PASSWORD = '*rt@40(FL&dasl1'  
    );  
    GO  
    -- Attach the database that is being moved.   
    -- The path of the database files must be the location where you have stored the database files.  
    CREATE DATABASE [CustRecords] ON   
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\CustRecords.mdf' ),  
    ( FILENAME = N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\CustRecords_log.LDF' )  
    FOR ATTACH ;  
    GO  
    ```  
  
 Para obtener más información, vea:  
  
-   [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)  
  
-   [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
## <a name="see-also"></a>Vea también  
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../databases/database-detach-and-attach-sql-server.md)  
  
  
