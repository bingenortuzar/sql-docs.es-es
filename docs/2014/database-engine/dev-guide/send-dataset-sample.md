---
title: Ejemplo de conjunto de datos de envío | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: d10dacbc-1b0f-4a4b-b53b-83eae2a6d809
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1a75160826fad9df3e6a401e72cc85b5a8c8c6e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62780962"
---
# <a name="send-dataset-sample"></a>Ejemplo de envío de conjunto de datos
  El ejemplo Send `DataSet` muestra cómo devolver un `DataSet` basado en ADO.NET dentro de un procedimiento almacenado basado en Common Language Runtime (CLR) del servidor como un conjunto de resultados para el cliente. Esto resulta útil, por ejemplo, cuando dicho procedimiento almacenado rellena un `DataSet` con los resultados de una consulta y, después, manipula los datos incluidos en ese `DataSet`. También es útil si el procedimiento almacenado crea y rellena un `DataSet` desde el principio. El ejemplo está compuesto por dos clases, `DataSetUtilities` y `TestSendDataSet`. El método `SendDataSet` de la clase `DataSetUtilities` implementa un modo general de transmitir el contenido de una instancia de un `DataSet` al cliente. El método `DoTest` definido en la clase `TestSendDataSet` comprueba que el método `SendDataSet` funciona creando un `DataSet` que rellena con datos del procedimiento almacenado de Transact-SQL `uspGetTwoBOMTestData` . `uspGetTwoBOMTestData` ejecuta el procedimiento almacenado de Transact-SQL `uspGetBillOfMaterials` dos veces para consultar de forma recursiva la lista de materiales de dos productos especificados como parámetros en el procedimiento almacenado `usp_GetTwoBOMTestData` . Generalmente, después de rellenar el conjunto de datos, los datos se modificarían antes de invocar a `SendDataSet` para entregar al cliente los datos del conjunto de datos en forma de conjunto de resultados. Para simplificar, este ejemplo devuelve los datos sin modificar.  
  
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
  
3.  En c:\MySample, cree `SendDataSet.vb` (para el ejemplo de Visual Basic) o `SendDataSet.cs` (para el ejemplo de C#) y copie el código muestra de Visual Basic o de C# que corresponda (más abajo) en el archivo.  
  
4.  Compile el código muestra en el ensamblado requerido ejecutando en el símbolo del sistema uno de los comandos siguientes, dependiendo de su opción de lenguaje.  
  
    -   `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll  /target:library SendDataSet.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /target:library SendDataSet.cs`  
  
5.  Copie el código de instalación de [!INCLUDE[tsql](../../includes/tsql-md.md)] en un archivo y guárdelo como `Install.sql` en el directorio de ejemplo.  
  
6.  Si el ejemplo está instalado en un directorio distinto de `C:\MySample\`, edite el archivo `Install.sql` del archivo como se indica para señalar esa ubicación.  
  
7.  Implemente el ensamblado, el procedimiento almacenado y las funciones ejecutando  
  
    -   `sqlcmd -E -I -i install.sql`  
  
8.  Copie el script de prueba [!INCLUDE[tsql](../../includes/tsql-md.md)] en un archivo y guárdelo como `test.sql` en el directorio de ejemplo.  
  
    -   `sqlcmd -E -I -i test.sql`  
  
9. Copie el script de limpieza de [!INCLUDE[tsql](../../includes/tsql-md.md)] en un archivo y guárdelo como `cleanup.sql` en el directorio de ejemplo.  
  
10. Ejecute el script con el siguiente comando  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>Código muestra  
 A continuación se muestran las listas de código para este ejemplo.  
  
 C#  
  
```  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
    public static class DataSetUtilities  
    {  
  
        public static void SendDataSet(DataSet ds)  
        {  
            if (ds == null)  
            {  
                throw new ArgumentException("SendDataSet requires a non-null data set.");  
            }  
            else  
            {  
                foreach (DataTable dt in ds.Tables)  
                {  
                    SendDataTable(dt);  
                }  
            }  
        }  
  
        public static void SendDataTable(DataTable dt)  
        {  
            bool[] coerceToString;  // Do we need to coerce this column to string?  
            SqlMetaData[] metaData = ExtractDataTableColumnMetaData(dt, out coerceToString);  
  
            SqlDataRecord record = new SqlDataRecord(metaData);  
            SqlPipe pipe = SqlContext.Pipe;  
            pipe.SendResultsStart(record);  
            try  
            {  
                foreach (DataRow row in dt.Rows)  
                {  
                    for (int index = 0; index < record.FieldCount; index++)  
                    {  
                        object value = row[index];  
                        if (null != value && coerceToString[index])  
                            value = value.ToString();  
                        record.SetValue(index, value);  
                    }  
  
                    pipe.SendResultsRow(record);  
                }  
            }  
            finally  
            {  
                pipe.SendResultsEnd();  
            }  
        }  
  
        private static SqlMetaData[] ExtractDataTableColumnMetaData(DataTable dt, out bool[] coerceToString)  
        {  
            SqlMetaData[] metaDataResult = new SqlMetaData[dt.Columns.Count];  
            coerceToString = new bool[dt.Columns.Count];  
            for (int index = 0; index < dt.Columns.Count; index++)  
            {  
                DataColumn column = dt.Columns[index];  
                metaDataResult[index] = SqlMetaDataFromColumn(column, out coerceToString[index]);  
            }  
  
            return metaDataResult;  
        }  
  
        private static Exception InvalidDataTypeCode(TypeCode code)  
        {  
            return new ArgumentException("Invalid type: " + code);  
        }  
  
        private static Exception UnknownDataType(Type clrType)  
        {  
            return new ArgumentException("Unknown type: " + clrType);  
        }  
  
        private static SqlMetaData SqlMetaDataFromColumn(DataColumn column, out bool coerceToString)  
        {  
            coerceToString = false;  
            SqlMetaData sql_md = null;  
            Type clrType = column.DataType;  
            string name = column.ColumnName;  
            switch (Type.GetTypeCode(clrType))  
            {  
                case TypeCode.Boolean: sql_md = new SqlMetaData(name, SqlDbType.Bit); break;  
                case TypeCode.Byte: sql_md = new SqlMetaData(name, SqlDbType.TinyInt); break;  
                case TypeCode.Char: sql_md = new SqlMetaData(name, SqlDbType.NVarChar, 1); break;  
                case TypeCode.DateTime: sql_md = new SqlMetaData(name, SqlDbType.DateTime); break;  
                case TypeCode.DBNull: throw InvalidDataTypeCode(TypeCode.DBNull);  
                case TypeCode.Decimal: sql_md = new SqlMetaData(name, SqlDbType.Decimal, 18, 0); break;  
                case TypeCode.Double: sql_md = new SqlMetaData(name, SqlDbType.Float); break;  
                case TypeCode.Empty: throw InvalidDataTypeCode(TypeCode.Empty);  
                case TypeCode.Int16: sql_md = new SqlMetaData(name, SqlDbType.SmallInt); break;  
                case TypeCode.Int32: sql_md = new SqlMetaData(name, SqlDbType.Int); break;  
                case TypeCode.Int64: sql_md = new SqlMetaData(name, SqlDbType.BigInt); break;  
                case TypeCode.SByte: throw InvalidDataTypeCode(TypeCode.SByte);  
                case TypeCode.Single: sql_md = new SqlMetaData(name, SqlDbType.Real); break;  
                case TypeCode.String: sql_md = new SqlMetaData(name, SqlDbType.NVarChar, column.MaxLength);  
                    break;  
                case TypeCode.UInt16: throw InvalidDataTypeCode(TypeCode.UInt16);  
                case TypeCode.UInt32: throw InvalidDataTypeCode(TypeCode.UInt32);  
                case TypeCode.UInt64: throw InvalidDataTypeCode(TypeCode.UInt64);  
                case TypeCode.Object:  
                    sql_md = SqlMetaDataFromObjectColumn(name, column, clrType);  
                    if (sql_md == null)  
                    {  
                        // Unknown type, try to treat it as string;  
                        sql_md = new SqlMetaData(name, SqlDbType.NVarChar, column.MaxLength);  
                        coerceToString = true;  
                    }  
                    break;  
  
                default: throw UnknownDataType(clrType);  
            }  
  
            return sql_md;  
        }  
  
        private static SqlMetaData SqlMetaDataFromObjectColumn(string name, DataColumn column, Type clrType)  
        {  
            SqlMetaData sql_md = null;  
            if (clrType == typeof(System.Byte[]) || clrType == typeof(SqlBinary) || clrType == typeof(SqlBytes) ||  
        clrType == typeof(System.Char[]) || clrType == typeof(SqlString) || clrType == typeof(SqlChars))  
                sql_md = new SqlMetaData(name, SqlDbType.VarBinary, column.MaxLength);  
            else if (clrType == typeof(System.Guid))  
                sql_md = new SqlMetaData(name, SqlDbType.UniqueIdentifier);  
            else if (clrType == typeof(System.Object))  
                sql_md = new SqlMetaData(name, SqlDbType.Variant);  
            else if (clrType == typeof(SqlBoolean))  
                sql_md = new SqlMetaData(name, SqlDbType.Bit);  
            else if (clrType == typeof(SqlByte))  
                sql_md = new SqlMetaData(name, SqlDbType.TinyInt);  
            else if (clrType == typeof(SqlDateTime))  
                sql_md = new SqlMetaData(name, SqlDbType.DateTime);  
            else if (clrType == typeof(SqlDouble))  
                sql_md = new SqlMetaData(name, SqlDbType.Float);  
            else if (clrType == typeof(SqlGuid))  
                sql_md = new SqlMetaData(name, SqlDbType.UniqueIdentifier);  
            else if (clrType == typeof(SqlInt16))  
                sql_md = new SqlMetaData(name, SqlDbType.SmallInt);  
            else if (clrType == typeof(SqlInt32))  
                sql_md = new SqlMetaData(name, SqlDbType.Int);  
            else if (clrType == typeof(SqlInt64))  
                sql_md = new SqlMetaData(name, SqlDbType.BigInt);  
            else if (clrType == typeof(SqlMoney))  
                sql_md = new SqlMetaData(name, SqlDbType.Money);  
            else if (clrType == typeof(SqlDecimal))  
                sql_md = new SqlMetaData(name, SqlDbType.Decimal, SqlDecimal.MaxPrecision, 0);  
            else if (clrType == typeof(SqlSingle))  
                sql_md = new SqlMetaData(name, SqlDbType.Real);  
            else if (clrType == typeof(SqlXml))  
                sql_md = new SqlMetaData(name, SqlDbType.Xml);  
            else  
                sql_md = null;  
  
            return sql_md;  
        }  
  
    }  
 public static class TestSendDataSet  
    {  
        private const string TestConnectionString = "context connection=true";  
        const int prod1ID = 750; //Product ID of Road-150 Red, 44 bicycle  
        const int prod2ID = 751; //Product ID of Road-150 Red, 48 bicycle  
  
        /// <summary>  
        /// Invoke a stored procedure to get some bill of material information and   
        /// fill a data set with the two result sets.  Return the data set to the client.  
        /// </summary>  
        public static void DoTest()  
        {  
            using (SqlConnection conn = new SqlConnection(TestConnectionString))  
            {  
                SqlCommand cmd = conn.CreateCommand();  
                cmd.CommandText = "usp_GetTwoBOMTestData";  
                cmd.CommandType = CommandType.StoredProcedure;  
  
                SqlParameter prod1Param = new SqlParameter("@ProductID1", SqlDbType.Int);  
                prod1Param.Value = prod1ID;  
                cmd.Parameters.Add(prod1Param);  
  
                SqlParameter prod2Param = new SqlParameter("@ProductID2", SqlDbType.Int);  
                prod2Param.Value = prod2ID;  
                cmd.Parameters.Add(prod2Param);  
  
                SqlParameter asOfDateParam = new SqlParameter("@AsOfDate", SqlDbType.DateTime);  
                asOfDateParam.Value = DateTime.Now;  
                cmd.Parameters.Add(asOfDateParam);  
  
                DataSet ds = new DataSet("TestData");  
                SqlDataAdapter sda = new SqlDataAdapter(cmd);  
                conn.Open();  
                sda.Fill(ds);  
  
// Normally, after filling the data set, rather than immediately returning it,   
// the data would be modified before invoking SendDataSet to deliver   
// the data within the data set as a result set to the client.  For simplicity   
// this sample simply returns the data.  
  
                DataSetUtilities.SendDataSet(ds);  
  
            }  
        }  
  
    }  
```  
  
 Visual Basic  
  
```  
Imports Microsoft.VisualBasic  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Diagnostics  
Imports System.Collections.Generic  
Imports System.Text  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Runtime.InteropServices  
  
Public Class DataSetUtilities  
  
    Public Shared Sub SendDataSet(ByVal ds As DataSet)  
        If ds Is Nothing Then  
            Throw New ArgumentException("SendDataSet requires a non-null data set.")  
        Else  
            For Each dt As DataTable In ds.Tables  
                SendDataTable(dt)  
            Next  
        End If  
    End Sub  
  
    Public Shared Sub SendDataTable(ByVal dt As DataTable)  
        Dim coerceToString() As Boolean = Nothing ' Do we need to coerce this column to string?  
        Dim metaData As SqlMetaData() = ExtractDataTableColumnMetaData(dt, coerceToString)  
  
        Dim record As New SqlDataRecord(metaData)  
        Dim pipe As SqlPipe = SqlContext.Pipe  
        pipe.SendResultsStart(record)  
  
        Try  
            For Each row As DataRow In dt.Rows  
                For index As Integer = 0 To record.FieldCount - 1  
                    Dim value As Object = row(index)  
                    If Nothing Is value AndAlso coerceToString(index) Then  
                        value = value.ToString()  
                    End If  
  
                    record.SetValue(index, value)  
                Next  
  
                pipe.SendResultsRow(record)  
            Next  
        Finally  
            pipe.SendResultsEnd()  
        End Try  
    End Sub  
  
    Private Shared Function ExtractDataTableColumnMetaData(ByVal dt As DataTable, <Out()> ByRef coerceToString() As Boolean) As SqlMetaData()  
        Dim metaDataResult(dt.Columns.Count - 1) As SqlMetaData  
        coerceToString = New Boolean(dt.Columns.Count - 1) {}  
        For index As Integer = 0 To dt.Columns.Count - 1  
            Dim column As DataColumn = dt.Columns(index)  
            metaDataResult(index) = SqlMetaDataFromColumn(column, coerceToString(index))  
        Next  
  
        Return metaDataResult  
    End Function  
    Private Shared Function InvalidDataTypeCode(ByVal code As TypeCode) As Exception  
        Return New ArgumentException("Invalid type: " & code.ToString())  
    End Function  
  
    Private Shared Function UnknownDataType(ByVal clrType As Type) As Exception  
        Return New ArgumentException("Unknown type: " & clrType.ToString())  
    End Function  
  
    Private Shared Function SqlMetaDataFromColumn(ByVal column As DataColumn, ByRef coerceToString As Boolean) As SqlMetaData  
        coerceToString = False  
        Dim sql_md As SqlMetaData = Nothing  
        Dim clrType As Type = column.DataType  
        Dim name As String = column.ColumnName  
        Select Case Type.GetTypeCode(clrType)  
            Case TypeCode.Boolean  
                sql_md = New SqlMetaData(name, SqlDbType.Bit)  
            Case TypeCode.Byte  
                sql_md = New SqlMetaData(name, SqlDbType.TinyInt)  
            Case TypeCode.Char  
                sql_md = New SqlMetaData(name, SqlDbType.NVarChar, 1)  
            Case TypeCode.DateTime  
                sql_md = New SqlMetaData(name, SqlDbType.DateTime)  
            Case TypeCode.DBNull  
                Throw InvalidDataTypeCode(TypeCode.DBNull)  
            Case TypeCode.Decimal  
                sql_md = New SqlMetaData(name, SqlDbType.Decimal)  
            Case TypeCode.Double  
                sql_md = New SqlMetaData(name, SqlDbType.Float)  
            Case TypeCode.Empty  
                Throw InvalidDataTypeCode(TypeCode.Empty)  
            Case TypeCode.Int16  
                sql_md = New SqlMetaData(name, SqlDbType.SmallInt)  
            Case TypeCode.Int32  
                sql_md = New SqlMetaData(name, SqlDbType.Int)  
            Case TypeCode.Int64  
                sql_md = New SqlMetaData(name, SqlDbType.BigInt)  
            Case TypeCode.SByte  
                Throw InvalidDataTypeCode(TypeCode.SByte)  
            Case TypeCode.Single  
                sql_md = New SqlMetaData(name, SqlDbType.Real)  
            Case TypeCode.String  
                sql_md = New SqlMetaData(name, SqlDbType.NVarChar, column.MaxLength)  
            Case TypeCode.UInt16  
                Throw InvalidDataTypeCode(TypeCode.UInt16)  
            Case TypeCode.UInt32  
                Throw InvalidDataTypeCode(TypeCode.UInt32)  
            Case TypeCode.UInt64  
                Throw InvalidDataTypeCode(TypeCode.UInt64)  
            Case TypeCode.Object  
                sql_md = SqlMetaDataFromObjectColumn(name, column, clrType)  
                If sql_md Is Nothing Then  
                    ' Unknown type, try to treat it as string  
                    sql_md = New SqlMetaData(name, SqlDbType.NVarChar, column.MaxLength)  
                    coerceToString = True  
                End If  
            Case Else  
                Throw UnknownDataType(clrType)  
        End Select  
  
        Return sql_md  
    End Function  
  
    Private Shared Function SqlMetaDataFromObjectColumn(ByVal name As String, ByVal column As DataColumn, ByVal clrType As Type) As SqlMetaData  
        Dim sql_md As SqlMetaData = Nothing  
  
        If (clrType Is GetType(System.Byte()) OrElse clrType Is GetType(SqlBinary) OrElse clrType Is GetType(SqlBytes) _  
            OrElse clrType Is GetType(System.Char()) OrElse clrType Is GetType(SqlString) OrElse clrType Is GetType(SqlChars)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.VarBinary, column.MaxLength)  
        ElseIf (clrType Is GetType(System.Guid)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.UniqueIdentifier)  
        ElseIf (clrType Is GetType(System.Object)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.Variant)  
        ElseIf (clrType Is GetType(SqlBoolean)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.Bit)  
        ElseIf (clrType Is GetType(SqlByte)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.TinyInt)  
        ElseIf (clrType Is GetType(SqlDateTime)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.DateTime)  
        ElseIf (clrType Is GetType(SqlDouble)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.Float)  
        ElseIf (clrType Is GetType(SqlGuid)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.UniqueIdentifier)  
        ElseIf (clrType Is GetType(SqlInt16)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.SmallInt)  
        ElseIf (clrType Is GetType(SqlInt32)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.Int)  
        ElseIf (clrType Is GetType(SqlInt64)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.BigInt)  
        ElseIf (clrType Is GetType(SqlMoney)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.Money)  
        ElseIf (clrType Is GetType(SqlDecimal)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.Decimal, SqlDecimal.MaxPrecision, 0)  
        ElseIf (clrType Is GetType(SqlSingle)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.Real)  
        ElseIf (clrType Is GetType(SqlXml)) Then  
            sql_md = New SqlMetaData(name, SqlDbType.Xml)  
        Else  
            sql_md = Nothing  
        End If  
  
        Return sql_md  
    End Function  
End Class  
  
Public Class TestSendDataSet  
    Private Const TestConnectionString As String = "context connection=true"  
    Private Const prod1ID As Integer = 750  'Product ID of Road-150 Red, 44 bicycle  
    Private Const prod2ID As Integer = 751  'Product ID of Road-150 Red, 48 bicycle  
  
    ''' <summary>  
    ''' Invoke a stored procedure to get some bill of material information and   
    ''' fill a data set with the two result sets.  Return the data set to the client.  
  
    <SqlProcedure(Name:="usp_TestSendDataSet")> _  
    Public Shared Sub DoTest()  
        Dim conn As New SqlConnection(TestConnectionString)  
        Try  
            Dim cmd As SqlCommand = conn.CreateCommand()  
            cmd.CommandText = "usp_GetTwoBOMTestData"  
            cmd.CommandType = CommandType.StoredProcedure  
  
            Dim prod1Param As New SqlParameter("@ProductID1", SqlDbType.Int)  
            prod1Param.Value = prod1ID  
            cmd.Parameters.Add(prod1Param)  
  
            Dim prod2Param As New SqlParameter("@ProductID2", SqlDbType.Int)  
            prod2Param.Value = prod2ID  
            cmd.Parameters.Add(prod2Param)  
  
            Dim asOfDateParam As New SqlParameter("@AsOfDate", SqlDbType.DateTime)  
            asOfDateParam.Value = DateTime.Now  
            cmd.Parameters.Add(asOfDateParam)  
  
            Dim ds As New DataSet("TestData")  
            Dim sda As New SqlDataAdapter(cmd)  
            conn.Open()  
            sda.Fill(ds)  
  
            ' Normally, after filling the data set, rather than immediately returning it,   
            ' the data would be modified before invoking SendDataSet to deliver   
            ' the data within the data set as a result set to the client.  For simplicity   
            ' this sample simply returns the data.  
            DataSetUtilities.SendDataSet(ds)  
        Finally  
            conn.Dispose()  
        End Try  
    End Sub  
End Class  
  
```  
  
 Este es el script de instalación de [!INCLUDE[tsql](../../includes/tsql-md.md)] (`Install.sql`), que implementa el ensamblado y crea los procedimientos almacenados.  
  
```  
USE AdventureWorks;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'usp_GetTwoBOMTestData')  
DROP PROCEDURE usp_GetTwoBOMTestData;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'usp_TestSendDataSet')  
DROP PROCEDURE usp_TestSendDataSet;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = N'SendDataSet')   
DROP ASSEMBLY SendDataSet;  
GO  
  
-- Procedure used to generate test data to fill the data set being returned to the client  
CREATE PROCEDURE usp_GetTwoBOMTestData  
(  
@ProductID1 int,  
@ProductID2 int,  
@AsOfDate DateTime  
)  
AS  
BEGIN  
EXEC uspGetBillOfMaterials @ProductID1, @AsOfDate;  
EXEC uspGetBillOfMaterials @ProductID2, @AsOfDate;  
END;  
GO  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
Set @SamplesPath = N'C:\MySample\'  
  
CREATE ASSEMBLY SendDataSet from @SamplesPath +'SendDataSet.dll'  
WITH PERMISSION_SET = Safe;  
GO  
  
CREATE PROCEDURE usp_TestSendDataSet  
AS  
EXTERNAL NAME [SendDataSet].[TestSendDataSet].[DoTest];  
GO  
```  
  
 Este es el script de prueba de [!INCLUDE[tsql](../../includes/tsql-md.md)] (`test.sql`), que prueba el ejemplo.  
  
```  
USE AdventureWorks  
GO  
  
EXEC usp_TestSendDataSet  
GO  
```  
  
 El script [!INCLUDE[tsql](../../includes/tsql-md.md)] siguiente quita el ensamblado y el procedimiento almacenado de la base de datos.  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'usp_GetTwoBOMTestData')  
DROP PROCEDURE usp_GetTwoBOMTestData;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'usp_TestSendDataSet')  
DROP PROCEDURE usp_TestSendDataSet;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = N'SendDataSet')   
DROP ASSEMBLY SendDataSet;  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Escenarios de uso y ejemplos para la integración de Common Language Runtime &#40;CLR&#41;](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
