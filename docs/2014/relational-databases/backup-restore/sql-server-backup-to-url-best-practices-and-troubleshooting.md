---
title: Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ac34c95e7ee4dc6f57ef7d8806a7db1bb981a944
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175966"
---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server
  En este tema se incluyen procedimientos recomendados y sugerencias para la solución de problemas de SQL Server copias de seguridad y restauraciones en el Blob service de Azure.  
  
 Para obtener más información sobre el uso del servicio de almacenamiento de blobs de Azure para SQL Server operaciones de copia de seguridad o restauración, consulte:  
  
-   [SQL Server copias de seguridad y restauración con Azure Blob Storage servicio](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [Tutorial: SQL Server copias de seguridad y restauración en Azure Blob Storage servicio](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups"></a>Administrar copias de seguridad  
 La lista siguiente incluye recomendaciones generales para administrar copias de seguridad:  
  
-   Se recomienda usar un nombre de archivo único para cada copia de seguridad con el fin de evitar que se sobrescriban accidentalmente los blobs.  
  
-   Al crear un contenedor, se recomienda establecer el nivel de acceso en **privado**, de forma que solo los usuarios o las cuentas que puedan proporcionar la información de autenticación necesaria sean capaces de leer o escribir los blobs en el contenedor.  
  
-   En el caso de SQL Server bases de datos en una instancia de SQL Server que se ejecutan en una máquina virtual de Azure, use una cuenta de almacenamiento en la misma región que la máquina virtual para evitar costos de transferencia de datos entre regiones. El uso de la misma región también garantiza un rendimiento óptimo para las operaciones de copia de seguridad y restauración.  
  
-   Una actividad de copia de seguridad con errores puede dar como resultado un archivo de copia de seguridad no válido. Se recomienda identificar periódicamente las copias de seguridad con errores y eliminar los archivos blob. Para obtener más información, consulte [Deleting Backup Blob Files with Active Leases](deleting-backup-blob-files-with-active-leases.md).  
  
-   El uso de la opción `WITH COMPRESSION` durante la copia de seguridad puede reducir al mínimo los costos de almacenamiento y los costos de transacciones de almacenamiento. También puede reducir el tiempo necesario para completar el proceso de copia de seguridad.  
  
## <a name="handling-large-files"></a>Controlar archivos grandes  
  
-   La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operación de copia de seguridad utiliza varios subprocesos para optimizar la transferencia de datos a los servicios de almacenamiento de blobs de Azure.  Sin embargo, el rendimiento depende en varios factores, como el ancho de banda del ISV y el tamaño de la base de datos. Si piensa hacer copia de seguridad de bases de datos o grupos de archivos grandes desde una base de datos de SQL Server local, se recomienda que realice primero algunas pruebas de rendimiento. Los acuerdos de nivel de servicio de [Azure Storage](https://go.microsoft.com/fwlink/?LinkId=271619) tienen tiempos de procesamiento máximos para los blobs que puede tener en cuenta.  
  
-   Use la opción `WITH COMPRESSION` como se recomienda en la sección **Administrar copias de seguridad**, ya que es muy importante al realizar la copia de seguridad de archivos grandes.  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>Resolución de problemas para realizar la copia de seguridad de una dirección URL o una restauración a partir de esta  
 A continuación se indican algunas formas rápidas de solucionar errores al realizar copias de seguridad o restaurar desde el servicio de almacenamiento de blobs de Azure.  
  
 Para evitar errores debidos a opciones no admitidas o limitaciones, revise la lista de limitaciones y la información sobre los comandos de copia de seguridad y restauración en el artículo [SQL Server copias de seguridad y restauración con Azure BLOB Storage Service](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) .  
  
 **Errores de autenticación:**  
  
-   WITH CREDENTIAL es una opción nueva que es necesaria para realizar copias de seguridad en el servicio de almacenamiento de blobs de Azure o restaurar desde este. He aquí algunos errores relacionados con las credenciales:  
  
     La credencial especificada en el comando `BACKUP` o `RESTORE` no existe. Para evitar este problema, puede incluir instrucciones T-SQL para crear la credencial si no existe ninguna en la instrucción de copia de seguridad. He aquí un ejemplo que puede usar:  
  
    ```  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
  
    ```  
  
-   La credencial existe pero la cuenta de inicio de sesión usada para ejecutar el comando de copia de seguridad no tiene permisos de acceso a las credenciales. Use una cuenta de inicio de sesión en el rol **db_backupoperator** con permisos para **Modificar cualquier credencial** .  
  
-   Compruebe los valores de clave y nombre de la cuenta de almacenamiento. La información almacenada en la credencial debe coincidir con los valores de propiedad de la cuenta de almacenamiento de Azure que se usa en las operaciones de copia de seguridad y restauración.  
  
 **Errores de copia de seguridad:**  
  
-   Las copias de seguridad en paralelo en el mismo blob produce errores en una de las copias de seguridad y hacen que aparezca un **Error de inicialización** .  
  
-   Use los registros de errores siguientes como ayuda para solucionar problemas de copia de seguridad:  
  
    -   Establezca la marca de seguimiento 3051 para activar el registro en un registro de errores específico con el siguiente formato en:  
  
         BackupToUrl-\<instname>-\<dbname>-action-\<PID>.log, donde \<action> es uno de los siguientes elementos:  
  
        -   `DB`  
  
        -   `FILELISTONLY`  
  
        -   `LABELONLY`  
  
        -   `HEADERONLY`  
  
        -   `VERIFYONLY`  
  
    -   También puede buscar información si revisas el registro de eventos de Windows, en registros de aplicación con el nombre "SQLBackupToUrl".  
  
-   Al restaurar desde una copia de seguridad comprimida, puede aparecer el siguiente error:  
  
    -   **SqlException 3284. Gravedad 16 estado: 5**  
        **La marca de error del'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak 'mensaje en el dispositivo no está alineada. Vuelva a emitir la instrucción restore con el mismo tamaño de bloque usado para crear el conjunto de subconjunto: ' 65536 ' parece un valor posible.**  
  
         Para resolver este error, vuelva a emitir la instrucción `BACKUP` especificando `BLOCKSIZE = 65536`.  
  
-   Error durante la copia de seguridad porque los blobs tienen una concesión activa: una actividad de copia de seguridad con errores puede dar como resultado blobs con concesiones activas.  
  
     Si se vuelve a intentar una instrucción de copia de seguridad, la operación de copia de seguridad puede producir un error similar al siguiente:  
  
     **BACKUP TO URL recibió una excepción del extremo remoto. Mensaje de excepción: El servidor remoto devolvió un error: (412) actualmente hay una concesión en el BLOB y no se especificó ningún identificador de concesión en**la solicitud.  
  
     Si se intenta una instrucción de restauración en un archivo de blob de copia de seguridad que tiene una concesión activa, la operación de restauración produce un error similar al siguiente:  
  
     **Mensaje de excepción: El servidor remoto devolvió un error: (409) conflicto..**  
  
     Cuando se produce ese error, es necesario eliminar los archivos de blob. Para obtener más información sobre este escenario y cómo corregir este problema, vea [Deleting Backup Blob Files with Active Leases](deleting-backup-blob-files-with-active-leases.md).  
  
## <a name="proxy-errors"></a>Errores de proxy  
 Si usa servidores proxy para tener acceso a Internet, pueden producirse los problemas siguientes:  
  
 **Limitación de la conexión por parte de los servidores proxy:**  
  
 Los servidores proxy pueden tener configuraciones que limitan el número de conexiones por minuto. Copia de seguridad en URL es un proceso multiproceso y, por tanto, puede sobrepasar este límite. Si esto ocurre, el servidor proxy elimina la conexión. Para resolver este problema, cambie la configuración de proxy para que SQL Server no utilice el proxy.   A continuación se muestran algunos ejemplos de los tipos o mensajes de error que puede ver en el registro de errores:  
  
-   No se pudo'http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak 'escribir en : BACKUP TO URL recibió una excepción del extremo remoto. Mensaje de excepción: No se pueden leer los datos de la conexión de transporte: La conexión se cerró.  
  
-   Error de E/S irrecuperable en el archivo "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak: ". No se pudo recopilar el error del punto de conexión remoto.  
  
     Mensaje 3013, nivel 16, estado 1, línea 2  
  
     Fin anómalo de BACKUP DATABASE.  
  
-   BackupIoRequest:: ReportIoError: error de escritura en el dispositivo'http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak 'de copia de seguridad. Error de sistema operativo Copia de seguridad en URL recibió una excepción del extremo remoto. Mensaje de excepción: No se pueden leer los datos de la conexión de transporte: La conexión se cerró.  
  
 Si activa el registro detallado mediante la marca de seguimiento 3051, puede ver también el mensaje siguiente en los registros:  
  
 Código de estado HTTP 502, error de proxy del mensaje de estado HTTP (El número de peticiones HTTP por minuto superó el límite configurado. Póngase en contacto con el administrador del servidor ISA.  )  
  
 **Configuración de proxy predeterminada no seleccionada:**  
  
 A veces, la configuración predeterminada no se selecciona, lo que produce errores de autenticación del proxy como el que se muestra a continuación: *Error de E/S irrecuperable en el archivo "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak: ". La copia de seguridad en URL recibió una excepción del punto de conexión remoto. Mensaje de excepción: El servidor remoto devolvió un error: (407) Se requiere **autenticación de proxy.***  
  
 Para resolver este problema, cree un archivo de configuración que permita al proceso Copia de seguridad en URL utilizar la configuración de proxy predeterminada mediante los pasos siguientes:  
  
1.  Cree un archivo de configuración denominado BackuptoURL.exe.config con el código XML siguiente:  
  
    ```  
    <?xml version ="1.0"?>  
    <configuration>   
                    <system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    </system.net>  
    </configuration>  
  
    ```  
  
2.  Coloque el archivo de configuración en la carpeta Binn de la instancia de SQL Server. Por ejemplo, si mi SQL Server está instalado en la unidad C de la máquina, coloque el archivo de configuración aquí: *C:\Archivos de programa\Microsoft SQL Server\MSSQL12. NombreDeInstancia\<> \MSSQL\Binn*.  
  
## <a name="troubleshooting-sql-server-managed-backup-to-azure"></a>Solución de problemas de SQL Server copia de seguridad administrada en Azure  
 Puesto que Copia de seguridad administrada de SQL Server se basa en Copia de seguridad en URL, las sugerencias para la solución de problemas que se han descrito en las secciones anteriores son aplicables también a las bases de datos o las instancias que utilizan Copia de seguridad administrada de SQL Server.  La información sobre la solución de problemas de SQL Server copia de seguridad administrada en Azure se describe con más detalle en [solución de problemas de SQL Server copia de seguridad administrada en Azure](sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="see-also"></a>Vea también  
 [Restaurar a partir de copias de seguridad almacenadas en Azure](restoring-from-backups-stored-in-microsoft-azure.md)  
  
  
