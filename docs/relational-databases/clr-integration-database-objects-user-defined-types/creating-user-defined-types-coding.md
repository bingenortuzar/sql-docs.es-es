---
title: Codificar tipos definidos por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- validation [CLR integration]
- UDTs [CLR integration], coding
- UserDefined serialization format [CLR integration]
- Point UDT
- Parse method
- null values [CLR integration]
- ToString method
- ValidatePoint method
- attributes [CLR integration]
- coding user-defined types [CLR integration]
- Read method
- Write method
- nullability [CLR integration]
- user-defined types [CLR integration], coding
- Currency UDT
- validating UDT values
- exposing UDT properties [CLR integration]
ms.assetid: 1e5b43b3-4971-45ee-a591-3f535e2ac722
author: rothja
ms.author: jroth
ms.openlocfilehash: e94662043d3801cc7088533d7f0fbadd638bec5b
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874814"
---
# <a name="creating-user-defined-types---coding"></a>Crear tipos definidos por el usuario: codificación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Al codificar la definición de un tipo definido por el usuario (UDT), debe implementar varias características, en función de si implementa el UDT como una clase o como una estructura, así como de las opciones de formato y serialización que haya elegido.  
  
 En el ejemplo de esta sección se muestra cómo implementar un UDT de **punto** como **struct** (o **estructura** en Visual Basic). El UDT **Point** se compone de las coordenadas X e y implementadas como procedimientos de propiedad.  
  
 Para definir un UDT, se requieren los espacios de nombres siguientes:  
  
```vb  
Imports System  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
```  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
```  
  
 El espacio de nombres **Microsoft. SqlServer. Server** contiene los objetos necesarios para varios atributos del UDT y el espacio de nombres **System. Data. SqlTypes** contiene las clases [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que representan los tipos de datos nativos disponibles para el assembl. Es obvio que puede haber espacios de nombres adicionales que el ensamblado necesite para funcionar correctamente. El UDT **Point** también usa el espacio de nombres **System. Text** para trabajar con cadenas.  
  
> [!NOTE]  
>  No C++ se admite la ejecución de objetos de base de datos visual, como UDT, compilados con **/clr: Pure** .  
  
## <a name="specifying-attributes"></a>Especificar atributos  
 Los atributos determinan el modo de usar la serialización para construir la representación de almacenamiento de los UDT y para transmitirlos por valor al cliente.  
  
 Se requiere **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** . El atributo **serializable** es opcional. También puede especificar **Microsoft. SqlServer. Server. SqlFacetAttribute** para proporcionar información sobre el tipo de valor devuelto de un UDT. Para obtener más información, vea [Atributos personalizados para las rutinas CLR](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md).  
  
### <a name="point-udt-attributes"></a>Atributos del UDT Point  
 **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** establece el formato de almacenamiento para el UDT **Point** en **Native**. **IsByteOrdered** se establece en **true**, lo que garantiza que los resultados de las comparaciones son los mismos en SQL Server como si hubiera tenido lugar la misma comparación en código administrado. El UDT implementa la interfaz **System. Data. SqlTypes. INullable** para que el UDT sea compatible con NULL.  
  
 En el siguiente fragmento de código se muestran los atributos del UDT **Point** .  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True)> _  
  Public Structure Point  
    Implements INullable  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true)]  
public struct Point : INullable  
{  
```  
  
## <a name="implementing-nullability"></a>Implementar la nulabilidad  
 Además de especificar correctamente los atributos de los ensamblados, el UDT también debe admitir la nulabilidad. Los UDT cargados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen reconocimiento nulo, pero para que el UDT reconozca un valor null, el UDT debe implementar la interfaz **System. Data. SqlTypes. INullable** .  
  
 Debe crear una propiedad denominada **IsNull**, que es necesaria para determinar si un valor es null dentro del código CLR. Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encuentra una instancia NULL de un UDT, el UDT se conserva mediante los métodos habituales de control de valores NULL. El servidor no pierde tiempo serializando o deserializando el UDT sin necesidad y no desaprovecha espacio para almacenar un UDT NULL. Esta comprobación de valores NULL se realiza cada vez que se usa un UDT de CLR, lo que significa que el uso de la construcción IS NULL de [!INCLUDE[tsql](../../includes/tsql-md.md)] para comprobar los UDT que son NULL debería funcionar siempre. La propiedad **IsNull** también la usa el servidor para probar si una instancia es NULL. Una vez que el servidor determina que el UDT es NULL, puede usar su propio control de valores NULL nativos.  
  
 El método **get ()** de **IsNull** no tiene ninguna grafía especial. Si una variable  **\@** de **punto**  **pesnull,p.IsNullseevaluará,deformapredeterminada,como"null",nocomo"1".\@** Esto se debe a que el atributo **SqlMethod (OnNullCall)** del método **IsNull get ()** tiene como valor predeterminado False. Dado que el objeto es **null**, cuando se solicita la propiedad, el objeto no se deserializa, no se llama al método y se devuelve un valor predeterminado de "null".  
  
### <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, la variable `is_Null` es privada y contiene el estado NULL para la instancia del UDT. El código debe mantener un valor adecuado para `is_Null`. El UDT también debe tener una propiedad estática denominada **null** que devuelva una instancia de valor null del UDT. Esto permite al UDT devolver un valor NULL si la instancia también es NULL en la base de datos.  
  
```vb  
Private is_Null As Boolean  
  
Public ReadOnly Property IsNull() As Boolean _  
   Implements INullable.IsNull  
    Get  
        Return (is_Null)  
    End Get  
End Property  
  
Public Shared ReadOnly Property Null() As Point  
    Get  
        Dim pt As New Point  
        pt.is_Null = True  
        Return (pt)  
    End Get  
End Property  
```  
  
```csharp  
private bool is_Null;  
  
public bool IsNull  
{  
    get  
    {  
        return (is_Null);  
    }  
}  
  
public static Point Null  
{  
    get  
    {  
        Point pt = new Point();  
        pt.is_Null = true;  
        return pt;  
    }  
}  
```  
  
### <a name="is-null-vs-isnull"></a>ES NULL frente a IsNull  
 Considere una tabla que contiene los puntos de esquema (identificador int, punto de ubicación), donde **Point** es un UDT de CLR y las siguientes consultas:  
  
```  
--Query 1  
SELECT ID  
FROM Points  
WHERE NOT (location IS NULL) -- Or, WHERE location IS NOT NULL;  
```  
  
```  
--Query 2:  
SELECT ID  
FROM Points  
WHERE location.IsNull = 0;  
```  
  
 Ambas consultas devuelven los identificadores de puntos con ubicaciones no**nulas** . En la consulta 1 (Query 1), se usa el control habitual de valores NULL y no se requiere ninguna deserialización de UDT. La consulta 2, por otro lado, tiene que deserializar cada objeto distinto de**null** y llamar a CLR para obtener el valor de la propiedad **IsNull** . Claramente, el uso de **is null** mostrará un mejor rendimiento y nunca debería haber una razón para leer la propiedad **IsNull** de un UDT [!INCLUDE[tsql](../../includes/tsql-md.md)] desde el código.  
  
 Por lo tanto, ¿qué es el uso de la propiedad **IsNull** ? En primer lugar, es necesario determinar si un valor es **null** desde el código CLR. En segundo lugar, el servidor necesita una manera de probar si una instancia es **null**, por lo que el servidor usa esta propiedad. Una vez que determina que es **null**, puede utilizar su control de valores NULL nativos para controlarlo.  
  
## <a name="implementing-the-parse-method"></a>Implementar el método Parse  
 Los métodos **Parse** y **ToString** permiten conversiones a y desde representaciones de cadena del UDT. El método **Parse** permite convertir una cadena en un UDT. Debe declararse como **static** (o **compartirse** en Visual Basic) y tomar un parámetro de tipo **System. Data. SqlTypes. SqlString**.  
  
 El código siguiente implementa el método **Parse** para el UDT **Point** , que separa las coordenadas X e y. El método **Parse** tiene un único argumento de tipo **System. Data. SqlTypes. SqlString**y da por supuesto que los valores X e y se proporcionan como una cadena delimitada por comas. Si se establece el atributo **Microsoft. SqlServer. Server. SqlMethodAttribute. OnNullCall** en **false** , se evita que se llame al método **Parse** desde una instancia null de Point.  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
    return pt;  
}  
```  
  
## <a name="implementing-the-tostring-method"></a>Implementar el método ToString  
 El método **ToString** convierte el UDT **Point** en un valor de cadena. En este caso, se devuelve la cadena "NULL" para una instancia NULL del tipo **Point** . El método **ToString** invierte el método **Parse** con **System. Text. StringBuilder** para devolver una **cadena System. String** separada por comas que consta de los valores de las coordenadas X e y. Dado que **InvokeIfReceiverIsNull** tiene como valor predeterminado False, no es necesario comprobar si hay una instancia nula de **Point** .  
  
```vb  
Private _x As Int32  
Private _y As Int32  
  
Public Overrides Function ToString() As String  
    If Me.IsNull Then  
        Return "NULL"  
    Else  
        Dim builder As StringBuilder = New StringBuilder  
        builder.Append(_x)  
        builder.Append(",")  
        builder.Append(_y)  
        Return builder.ToString  
    End If  
End Function  
```  
  
```csharp  
private Int32 _x;  
private Int32 _y;  
  
public override string ToString()  
{  
    if (this.IsNull)  
        return "NULL";  
    else  
    {  
        StringBuilder builder = new StringBuilder();  
        builder.Append(_x);  
        builder.Append(",");  
        builder.Append(_y);  
        return builder.ToString();  
    }  
}  
```  
  
## <a name="exposing-udt-properties"></a>Exponer las propiedades del UDT  
 El UDT **Point** expone las coordenadas X e y que se implementan como propiedades de lectura y escritura públicas del tipo **System. Int32**.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _x = Value  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _y = Value  
    End Set  
End Property  
```  
  
```csharp  
public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    set   
    {  
        _x = value;  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        _y = value;  
    }  
}  
```  
  
## <a name="validating-udt-values"></a>Validar los valores UDT  
 Al trabajar con datos UDT, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] convierte automáticamente los valores binarios en valores UDT. Este proceso de conversión implica la comprobación de que los valores son adecuados para el formato de serialización del tipo, así como asegurarse de que el valor puede deserializarse correctamente. Esto garantiza que el valor se pueda volver a convertir al formato binario. En el caso de los UDT ordenados por bytes, esto también garantiza que el valor binario resultante coincida con el valor binario original. De esta forma, se evita que los valores que no son válidos se conserven en la base de datos. En algunos casos, este nivel de comprobación puede resultar inadecuado. Puede ser necesaria una validación adicional cuando se exige que los valores UDT se encuentren en un dominio o intervalo esperado. Por ejemplo, un UDT que implementa una fecha podría exigir que el valor de día sea un número positivo que pertenezca a un intervalo determinado de valores válidos.  
  
 La propiedad **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute. ValidationMethodName** de **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** permite proporcionar el nombre de un método de validación que ejecuta el servidor. Cuando los datos se asignan a un UDT o se convierten en un UDT. También se llama a **ValidationMethodName** durante la ejecución de la utilidad bcp, Bulk Insert, DBCC CHECKDB, DBCC CHECKFILEGROUP, DBCC CHECKTABLE, consulta distribuida y operaciones de llamada a procedimiento remoto (RPC) del flujo TDS. El valor predeterminado de **ValidationMethodName** es null, lo que indica que no hay ningún método de validación.  
  
### <a name="example"></a>Ejemplo  
 En el fragmento de código siguiente se muestra la declaración de la clase **Point** , que especifica un **ValidationMethodName** de **ValidatePoint**.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True, _  
  ValidationMethodName:="ValidatePoint")> _  
  Public Structure Point  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true,   
  ValidationMethodName = "ValidatePoint")]  
public struct Point : INullable  
{  
```  
  
 Si se especifica un método de validación, debe tener una firma de aspecto similar al fragmento de código siguiente.  
  
```vb  
Private Function ValidationFunction() As Boolean  
    If (validation logic here) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidationFunction()  
{  
    if (validation logic here)  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
 El método de validación puede tener cualquier ámbito y debe devolver **true** si el valor es válido y **false** en caso contrario. Si el método devuelve **false** o inicia una excepción, el valor se trata como no válido y se produce un error.  
  
 En el ejemplo siguiente, el código solamente permite valores iguales a cero o mayores que las coordenadas X e Y.  
  
```vb  
Private Function ValidatePoint() As Boolean  
    If (_x >= 0) And (_y >= 0) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidatePoint()  
{  
    if ((_x >= 0) && (_y >= 0))  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
### <a name="validation-method-limitations"></a>Limitaciones del método de validación  
 El servidor llama al método de validación cuando está realizando conversiones, no cuando los datos se insertan mediante el establecimiento de propiedades individuales ni cuando los datos se insertan mediante una instrucción INSERT de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Debe llamar explícitamente al método de validación desde establecedores de propiedades y el método **Parse** si desea que el método de validación se ejecute en todas las situaciones. No se trata de ningún requisito e incluso, en algunos casos, es posible que no se desee.  
  
### <a name="parse-validation-example"></a>Ejemplo de validación de Parse  
 Para asegurarse de que se invoca el método **ValidatePoint** en la clase **Point** , debe llamarlo desde el método **Parse** y desde los procedimientos de propiedad que establecen los valores de las coordenadas X e y. En el fragmento de código siguiente se muestra cómo llamar al método de validación **ValidatePoint** desde la función **Parse** .  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
  
    ' Call ValidatePoint to enforce validation  
    ' for string conversions.  
    If Not pt.ValidatePoint() Then  
        Throw New ArgumentException("Invalid XY coordinate values.")  
    End If  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
  
    // Call ValidatePoint to enforce validation  
    // for string conversions.  
    if (!pt.ValidatePoint())   
        throw new ArgumentException("Invalid XY coordinate values.");  
    return pt;  
}  
```  
  
### <a name="property-validation-example"></a>Ejemplo de validación de propiedad  
 En el fragmento de código siguiente se muestra cómo llamar al método de validación **ValidatePoint** desde los procedimientos de propiedad que establecen las coordenadas X e y.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _x  
        _x = Value  
        If Not ValidatePoint() Then  
            _x = temp  
            Throw New ArgumentException("Invalid X coordinate value.")  
        End If  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _y  
        _y = Value  
        If Not ValidatePoint() Then  
            _y = temp  
            Throw New ArgumentException("Invalid Y coordinate value.")  
        End If  
    End Set  
End Property  
```  
  
```csharp  
    public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    // Call ValidatePoint to ensure valid range of Point values.  
    set   
    {  
        Int32 temp = _x;  
        _x = value;  
        if (!ValidatePoint())  
        {  
            _x = temp;  
            throw new ArgumentException("Invalid X coordinate value.");  
        }  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        Int32 temp = _y;  
        _y = value;  
        if (!ValidatePoint())  
        {  
            _y = temp;  
            throw new ArgumentException("Invalid Y coordinate value.");  
        }  
    }  
}  
```  
  
## <a name="coding-udt-methods"></a>Codificar métodos UDT  
 Cuando codifique los métodos UDT, tenga en cuenta si el algoritmo usado podría cambiar con el tiempo. En ese caso, es posible que desee considerar la posibilidad de crear una clase independiente para los métodos que usa el UDT. Si el algoritmo cambia, puede volver a compilar la clase con el nuevo código, así como cargar el ensamblado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin que esto afecte al UDT. En muchos casos, los UDT pueden volver a cargarse mediante la instrucción ALTER ASSEMBLY de [!INCLUDE[tsql](../../includes/tsql-md.md)], pero eso podría causar problemas con los datos existentes. Por ejemplo, el UDT **Currency** que se incluye con la base de datos de ejemplo **AdventureWorks** usa una función **ConvertCurrency** para convertir los valores de moneda, que se implementa en una clase independiente. Es posible que en un futuro los algoritmos de conversión cambien de modo impredecible o que se necesite nueva funcionalidad. Separar la función **ConvertCurrency** de la implementación UDT de **moneda** proporciona mayor flexibilidad a la hora de planear cambios futuros.  
  
### <a name="example"></a>Ejemplo  
 La clase **Point** contiene tres métodos simples para calcular la distancia: **Distance**, **DistanceFrom** y **DistanceFromXY**. Cada devuelve un **valor Double** que calcula la distancia de **punto** a cero, la distancia de un punto a **punto**especificado y la distancia desde las coordenadas X e y especificadas hasta el **punto**. **Distance** y **DistanceFrom** llaman a **DistanceFromXY**y muestran cómo usar argumentos diferentes para cada método.  
  
```vb  
' Distance from 0 to Point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function Distance() As Double  
    Return DistanceFromXY(0, 0)  
End Function  
  
' Distance from Point to the specified point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFrom(ByVal pFrom As Point) As Double  
    Return DistanceFromXY(pFrom.X, pFrom.Y)  
End Function  
  
' Distance from Point to the specified x and y values.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFromXY(ByVal ix As Int32, ByVal iy As Int32) _  
    As Double  
    Return Math.Sqrt(Math.Pow(ix - _x, 2.0) + Math.Pow(iy - _y, 2.0))  
End Function  
```  
  
```csharp  
// Distance from 0 to Point.  
[SqlMethod(OnNullCall = false)]  
public Double Distance()  
{  
    return DistanceFromXY(0, 0);  
}  
  
// Distance from Point to the specified point.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFrom(Point pFrom)  
{  
    return DistanceFromXY(pFrom.X, pFrom.Y);  
}  
  
// Distance from Point to the specified x and y values.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFromXY(Int32 iX, Int32 iY)  
{  
    return Math.Sqrt(Math.Pow(iX - _x, 2.0) + Math.Pow(iY - _y, 2.0));  
}  
```  
  
### <a name="using-sqlmethod-attributes"></a>Usar atributos SqlMethod  
 La clase **Microsoft. SqlServer. Server. SqlMethodAttribute** proporciona atributos personalizados que se pueden usar para marcar las definiciones de método con el fin de especificar el determinismo, el comportamiento de la llamada NULL y especificar si un método es un mutador. Se asume el uso de valores predeterminados para estas propiedades y solamente se usa el atributo personalizado cuando se necesita un valor no predeterminado.  
  
> [!NOTE]  
>  La clase **SqlMethodAttribute** hereda de la clase **SqlFunctionAttribute** , por lo que **SqlMethodAttribute** hereda los campos **FillRowMethodName** y **TableDefinition** de **SqlFunctionAttribute**. Esto significa que es posible escribir un método con valores de tabla, que no es el caso. El método compila y el ensamblado implementa, pero se genera un error sobre el tipo de valor devuelto **IEnumerable** en tiempo de ejecución con el siguiente mensaje: "El método, propiedad o campo '\<nombre > ' de la clase\<' clase > ' en el\<ensamblado ' ensamblado > ' tiene un tipo de valor devuelto no válido."  
  
 En la tabla siguiente se describen algunas de las propiedades de **Microsoft. SqlServer. Server. SqlMethodAttribute** relevantes que se pueden usar en los métodos UDT y se enumeran sus valores predeterminados.  
  
 DataAccess  
 Indica si la función implica el acceso a los datos de usuario almacenados en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El valor predeterminado es **DataAccessKind**. **Ninguno**.  
  
 IsDeterministic  
 Indica si la función genera los mismos valores de salida si se especifican los mismos valores de entrada y el mismo estado de la base de datos. El valor predeterminado es **false**.  
  
 IsMutator  
 Indica si el método produce un cambio de estado en la instancia del UDT. El valor predeterminado es **false**.  
  
 IsPrecise  
 Indica si la función implica cálculos imprecisos, como operaciones de punto flotante. El valor predeterminado es **false**.  
  
 OnNullCall  
 Indica si se llama al método cuando se especifican argumentos de entrada de referencia NULL. El valor predeterminado es **true**.  
  
### <a name="example"></a>Ejemplo  
 La propiedad **Microsoft. SqlServer. Server. SqlMethodAttribute. IsMutator** permite marcar un método que permite un cambio en el estado de una instancia de un UDT. [!INCLUDE[tsql](../../includes/tsql-md.md)] no permite que el usuario establezca dos propiedades UDT en la cláusula SET de una instrucción UPDATE. Sin embargo, puede tener un método marcado como mutador que cambie los dos miembros.  
  
> [!NOTE]  
>  No se permite el uso de métodos mutadores en las consultas. Solo puede llamarse a estos métodos en instrucciones de asignación o en instrucciones de modificación de datos. Si un método marcado como mutador no devuelve **void** (o no es **Sub** en Visual Basic), Create Type produce un error.  
  
 La siguiente instrucción supone la existencia de un UDT de **triángulos** que tiene un método **Rotate** . La siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción UPDATE invoca el método **Rotate** :  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 El **método rotate** se decora con el atributo SqlMethod **IsMutator** en **true** para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda marcar el método como un método mutador. El código también establece **OnNullCall** en **false**, que indica al servidor que el método devuelve una referencia nula (**Nothing** en Visual Basic) si alguno de los parámetros de entrada es una referencia nula.  
  
```vb  
<SqlMethod(IsMutator:=True, OnNullCall:=False)> _  
Public Sub Rotate(ByVal anglex as Double, _  
  ByVal angley as Double, ByVal anglez As Double)   
   RotateX(anglex)  
   RotateY(angley)  
   RotateZ(anglez)  
End Sub  
```  
  
```csharp  
[SqlMethod(IsMutator = true, OnNullCall = false)]  
public void Rotate(double anglex, double angley, double anglez)   
{  
   RotateX(anglex);  
   RotateY(angley);  
   RotateZ(anglez);  
}  
```  
  
## <a name="implementing-a-udt-with-a-user-defined-format"></a>Implementar un UDT con un formato definido por el usuario  
 Al implementar un UDT con un formato definido por el usuario, debe implementar métodos de **lectura** y **escritura** que implementen la interfaz Microsoft. SqlServer. Server. IBinarySerialize para controlar la serialización y deserialización de los datos UDT. También debe especificar la propiedad **MaxByteSize** de **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute**.  
  
### <a name="the-currency-udt"></a>El UDT Currency  
 El UDT **Currency** se incluye con los ejemplos de CLR que se pueden instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]con, a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]partir de.  
  
 El UDT **Currency** permite administrar cantidades de dinero en el sistema monetario de una referencia cultural determinada. Debe definir dos campos: una **cadena** para **CultureInfo**, que especifica quién emitió la moneda (por ejemplo, en-US) y un **decimal** para **CurrencyValue**, la cantidad de dinero.  
  
 Aunque el servidor no lo usa para realizar comparaciones, el UDT de **moneda** implementa la interfaz **System. IComparable** , que expone un método único, **System. IComparable. CompareTo**. Se usa del lado cliente en situaciones en las que se desean realizar comparaciones precisas u ordenar valores de moneda dentro de las referencias culturales.  
  
 El código que se ejecuta en CLR compara por separado la referencia cultural y el valor de moneda. Para el código [!INCLUDE[tsql](../../includes/tsql-md.md)], las acciones siguientes determinan la comparación:  
  
1.  Establezca el atributo **IsByteOrdered** en true, que indica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a que use la representación binaria persistente en el disco para las comparaciones.  
  
2.  Use el método **Write** para el UDT **Currency** para determinar cómo se conserva el UDT en el disco y, por tanto, cómo se comparan [!INCLUDE[tsql](../../includes/tsql-md.md)] y se ordenan los valores de UDT para las operaciones.  
  
3.  Guarde el UDT de **moneda** con el siguiente formato binario:  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    1.  Guarde la referencia cultural como una cadena codificada mediante UTF-16, con bytes del 0 al 19, que se rellena a la derecha con caracteres NULL.  
  
    2.  Use el byte 20 y los bytes siguientes para almacenar el valor decimal de la moneda.  
  
 El propósito del relleno es asegurarse de que la referencia cultural esté completamente separada del valor de moneda, de forma que al comparar un UDT con otro en código [!INCLUDE[tsql](../../includes/tsql-md.md)], los bytes de la referencia cultural se comparen con los bytes de la referencia cultural y los valores de bytes de moneda se comparen con los valores de bytes de moneda.  
  
 Para obtener la lista de código completa del UDT de **moneda** , siga las instrucciones para instalar los ejemplos de CLR en [SQL Server ejemplos de motor de base de datos](https://msftengprodsamples.codeplex.com/).  
  
### <a name="currency-attributes"></a>Atributos de Currency  
 El UDT de **moneda** se define con los siguientes atributos.  
  
```vb  
<Serializable(), Microsoft.SqlServer.Server.SqlUserDefinedType( _  
    Microsoft.SqlServer.Server.Format.UserDefined, _  
    IsByteOrdered:=True, MaxByteSize:=32), _  
    CLSCompliant(False)> _  
Public Structure Currency  
Implements INullable, IComparable, _  
Microsoft.SqlServer.Server.IBinarySerialize  
```  
  
```csharp  
[Serializable]  
[SqlUserDefinedType(Format.UserDefined,   
    IsByteOrdered = true, MaxByteSize = 32)]  
    [CLSCompliant(false)]  
    public struct Currency : INullable, IComparable, IBinarySerialize  
    {  
```  
  
## <a name="creating-read-and-write-methods-with-ibinaryserialize"></a>Crear métodos de lectura y escritura con IBinarySerialize  
 Cuando elige el formato de serialización **UserDefined** , también debe implementar la interfaz **IBinarySerialize** y crear sus propios métodos de **lectura** y **escritura** . Los procedimientos siguientes del UDT **Currency** usan **System. IO. BinaryReader** y **System. IO. BinaryWriter** para leer y escribir en el UDT.  
  
```vb  
' IBinarySerialize methods  
' The binary layout is as follow:  
'    Bytes 0 - 19: Culture name, padded to the right with null  
'    characters, UTF-16 encoded  
'    Bytes 20+: Decimal value of money  
' If the culture name is empty, the currency is null.  
Public Sub Write(ByVal w As System.IO.BinaryWriter) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Write  
    If Me.IsNull Then  
        w.Write(nullMarker)  
        w.Write(System.Convert.ToDecimal(0))  
        Return  
    End If  
  
    If cultureName.Length > cultureNameMaxSize Then  
        Throw New ApplicationException(String.Format(CultureInfo.CurrentUICulture, _  
           "{0} is an invalid culture name for currency as it is too long.", cultureNameMaxSize))  
    End If  
  
    Dim paddedName As String = cultureName.PadRight(cultureNameMaxSize, CChar(vbNullChar))  
  
    For i As Integer = 0 To cultureNameMaxSize - 1  
        w.Write(paddedName(i))  
    Next i  
  
    ' Normalize decimal value to two places  
    currencyVal = Decimal.Floor(currencyVal * 100) / 100  
    w.Write(currencyVal)  
End Sub  
  
Public Sub Read(ByVal r As System.IO.BinaryReader) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Read  
    Dim name As Char() = r.ReadChars(cultureNameMaxSize)  
    Dim stringEnd As Integer = Array.IndexOf(name, CChar(vbNullChar))  
  
    If stringEnd = 0 Then  
        cultureName = Nothing  
        Return  
    End If  
  
    cultureName = New String(name, 0, stringEnd)  
    currencyVal = r.ReadDecimal()  
End Sub  
  
```  
  
```csharp  
// IBinarySerialize methods  
// The binary layout is as follow:  
//    Bytes 0 - 19:Culture name, padded to the right   
//    with null characters, UTF-16 encoded  
//    Bytes 20+:Decimal value of money  
// If the culture name is empty, the currency is null.  
public void Write(System.IO.BinaryWriter w)  
{  
    if (this.IsNull)  
    {  
        w.Write(nullMarker);  
        w.Write((decimal)0);  
        return;  
    }  
  
    if (cultureName.Length > cultureNameMaxSize)  
    {  
        throw new ApplicationException(string.Format(  
            CultureInfo.InvariantCulture,   
            "{0} is an invalid culture name for currency as it is too long.",   
            cultureNameMaxSize));  
    }  
  
    String paddedName = cultureName.PadRight(cultureNameMaxSize, '\0');  
    for (int i = 0; i < cultureNameMaxSize; i++)  
    {  
        w.Write(paddedName[i]);  
    }  
  
    // Normalize decimal value to two places  
    currencyValue = Decimal.Floor(currencyValue * 100) / 100;  
    w.Write(currencyValue);  
}  
public void Read(System.IO.BinaryReader r)  
{  
    char[] name = r.ReadChars(cultureNameMaxSize);  
    int stringEnd = Array.IndexOf(name, '\0');  
  
    if (stringEnd == 0)  
    {  
        cultureName = null;  
        return;  
    }  
  
    cultureName = new String(name, 0, stringEnd);  
    currencyValue = r.ReadDecimal();  
}  
```  
  
 Para obtener la lista de código completa para el UDT de **moneda** , consulte [ejemplos de motor de base de datos de SQL Server](https://msftengprodsamples.codeplex.com/).  
  
## <a name="see-also"></a>Vea también  
 [Crear un tipo definido por el usuario](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
