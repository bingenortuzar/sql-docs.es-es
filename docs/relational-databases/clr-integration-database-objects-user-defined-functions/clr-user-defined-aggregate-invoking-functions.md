---
title: Invocar funciones de agregado definido por el usuario CLR | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- aggregate functions [CLR integration]
- invoking user-defined aggregate functions
- user-defined functions [CLR integration]
ms.assetid: 5a188b50-7170-4069-acad-5de5c915f65d
author: rothja
ms.author: jroth
ms.openlocfilehash: 53cd38b80b6884e9be5c41042fac34b68ec2cda0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028376"
---
# <a name="clr-user-defined-aggregate---invoking-functions"></a>Agregado definido por el usuario de CLR: invocar funciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En las instrucciones SELECT de [!INCLUDE[tsql](../../includes/tsql-md.md)], puede invocar agregados definidos por el usuario de Common Language Runtime (CLR), siguiendo todas las reglas que se aplican a las funciones de agregado del sistema.  
  
 Se aplican las siguientes reglas adicionales:  
  
-   El usuario actual debe tener **EXECUTE** permiso en el agregado definido por el usuario.  
  
-   Agregados definidos por el usuario se deben invocar utilizando un nombre de dos partes en forma de *nombre_esquema.nombre_agrdu*.  
  
-   El tipo de argumento del agregado definido por el usuario debe coincidir con o ser implícitamente convertible a la *input_type* del agregado, tal como se define en el **CREATE AGGREGATE** instrucción.  
  
-   El tipo de valor devuelto del agregado definido por el usuario debe coincidir con el *return_type* en el **CREATE AGGREGATE** instrucción.  
  
## <a name="example-1"></a>Ejemplo 1  
 A continuación figura un ejemplo de una función de agregado definida por el usuario que concatena un conjunto de valores de cadena obtenido de una columna de una tabla:  
  
 [C#]  
  
```  
using System;  
using System.Data;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlTypes;  
using System.IO;  
using System.Text;  
  
[Serializable]  
[SqlUserDefinedAggregate(  
    Format.UserDefined, //use clr serialization to serialize the intermediate result  
    IsInvariantToNulls = true, //optimizer property  
    IsInvariantToDuplicates = false, //optimizer property  
    IsInvariantToOrder = false, //optimizer property  
    MaxByteSize = 8000) //maximum size in bytes of persisted value  
]  
public class Concatenate : IBinarySerialize  
{  
    /// <summary>  
    /// The variable that holds the intermediate result of the concatenation  
    /// </summary>  
    public StringBuilder intermediateResult;  
  
    /// <summary>  
    /// Initialize the internal data structures  
    /// </summary>  
    public void Init()  
    {  
        this.intermediateResult = new StringBuilder();  
    }  
  
    /// <summary>  
    /// Accumulate the next value, not if the value is null  
    /// </summary>  
    /// <param name="value"></param>  
    public void Accumulate(SqlString value)  
    {  
        if (value.IsNull)  
        {  
            return;  
        }  
  
        this.intermediateResult.Append(value.Value).Append(',');  
    }  
  
    /// <summary>  
    /// Merge the partially computed aggregate with this aggregate.  
    /// </summary>  
    /// <param name="other"></param>  
    public void Merge(Concatenate other)  
    {  
        this.intermediateResult.Append(other.intermediateResult);  
    }  
  
    /// <summary>  
    /// Called at the end of aggregation, to return the results of the aggregation.  
    /// </summary>  
    /// <returns></returns>  
    public SqlString Terminate()  
    {  
        string output = string.Empty;  
        //delete the trailing comma, if any  
        if (this.intermediateResult != null  
            && this.intermediateResult.Length > 0)  
        {  
            output = this.intermediateResult.ToString(0, this.intermediateResult.Length - 1);  
        }  
  
        return new SqlString(output);  
    }  
  
    public void Read(BinaryReader r)  
    {  
        intermediateResult = new StringBuilder(r.ReadString());  
    }  
  
    public void Write(BinaryWriter w)  
    {  
        w.Write(this.intermediateResult.ToString());  
    }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlTypes  
Imports System.IO  
Imports System.Text  
  
<Serializable(), SqlUserDefinedAggregate(Format.UserDefined, IsInvariantToNulls:=True, IsInvariantToDuplicates:=False, IsInvariantToOrder:=False, MaxByteSize:=8000)> _  
Public Class Concatenate  
    Implements IBinarySerialize  
  
    ''' <summary>  
    ''' The variable that holds the intermediate result of the concatenation  
    ''' </summary>  
    Public intermediateResult As StringBuilder  
  
    ''' <summary>  
    ''' Initialize the internal data structures  
    ''' </summary>  
    Public Sub Init()  
        Me.intermediateResult = New StringBuilder()  
    End Sub  
  
    ''' <summary>  
    ''' Accumulate the next value, not if the value is null  
    ''' </summary>  
    ''' <param name="value"></param>  
    Public Sub Accumulate(ByVal value As SqlString)  
        If value.IsNull Then  
            Return  
        End If  
  
        Me.intermediateResult.Append(value.Value).Append(","c)  
    End Sub  
    ''' <summary>  
    ''' Merge the partially computed aggregate with this aggregate.  
    ''' </summary>  
    ''' <param name="other"></param>  
    Public Sub Merge(ByVal other As Concatenate)  
        Me.intermediateResult.Append(other.intermediateResult)  
    End Sub  
  
    ''' <summary>  
    ''' Called at the end of aggregation, to return the results of the aggregation.  
    ''' </summary>  
    ''' <returns></returns>  
    Public Function Terminate() As SqlString  
        Dim output As String = String.Empty  
  
        'delete the trailing comma, if any  
        If Not (Me.intermediateResult Is Nothing) AndAlso Me.intermediateResult.Length > 0 Then  
            output = Me.intermediateResult.ToString(0, Me.intermediateResult.Length - 1)  
        End If  
  
        Return New SqlString(output)  
    End Function  
  
    Public Sub Read(ByVal r As BinaryReader) Implements IBinarySerialize.Read  
        intermediateResult = New StringBuilder(r.ReadString())  
    End Sub  
  
    Public Sub Write(ByVal w As BinaryWriter) Implements IBinarySerialize.Write  
        w.Write(Me.intermediateResult.ToString())  
    End Sub  
End Class  
```  
  
 Una vez compilado el código en **MyAgg.dll**, puede registrar el agregado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como sigue:  
  
```  
CREATE ASSEMBLY MyAgg FROM 'C:\MyAgg.dll';  
GO  
CREATE AGGREGATE MyAgg (@input nvarchar(200)) RETURNS nvarchar(max)  
EXTERNAL NAME MyAgg.Concatenate;  
```  
  
> [!NOTE]  
>  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no se admite la ejecución de objetos de base de datos de Visual C++, como las funciones escalares, que se han compilado con la opción /clr:pure del compilador.  
  
 Al igual que con la mayoría de los agregados, la mayor parte de la lógica en el **Accumulate** método. Aquí, la cadena que se pasa como un parámetro a la **Accumulate** método se anexa a la **StringBuilder** objeto que se inicializó en el **Init** método. Suponiendo que esto no es la primera vez el **Accumulate** ha llamado al método, también se anexa una coma a la **StringBuilder** antes de anexar la cadena pasada. Al finalizar las tareas de cálculo, el **Terminate** llama el método, que devuelve el **StringBuilder** como una cadena.  
  
 Considere, por ejemplo, una tabla con el siguiente esquema:  
  
```  
CREATE TABLE BookAuthors  
(  
   BookID   int       NOT NULL,  
   AuthorName    nvarchar(200) NOT NULL  
);  
```  
  
 A continuación, inserte las filas siguientes:  
  
```  
INSERT BookAuthors VALUES(1, 'Johnson'),(2, 'Taylor'),(3, 'Steven'),(2, 'Mayler'),(3, 'Roberts'),(3, 'Michaels');  
```  
  
 La consulta siguiente generará entonces el resultado siguiente:  
  
```  
SELECT BookID, dbo.MyAgg(AuthorName)  
FROM BookAuthors  
GROUP BY BookID;  
```  
  
|BookID|Nombres de autor|  
|------------|------------------|  
|1|Johnson|  
|2|Taylor, Mayler|  
|3|Roberts, Michaels, Steven|  
  
## <a name="example-2"></a>Ejemplo 2  
 El ejemplo siguiente muestra un agregado que tiene dos parámetros en la **Accumulate** método.  
  
 [C#]  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
[Serializable]  
[SqlUserDefinedAggregate(  
    Format.Native,  
    IsInvariantToDuplicates = false,  
    IsInvariantToNulls = true,  
    IsInvariantToOrder = true,  
    IsNullIfEmpty = true,  
    Name = "WeightedAvg")]  
public struct WeightedAvg  
{  
    /// <summary>  
    /// The variable that holds the intermediate sum of all values multiplied by their weight  
    /// </summary>  
    private long sum;  
  
    /// <summary>  
    /// The variable that holds the intermediate sum of all weights  
    /// </summary>  
    private int count;  
  
    /// <summary>  
    /// Initialize the internal data structures  
    /// </summary>  
    public void Init()  
    {  
        sum = 0;  
        count = 0;  
    }  
  
    /// <summary>  
    /// Accumulate the next value, not if the value is null  
    /// </summary>  
    /// <param name="Value">Next value to be aggregated</param>  
    /// <param name="Weight">The weight of the value passed to Value parameter</param>  
    public void Accumulate(SqlInt32 Value, SqlInt32 Weight)  
    {  
        if (!Value.IsNull && !Weight.IsNull)  
        {  
            sum += (long)Value * (long)Weight;  
            count += (int)Weight;  
        }  
    }  
  
    /// <summary>  
    /// Merge the partially computed aggregate with this aggregate  
    /// </summary>  
    /// <param name="Group">The other partial results to be merged</param>  
    public void Merge(WeightedAvg Group)  
    {  
        sum += Group.sum;  
        count += Group.count;  
    }  
  
    /// <summary>  
    /// Called at the end of aggregation, to return the results of the aggregation.  
    /// </summary>  
    /// <returns>The weighted average of all inputed values</returns>  
    public SqlInt32 Terminate()  
    {  
        if (count > 0)  
        {  
            int value = (int)(sum / count);  
            return new SqlInt32(value);  
        }  
        else  
        {  
            return SqlInt32.Null;  
        }  
    }  
}  
```  
  
 [Visual Basic]  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Runtime.InteropServices  
  
<StructLayout(LayoutKind.Sequential)> _  
<Serializable(), SqlUserDefinedAggregate(Format.Native, _  
IsInvariantToDuplicates:=False, _  
IsInvariantToNulls:=True, _  
IsInvariantToOrder:=True, _  
IsNullIfEmpty:=True, _  
Name:="WeightedAvg")> _  
Public Class WeightedAvg  
  
    ''' <summary>  
    ''' The variable that holds the intermediate sum of all values multiplied by their weight  
    ''' </summary>  
    Private sum As Long  
  
    ''' <summary>  
    ''' The variable that holds the intermediate sum of all weights  
    ''' </summary>  
    Private count As Integer  
  
    ''' <summary>  
    ''' The variable that holds the intermediate sum of all weights  
    ''' </summary>  
    Public Sub Init()  
        sum = 0  
        count = 0  
    End Sub  
  
    ''' <summary>  
    ''' Accumulate the next value, not if the value is null  
    ''' </summary>  
    ''' <param name="Value">Next value to be aggregated</param>  
    ''' <param name="Weight">The weight of the value passed to Value parameter</param>  
    Public Sub Accumulate(ByVal Value As SqlInt32, ByVal Weight As SqlInt32)  
        If Not Value.IsNull AndAlso Not Weight.IsNull Then  
            sum += CType(Value, Long) * CType(Weight, Long)  
            count += CType(Weight, Integer)  
        End If  
    End Sub  
  
    ''' <summary>  
    ''' Merge the partially computed aggregate with this aggregate.  
    ''' </summary>  
    ''' <param name="Group">The other partial results to be merged</param>  
    Public Sub Merge(ByVal Group As WeightedAvg)  
        sum = Group.sum  
        count = Group.count  
    End Sub  
  
    ''' <summary>  
    ''' Called at the end of aggregation, to return the results of the aggregation.  
    ''' </summary>  
    ''' <returns>The weighted average of all inputed values</returns>  
    Public Function Terminate() As SqlInt32  
        If count > 0 Then  
            ''                        int value = (int)(sum / count);  
            ''          return new SqlInt32(value);  
            Dim value As Integer = CType(sum / count, Integer)  
            Return New SqlInt32(value)  
        Else  
            Return SqlInt32.Null  
        End If  
    End Function  
End Class  
```  
  
 Después de compilar el código fuente de C# o Visual Basic, ejecute el siguiente código [!INCLUDE[tsql](../../includes/tsql-md.md)].  Para este script se asume que la DLL se denomina WghtAvg.dll y se encuentra en el directorio raíz de su unidad C.  También se asume una base de datos denominada test.  
  
```  
use test;  
go  
  
-- sp_configure 'clr enabled', 1;  
-- go  
  
--- RECONFIGURE WITH OVERRIDE;  
-- go  
  
IF EXISTS (SELECT name FROM systypes WHERE name = 'MyTableType')  
   DROP TYPE MyTableType;  
go  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'WeightedAvg')  
   DROP AGGREGATE WeightedAvg;  
go  
  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'MyClrCode')  
   DROP ASSEMBLY MyClrCode;  
go  
  
CREATE ASSEMBLY MyClrCode FROM 'C:\WghtAvg.dll';  
GO  
  
CREATE AGGREGATE WeightedAvg (@value int, @weight int) RETURNS int  
EXTERNAL NAME MyClrCode.WeightedAvg;  
go  
  
CREATE TYPE MyTableType AS table (ItemValue int, ItemWeight int);  
go  
  
DECLARE @myTable AS MyTableType;  
  
INSERT INTO @myTable VALUES(1, 4), (6, 1);  
  
SELECT dbo.WeightedAvg(ItemValue, ItemWeight) FROM @myTable;  
go  
```  
  
## <a name="see-also"></a>Vea también  
 [Agregados definidos por el usuario de CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)  
  
  
