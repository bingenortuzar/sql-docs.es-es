---
title: Tratar objetos grandes con CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 4140d6b1-51cb-4d23-a4b6-8155360034fe
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6c7230150807b5bdd0849ea7ad5af00dbedb4ff3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781540"
---
# <a name="handling-large-objects-using-clr"></a>Tratar objetos grandes con CLR
  El ejemplo `HandlingLOBUsingCLR` para SQL Server muestra la transferencia de objetos grandes (LOB) entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un sistema de archivos que está disponible en el servidor utilizando procedimientos almacenados de Common Language Runtime (CLR). Este ejemplo muestra cómo obtener acceso a los archivos en el código del servidor, y cómo invocar después consultas dinámicas y procedimientos almacenados desde procedimientos almacenados basados en CLR. También muestra cómo eliminar del Registro y cómo registrar métodos y ensamblados de CLR mediante [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para crear y ejecutar este proyecto se debe instalar el siguiente software:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express. Puede obtener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express de forma gratuita desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sitio web [de documentación y ejemplos de](https://go.microsoft.com/fwlink/?LinkId=31046)Express.  
  
-   La base de datos de AdventureWorks que está disponible en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sitio web [para desarrolladores de](https://go.microsoft.com/fwlink/?linkid=62796).  
  
-   .NET Framework SDK 2.0 o posterior, o Microsoft Visual Studio 2005 o posterior. Puede obtener .NET Framework SDK de forma gratuita.  
  
-   Además, se deben cumplir las siguientes condiciones:  
  
-   La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está usando debe tener habilitada la integración con CLR.  
  
-   Para habilitar la integración con CLR, siga estos pasos:  
  
    #### <a name="enabling-clr-integration"></a>Habilitar la integración con CLR  
  
    -   Ejecute los siguientes comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  Para habilitar CLR, debe tener el permiso de nivel de servidor `ALTER SETTINGS`, que se concede implícitamente a los miembros de los roles fijos de servidor `sysadmin` y `serveradmin`.  
  
-   La base de datos de AdventureWorks debe estar instalada en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está usando.  
  
-   Si no es administrador de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está usando, debe hacer que un administrador le conceda el permiso **CreateAssembly**  para completar la instalación.  
  
## <a name="building-the-sample"></a>Generar el ejemplo  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>Cree y ejecute el ejemplo utilizando las siguientes instrucciones:  
  
1.  Abra un símbolo del sistema de Visual Studio o de .NET Framework.  
  
2.  Si es necesario, cree un directorio para el ejemplo. Para este ejemplo, utilizaremos C:\MySample.  
  
3.  Como este ejemplo requiere un ensamblado firmado, cree una clave asimétrica escribiendo el comando:  
  
## <a name="sample-code"></a>Código muestra  
 A continuación se muestran las listas de código para este ejemplo.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.IO;  
using System.Globalization;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;  
  
    public sealed class LargeObjectBinary  
    {  
        //Recommended chunk size for processing large amounts of data  
        private const int bufferSize = 4000;  
  
        /// <summary>  
        ///This class only contains static members, therefore it needs no public constructor.  
        /// </summary>  
        private LargeObjectBinary()  
        {  
        }  
  
        /// <summary>  
        /// Retrieves a thumbnail photograph from the database into a file assessible to the server.    
        /// </summary>  
        /// <param name="photoId">Unique identifier for a product picture.</param>  
        /// <param name="currentDirectory">Which folder to put the picture into.</param>  
        /// <param name="fileName">What to call the picture in the specified folder.</param>  
        public static void GetPhotoFromDB(Int32 photoId, string currentDirectory, string fileName)  
        {  
            SqlDataReader sqlReader = null;  
  
            SqlConnection conn = new SqlConnection("context connection = true");  
            conn.Open();  
  
            SqlCommand sprocCommand = conn.CreateCommand();  
            //Even though we are supply an int, it is a good habit to use parameters to insert  
            //values into command text rather than using String.Format.  In the case of string parameters, it can  
            //help prevent injection attacks.  
            sprocCommand.CommandText = "SELECT ThumbNailPhoto FROM Production.ProductPhoto WHERE ProductPhotoID = @ProductPhotoID";  
            sprocCommand.Parameters.Add("@ProductPhotoID", SqlDbType.Int);  
            sprocCommand.Parameters[0].Value = photoId;  
  
            //TODO: Is getting chunks the best way to retrieve LOB from the database?  Is there a limit?  
            try  
            {  
                sqlReader = sprocCommand.ExecuteReader( //CommandBehavior.SequentialAccess  
                    );  
                if (sqlReader == null)  
                {  
                    LogError(currentDirectory, "ExecuteReader failed!");  
                }  
                else  
                {  
                    if (sqlReader.Read())  
                    {  
                        // Create a file to hold the output.  
                        if (!Directory.Exists(currentDirectory))  
                            Directory.CreateDirectory(currentDirectory);  
                        fileName = currentDirectory + fileName;  
                        using (FileStream fileStream = new FileStream(fileName,  
                                                                      FileMode.  
                                                                      OpenOrCreate,  
                                                                      FileAccess.  
                                                                      Write))  
                        {  
                            using (BinaryWriter binaryWriter =  
                                                new BinaryWriter(  
                                fileStream))  
                            {  
                                // The BLOB byte[] buffer to be filled by GetBytes.  
                                byte[] outbyte = new byte[bufferSize];  
  
                                // The starting position in the BLOB output.  
                                long startIndex = 0;  
  
                                // Read the bytes into outbyte[] and retain the number of bytes returned.  
                                long retval = sqlReader.GetBytes(0, startIndex,  
                                                                 outbyte, 0,  
                                                                 bufferSize);  
  
                                // Continue reading and writing while there are bytes beyond the size of the buffer.  
                                while (retval == bufferSize)  
                                {  
                                    binaryWriter.Write(outbyte);  
  
                                    // Reposition the start index to the end of the last buffer and fill the buffer.  
                                    startIndex += bufferSize;  
                                    retval = sqlReader.GetBytes(0, startIndex,  
                                                                outbyte, 0,  
                                                                bufferSize);  
                                }  
  
                                // Write the remaining buffer.  
                                binaryWriter.Write(outbyte);  
                                //TODO:  Shouldn't need to flush here because the close will do it for me?  
                                //binaryWriter.Flush();  
                            }  
                        }  
                    }  
                    else  
                        LogError(currentDirectory, "No row returned!");  
                }  
            }  
            catch (SqlException e)  
            {  
                LogError(currentDirectory, String.Format(CultureInfo.InvariantCulture, "Unable to copy binary contents from database.  Error: {0}", e.ToString()));  
            }  
            finally  
            {  
                if (sqlReader != null)  
                    sqlReader.Close();  
  
                //dispose the conn  
                if (conn != null)  
                {  
                    conn.Close();  
                    conn.Dispose();  
                }  
            }  
        }  
  
        /// <summary>  
        /// Saves a thumbnail picture into the database from a file accessible to the server.  
        /// </summary>  
        /// <param name="photoId">Unique identifier for a product picture.</param>  
        /// <param name="currentDirectory">Which folder to get the picture from.</param>  
        /// <param name="fileName">What the picture in the specified folder is called.</param>  
        public static void PutPhotoIntoDB(Int32 photoId, string currentDirectory, string fileName)  
        {  
            //TODO: Is there a limit on how large the LOB can be?  
            string fullFileName = currentDirectory + fileName;  
            byte[] bytes = ReadFile(fullFileName);  
  
            try  
            {  
                SqlConnection conn = new SqlConnection("context connection = true");  
                conn.Open();  
  
                SqlCommand sprocCommand = conn.CreateCommand();  
                sprocCommand.CommandText = "dbo.usp_UpdateImage";  
                sprocCommand.CommandType = CommandType.StoredProcedure;  
  
                sprocCommand.Parameters.Add(new SqlParameter("@ProductPhotoID", SqlDbType.Int));  
                // Add time to the short name because there is an unique constraint on this column.  
                sprocCommand.Parameters[0].Value = photoId;  
                sprocCommand.Parameters.Add(new SqlParameter("@ThumbNailPhoto", SqlDbType.VarBinary));  
                sprocCommand.Parameters[1].Value = bytes;  
                sprocCommand.ExecuteNonQuery();  
            }  
            catch (SqlException e)  
            {  
                LogError(currentDirectory, String.Format(CultureInfo.InvariantCulture, "Unable to update binary contents into the database.  Error: {0}", e.ToString()));  
            }  
        }  
  
        /// <summary>  
        /// Read the contents of a file and return the bytes.  
        /// </summary>  
        /// <param name="fileName">The name of the file to be read.</param>  
        /// <returns></returns>  
        private static byte[] ReadFile(string fileName)  
        {  
            // Open the file assuming the file is in ASCII format.  
            using (BinaryReader binaryReader = new BinaryReader((Stream)File.OpenRead(fileName), System.Text.Encoding.ASCII))  
            {  
                long fileSize = binaryReader.BaseStream.Length;  
                byte[] bytes = new Byte[fileSize];  
                binaryReader.Read(bytes, 0, (int)fileSize);  
                return bytes;  
            }  
        }  
  
        /// <summary>  
        ///Appends a message to a file accessible to the server.  When System.Diagnostics is available from  
        /// CLR Sprocs this should be changed to use the event log.  
        /// </summary>  
        /// <param name="currentDirectory">Which folder the message log file resides in</param>  
        /// <param name="errorMessage">The text to add to the message log file</param>  
        private static void LogError(string currentDirectory, string errorMessage)  
        {  
            using (FileStream errorLogStream = new FileStream(currentDirectory + "error.log", FileMode.Append, FileAccess.Write))  
            {  
                using (StreamWriter errorLogWriter = new StreamWriter(errorLogStream))  
                {  
                    errorLogWriter.WriteLine(errorMessage);  
                }  
            }  
        }  
    }  
```  
  
 Visual Basic  
  
```  
Imports Microsoft.SqlServer.Server  
Imports Microsoft.VisualBasic  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Diagnostics  
Imports System.Globalization  
Imports System.IO  
Imports System.Reflection  
  
Public NotInheritable Class LargeObjectBinary  
    'Recommended chunk size for processing large amounts of data  
    Private Const bufferSize As Integer = 4000  
  
    ''' <summary>  
    '''    This class only contains static members, therefore it needs no public constructor.  
    ''' </summary>  
    Private Sub New()  
    End Sub  
  
    ''' <summary>  
    ''' Retrieves a thumbnail photograph from the database into a file assessible to the server.    
    ''' </summary>  
    ''' <param name="photoId">Unique identifier for a product picture.</param>  
    ''' <param name="currentDirectory">Which folder to put the picture into.</param>  
    ''' <param name="fileName">What to call the picture in the specified folder.</param>  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub GetPhotoFromDB(ByVal photoId As Integer, _  
        ByVal currentDirectory As String, ByVal fileName As String)  
        Dim sqlReader As SqlDataReader = Nothing  
  
        Dim conn As SqlConnection = New SqlConnection("context connection = true")  
        conn.Open()  
  
        Dim sprocCommand As SqlCommand = conn.CreateCommand()  
        'Even though we are supply an int, it is a good habit to use parameters to insert  
        'values into command text rather than using String.Format.  In the   
        'case of string parameters, it can help prevent injection attacks.  
        sprocCommand.CommandText = "SELECT ThumbNailPhoto FROM Production.ProductPhoto " _  
            & "WHERE ProductPhotoID = @ProductPhotoID"  
        sprocCommand.Parameters.Add("@ProductPhotoID", SqlDbType.Int)  
        sprocCommand.Parameters(0).Value = photoId  
  
        'TODO: Is getting chunks the best way to retrieve LOB from the database?  Is there a limit?  
        Try  
            sqlReader = sprocCommand.ExecuteReader() 'CommandBehavior.SequentialAccess  
            If sqlReader Is Nothing Then  
                LogError(currentDirectory, "ExecuteReader failed!")  
            Else  
                If sqlReader.Read() Then  
                    ' Create a file to hold the output.  
                    If (Not Directory.Exists(currentDirectory)) Then  
                        Directory.CreateDirectory(currentDirectory)  
                    End If  
  
                    fileName = currentDirectory + fileName  
                    Dim fileStream As New FileStream(fileName, FileMode.OpenOrCreate, FileAccess.Write)  
                    Try  
                        Dim binaryWriter As New BinaryWriter(fileStream)  
                        Try  
                            ' The BLOB byte() buffer to be filled by GetBytes.  
                            Dim outbyte(bufferSize) As Byte  
  
                            ' The starting position in the BLOB output.  
                            Dim startIndex As Long = 0  
  
                            ' Read the bytes into outbyte() and retain the number of bytes returned.  
                            Dim retval As Long = sqlReader.GetBytes(0, startIndex, outbyte, 0, bufferSize)  
  
                            ' Continue reading and writing while there are   
                            ' bytes beyond the size of the buffer.  
                            While retval = bufferSize  
                                binaryWriter.Write(outbyte)  
  
                                ' Reposition the start index to the end of   
                                ' the last buffer and fill the buffer.  
                                startIndex += bufferSize  
                                retval = sqlReader.GetBytes(0, startIndex, outbyte, 0, bufferSize)  
                            End While  
  
                            ' Write the remaining buffer.  
                            binaryWriter.Write(outbyte)  
                        Finally  
                            binaryWriter.Close()  
                        End Try  
                    Finally  
                        fileStream.Close()  
                    End Try 'binaryWriter.Flush();  
                Else  
                    LogError(currentDirectory, "No row returned!")  
                End If  
            End If  
        Catch e As SqlException  
            LogError(currentDirectory, String.Format(CultureInfo.InvariantCulture, _  
                "Unable to copy binary contents from database.  Error: {0}", e.ToString()))  
        Finally  
            If Not (sqlReader Is Nothing) Then  
                sqlReader.Close()  
            End If  
            'dispoae the conn  
            If Not (conn Is Nothing) Then  
                conn.Close()  
                conn.Dispose()  
            End If  
        End Try  
    End Sub  
  
    ''' <summary>  
    ''' Saves a thumbnail picture into the database from a file accessible to the server.  
    ''' </summary>  
    ''' <param name="photoId">Unique identifier for a product picture.</param>  
    ''' <param name="currentDirectory">Which folder to get the picture from.</param>  
    ''' <param name="fileName">What the picture in the specified folder is called.</param>  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub PutPhotoIntoDB(ByVal photoId As Integer, _  
        ByVal currentDirectory As String, ByVal fileName As String)  
        'TODO: Is there a limit on how large the LOB can be?  
        Dim fullFileName As String = currentDirectory + fileName  
        Dim bytes As Byte() = ReadFile(fullFileName)  
  
        Try  
            Dim conn As SqlConnection = New SqlConnection("context connection = true")  
            conn.Open()  
  
            Dim sprocCommand As SqlCommand = conn.CreateCommand()  
            sprocCommand.CommandText = "dbo.usp_UpdateImage"  
            sprocCommand.CommandType = CommandType.StoredProcedure  
  
            sprocCommand.Parameters.Add(New SqlParameter("@ProductPhotoID", SqlDbType.Int))  
            ' Add time to the short name because there is an unique constraint on this column.  
            sprocCommand.Parameters(0).Value = photoId  
            sprocCommand.Parameters.Add(New SqlParameter("@ThumbNailPhoto", SqlDbType.VarBinary))  
            sprocCommand.Parameters(1).Value = bytes  
            sprocCommand.ExecuteNonQuery()  
        Catch e As SqlException  
            LogError(currentDirectory, String.Format(CultureInfo.InvariantCulture, _  
                "Unable to update binary contents into the database.  Error: {0}", e.ToString()))  
        End Try  
    End Sub  
  
    ''' <summary>  
    ''' Read the contents of a file and return the bytes.  
    ''' </summary>  
    ''' <param name="fileName">The name of the file to be read.</param>  
    ''' <returns></returns>  
    Private Shared Function ReadFile(ByVal fileName As String) As Byte()  
        ' Open the file assuming the file is in ASCII format.  
        'Dim binaryReader As New BinaryReader(CType(File.OpenRead(fileName), Stream), System.Text.Encoding.ASCII)  
        'Try  
        '    Dim fileSize As Long = binaryReader.BaseStream.Length  
        '    Dim bytes() As Byte = New Byte(CType(fileSize, Integer)) {}  
        '    binaryReader.Read(bytes, 0, CType(fileSize, Integer))  
        '    Return bytes  
        'Finally  
        '    binaryReader.Close()  
        'End Try  
  
        Dim binaryReader As New BinaryReader(CType(File.OpenRead(fileName), Stream), System.Text.Encoding.ASCII)  
        Using (binaryReader)  
            Dim fileSize As Long = binaryReader.BaseStream.Length  
            Dim bytes() As Byte = New Byte(CType(fileSize, Integer)) {}  
            binaryReader.Read(bytes, 0, CType(fileSize, Integer))  
            Return bytes  
        End Using  
  
    End Function  
  
    ''' <summary>  
    '''        Appends a message to a file accessible to the server.  When System.Diagnostics is available from  
    '''        CLR Sprocs this should be changed to use the event log.  
    ''' </summary>  
    ''' <param name="currentDirectory">Which folder the message log file resides in</param>  
    ''' <param name="errorMessage">The text to add to the message log file</param>  
    Private Shared Sub LogError(ByVal currentDirectory As String, ByVal errorMessage As String)  
        Dim errorLogStream As New FileStream(currentDirectory + "error.log", FileMode.Append, FileAccess.Write)  
        Try  
            Dim errorLogWriter As New StreamWriter(errorLogStream)  
            Try  
                errorLogWriter.WriteLine(errorMessage)  
            Finally  
                errorLogWriter.Close()  
            End Try  
        Finally  
            errorLogStream.Close()  
        End Try  
    End Sub  
End Class  
  
```  
  
 Este es el script (`Install.sql`) de instalación de [!INCLUDE[tsql](../../includes/tsql-md.md)], que implementa el ensamblado y crea los objetos de seguridad y los procedimientos almacenados que se requieren en este ejemplo.  
  
```  
USE AdventureWorks  
GO  
  
-- Drop procedures defined in this script if they exist  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'usp_UpdateImage')  
DROP PROCEDURE [dbo].[usp_UpdateImage];  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'GetPhotoFromDB')  
DROP PROCEDURE [dbo].[GetPhotoFromDB];  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'PutPhotoIntoDB')  
DROP PROCEDURE [dbo].[PutPhotoIntoDB];  
GO  
  
-- If the assembly we want to add already exists, drop it.  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'HandlingLOBUsingCLR')  
DROP ASSEMBLY HandlingLOBUsingCLR;  
GO  
use master  
go  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
  
--Before we register the assembly to SQL Server, we must arrange for the appropriate permissions.  
--Assemblies with unsafe or external_access permissions can only be registered and operate correctly  
--if either the database trustworthy bit is set or if the assembly is signed with a key,  
--that key is registered with SQL Server, a server principal is created from that key,  
--and that principal is granted the external access or unsafe assembly permission.  We choose  
--the latter approach as it is more granular, and therefore safer.  You should never  
--register an assembly with SQL Server (especially with external_access or unsafe permissions) without  
--thoroughly reviewing the source code of the assembly to make sure that its actions   
--do not pose an operational or security risk for your site.  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath = N'C:\MySample\'  
  
EXEC('CREATE ASYMMETRIC KEY ExternalSample_Key FROM EXECUTABLE FILE = ''' + @SamplesPath + 'HandlingLOBUsingCLR.dll'';');  
CREATE LOGIN ExternalSample_Login FROM ASYMMETRIC KEY ExternalSample_Key  
GRANT EXTERNAL ACCESS ASSEMBLY TO ExternalSample_Login  
GO  
  
USE AdventureWorks  
GO  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath = N'C:\MySample\'  
CREATE ASSEMBLY HandlingLOBUsingCLR  
FROM @SamplesPath + 'HandlingLOBUsingCLR.dll'  
WITH permission_set = external_access;  
GO  
  
-- Register the CLR method for retrieving thumbnail photos from the ProductPhoto table  
  
CREATE PROCEDURE [dbo].[GetPhotoFromDB]  
(  
    @ProductPhotoID int  
    ,@CurrentDirectory nvarchar(1024)  
    ,@FileName nvarchar(1024)     
)  
AS EXTERNAL NAME HandlingLOBUsingCLR.[LargeObjectBinary].GetPhotoFromDB;  
GO  
  
-- Register the CLR method for storing thumbnail photos into the ProductPhoto table  
  
CREATE PROCEDURE [dbo].[PutPhotoIntoDB]  
(  
    @ProductPhotoID int  
    ,@CurrentDirectory nvarchar(1024)  
    ,@FileName nvarchar(1024)     
)  
AS EXTERNAL NAME HandlingLOBUsingCLR.[LargeObjectBinary].PutPhotoIntoDB;  
GO  
  
-- Add a helper T-SQL method which does the actual work of updating the row  
  
CREATE PROCEDURE [dbo].[usp_UpdateImage]  
/* **********************************************************************************  
   Date:    April 22, 2003  
   Purpose: Change a thumbnail picture stored in the ProductPhoto table.  
   ********************************************************************************** */  
    @ProductPhotoID int  
    ,@ThumbNailPhoto AS VARBINARY(max)  
AS  
BEGIN  
    SET NOCOUNT ON;  
  
BEGIN TRY  
    UPDATE Production.ProductPhoto   
        SET ThumbNailPhoto = @ThumbNailPhoto  
        WHERE ProductPhotoID = @ProductPhotoID;  
    IF(@@ROWCOUNT < 1)  
        RAISERROR ('Update failed.', 16, 1);  
END TRY  
BEGIN CATCH  
        SELECT   
ERROR_NUMBER() AS ErrorNumber,  
ERROR_SEVERITY() AS ErrorSeverity,  
ERROR_STATE() as ErrorState,  
ERROR_PROCEDURE() as ErrorProcedure,  
ERROR_LINE() as ErrorLine,  
ERROR_MESSAGE() as ErrorMessage;  
        RAISERROR ('Update failed.', 16, 1);  
END CATCH;  
END  -- END of sp_InsertDocument  
GO  
```  
  
 La siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] (`test.sql`) prueba el ejemplo ejecutando los procedimientos almacenados.  
  
```  
USE AdventureWorks  
GO  
  
EXEC GetPhotoFromDB 70, 'C:\Temp\', 'test6.gif';  
go  
  
EXEC PutPhotoIntoDB 70, 'C:\Temp\', 'test6.gif';  
go  
  
```  
  
 El siguiente código de [!INCLUDE[tsql](../../includes/tsql-md.md)] quita el ensamblado, el inicio de sesión, la clave y los procedimientos almacenados de la base de datos.  
  
```  
  
USE AdventureWorks  
GO  
  
-- Drop procedures defined in the install script if they exist  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'usp_UpdateImage')  
DROP PROCEDURE [dbo].[usp_UpdateImage];  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'GetPhotoFromDB')  
DROP PROCEDURE [dbo].[GetPhotoFromDB];  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'PutPhotoIntoDB')  
DROP PROCEDURE [dbo].[PutPhotoIntoDB];  
GO  
  
-- If the assembly exists, drop it.  
  
IF EXISTS (SELECT [name] FROM sys.assemblies WHERE [name] = N'HandlingLOBUsingCLR')  
DROP ASSEMBLY HandlingLOBUsingCLR;  
GO  
  
USE master  
GO  
  
IF EXISTS (SELECT * FROM sys.server_principals WHERE [name] = 'ExternalSample_Login')  
DROP LOGIN ExternalSample_Login;  
GO  
  
IF EXISTS (SELECT * FROM sys.asymmetric_keys WHERE [name] = 'ExternalSample_Key')  
DROP ASYMMETRIC KEY ExternalSample_Key;  
GO  
USE AdventureWorks  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Escenarios de uso y ejemplos para la integración de Common Language Runtime &#40;CLR&#41;](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
