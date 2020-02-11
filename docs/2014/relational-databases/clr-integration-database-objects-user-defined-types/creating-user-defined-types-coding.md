---
title: 编写用户定义类型的代码 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 7427de92691a2d5c0a92aac55ac16f47dd2ef6b1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "75232239"
---
# <a name="coding-user-defined-types"></a>用户定义类型编码
  编写用户定义类型 (UDT) 的定义时，必须根据是要将 UDT 作为类还是作为结构实现以及您所选择的格式和序列化选项来实现各种功能。  
  
 本节中的示例说明了如何将 `Point` UDT 作为 `struct`（在 Visual Basic 中为 `Structure`）实现。 
  `Point` UDT 由作为属性过程实现的 X 和 Y 坐标组成。  
  
 定义 UDT 时需要下列命名空间：  
  
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
  
 
  `Microsoft.SqlServer.Server` 命名空间包含 UDT 的各种属性所需的对象，`System.Data.SqlTypes` 命名空间包含表示程序集可用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机数据类型的类。 当然，还可能存在程序集正常运行所需的其他命名空间。 
  `Point` UDT 还使用 `System.Text` 命名空间来处理字符串。  
  
> [!NOTE]  
>  不再支持执行使用 `/clr:pure` 编译的 Visual C++ 数据库对象（例如 UDT）。  
  
## <a name="specifying-attributes"></a>指定属性  
 属性确定如何使用序列化来构造 UDT 的存储表示形式以及如何按值将 UDT 传输到客户端。  
  
 
  `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 是必需的。 
  `Serializable` 属性是可选的。 您也可以指定 `Microsoft.SqlServer.Server.SqlFacetAttribute` 以提供有关 UDT 的返回类型的信息。 有关详细信息，请参阅 [CLR 例程的自定义属性](../clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)。  
  
### <a name="point-udt-attributes"></a>Point UDT 属性  
 
  `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 将 `Point` UDT 的存储格式设置为 `Native`。 
  `IsByteOrdered` 设置为 `true`，这样可以保证在 SQL Server 中的比较结果相同，就像在托管代码中进行相同的比较一样。 UDT 实现 `System.Data.SqlTypes.INullable` 接口以使 UDT 能够识别 Null 值。  
  
 下面的代码段显示了 `Point` UDT 的属性。  
  
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
  
## <a name="implementing-nullability"></a>实现为 Null 性  
 除了为您的程序集正确指定属性外，UDT 还必须支持为 Null 性。 加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 UDT 是能够识别 Null 的，但为使 UDT 识别 Null 值，UDT 必须实现 `System.Data.SqlTypes.INullable` 接口。  
  
 您必须创建一个名为 `IsNull` 的属性，需要该属性才能从 CLR 代码中确定一个值是否为 Null。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发现 UDT 的 Null 实例时，会使用正常的 Null 处理方法来保留 UDT。 如果服务器不必序列化或反序列化 UDT，它不会在这些方面浪费时间；此外，它也不会浪费空间来存储 Null UDT。 每次从 CLR 中引入 UDT 时都会执行这种 Null 检查，也就是说，始终都应可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 构造来检查有无 Null UDT。 服务器也使用 `IsNull` 属性来测试实例是否为 Null。 一旦服务器确定 UDT 为 Null，它便可以使用其本机 Null 处理方法。  
  
 
  `get()` 的 `IsNull` 方法绝非特殊。 如果 `Point` 变量 `@p` 为 `Null`，则默认情况下 `@p.IsNull` 的计算结果将为“NULL”而不是“1”。 这是因为 `SqlMethod(OnNullCall)` 方法的 `IsNull get()` 属性默认为 False。 因为对象为 `Null`，因此请求属性时，不会反序列化该对象，不会调用该方法，而且会返回默认值“NULL”。  
  
### <a name="example"></a>示例  
 在下面的示例中，`is_Null` 变量是私有的并且保存了 UDT 实例的 Null 状态。 您的代码必须保留 `is_Null` 的相应值。 UDT 还必须具有一个名为 `Null` 的静态属性，该属性返回 UDT 的 Null 值实例。 这样，如果该实例在数据库中确实为 Null，UDT 便可返回 Null 值。  
  
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
  
### <a name="is-null-vs-isnull"></a>IS NULL 与 IsNull 的比较  
 假定有一个表包含架构 Points(id int, location Point)，其中 `Point` 为 CLR UDT，并且有如下查询：  
  
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
  
 这两个查询都返回具有非 `Null` 位置的点的 ID。 在 Query 1 中，使用的是正常 Null 处理方法，不需要反序列化 UDT。 另一方面，Query 2 必须反序列化每个非 `Null` 对象并调入 CLR 以获取 `IsNull` 属性的值。 显然，使用 `IS NULL` 会产生更高的性能，并且始终都不应从 `IsNull` 代码中读取 UDT 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 属性。  
  
 那么，`IsNull` 属性的用途是什么？ 首先，从 CLR 代码中确定值是否为 `Null` 时需要它。 其次，服务器需要使用一种方法来测试实例是否为 `Null`，因此服务器会使用该属性。 服务器确定该实例为 `Null` 之后，便可以使用其本机 Null 处理方法对该实例进行处理。  
  
## <a name="implementing-the-parse-method"></a>实现 Parse 方法  
 
  `Parse` 和 `ToString` 方法用于转换成 UDT 的字符串表示形式和从 UDT 的字符串表示形式进行转换。 
  `Parse` 方法允许字符串转换为 UDT。 它必须声明为 `static`（在 Visual Basic 中则为 `Shared`），并且采用 `System.Data.SqlTypes.SqlString` 类型的参数。  
  
 下面的代码实现了 `Parse` UDT 的 `Point` 方法，该方法将 X 坐标和 Y 坐标分隔开。 
  `Parse` 具有一个 `System.Data.SqlTypes.SqlString` 类型的参数，并假定以逗号分隔字符串的形式提供 X 和 Y 值。 将 `Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall` 属性设置为 `false` 可防止从 Point 的 Null 实例中调用 `Parse` 方法。  
  
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
  
## <a name="implementing-the-tostring-method"></a>实现 ToString 方法  
 
  `ToString` 方法用于将 `Point` UDT 转换为字符串值。 在此情况下，对于 `Point` 类型的 Null 实例，将返回字符串“NULL”。 
  `ToString` 方法执行的操作与 `Parse` 方法相反，它使用 `System.Text.StringBuilder` 返回由 X 和 Y 坐标值组成的逗号分隔 `System.String`。 由于**InvokeIfReceiverIsNull**默认为 false，因此不需要检查的 null 实例`Point` 。  
  
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
  
## <a name="exposing-udt-properties"></a>公开 UDT 属性  
 
  `Point` UDT 公开了作为 `System.Int32` 类型的公共读写属性实现的 X 和 Y 坐标。  
  
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
  
## <a name="validating-udt-values"></a>验证 UDT 值  
 处理 UDT 数据时，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]会自动将二进制值转换为 UDT 值。 该转换过程包括检查值是否符合类型的序列化格式和确保可以正确地反序列化值。 这样就确保了值可以转换回二进制形式。 对于采用字节顺序的 UDT，这样还可以确保产生的二进制值与原始二进制值匹配。 这会防止在数据库中保留无效值。 在某些情况下，只进行这种级别的检查可能是不够的。 当要求 UDT 值在预期的域或范围之内时可能需要进行其他验证。 例如，实现日期的 UDT 可能要求日值为特定的有效值范围内的正数。  
  
 
  `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.ValidationMethodName` 的 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 属性可用于提供在将数据分配给 UDT 或转换为 UDT 时服务器运行的验证方法的名称。 运行 bcp 实用工具、BULK INSERT、DBCC CHECKDB、DBCC CHECKFILEGROUP、DBCC CHECKTABLE、分布式查询和表格格式数据流 (TDS) 远程过程调用 (RPC) 操作期间也会调用 `ValidationMethodName`。 
  `ValidationMethodName` 的默认值为 Null，表示没有验证方法。  
  
### <a name="example"></a>示例  
 下面的代码段显示了 `Point` 类的声明，该声明指定了 `ValidationMethodName` 的 `ValidatePoint`。  
  
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
  
 如果指定了验证方法，则必须具有如下面的代码段所示的签名。  
  
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
  
 验证方法可具有任意作用域，如果值有效，它应返回 `true`，否则应返回 `false`。 如果此方法返回 `false` 或引发异常，则该值将被视为无效并且会出现错误。  
  
 在下面的示例中，代码仅允许零值或大于 X 和 Y 坐标的值。  
  
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
  
### <a name="validation-method-limitations"></a>验证方法限制  
 服务器是在执行转换时调用验证方法，而不是在通过设置个别属性插入数据时或在使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 语句插入数据时调用验证方法。  
  
 如果希望在所有情况下都执行验证方法，则`Parse`必须从属性 setter 和方法中显式调用验证方法。 并不要求这样做，在某些情况下可能甚至不需要这样做。  
  
### <a name="parse-validation-example"></a>Parse 验证示例  
 若要确保在`ValidatePoint` `Point`类中调用方法，必须从`Parse`方法和设置 X 和 Y 坐标值的属性过程中调用它。 下面的代码段演示如何从`ValidatePoint` `Parse`函数调用验证方法。  
  
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
  
### <a name="property-validation-example"></a>属性验证示例  
 下面的代码段演示如何从设置 X `ValidatePoint`和 Y 坐标的属性过程调用验证方法。  
  
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
  
## <a name="coding-udt-methods"></a>UDT 方法编码  
 编写 UDT 方法时，请考虑所用的算法是否可能会随时间的推移而改变。 如果可能改变的话，最好考虑为您的 UDT 所用的方法创建一个单独的类。 如果算法发生变化，则可以使用新代码重新编译该类并将程序集加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，而不会影响 UDT。 在许多情况下，都可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 语句重新加载 UDT，但这可能会使现有数据出现问题。 例如，AdventureWorks 示例`Currency`数据库中包含的**** UDT 使用**ConvertCurrency**函数转换货币值，该函数在单独的类中实现。 在未来，转换算法可能会发生不可预知的变化，或者可能需要新的功能。 在规划**** 将来的更改时`Currency` ，将 ConvertCurrency 函数与 UDT 实现分离可提供更大的灵活性。  
  
### <a name="example"></a>示例  
 `Point`类包含三种用于计算距离的简单方法：**距离**、 **DistanceFrom**和**DistanceFromXY**。 每个方法均返回一个 `double`，分别计算的是从 `Point` 到零的距离，从指定点到 `Point` 的距离，以及从指定的 X 和 Y 坐标到 `Point` 的距离。 每个调用**DistanceFromXY**的**距离**和**DistanceFrom** ，并演示如何对每个方法使用不同的参数。  
  
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
  
### <a name="using-sqlmethod-attributes"></a>使用 SqlMethod 属性  
 
  `Microsoft.SqlServer.Server.SqlMethodAttribute` 类提供了一些自定义属性，这些属性可用于标记方法定义以便指定 Null 调用行为的确定性以及指定方法是否为赋值函数。 使用的是这些属性的默认值，仅在需要非默认值时才使用自定义特性。  
  
> [!NOTE]  
>  
  `SqlMethodAttribute` 类继承自 `SqlFunctionAttribute` 类，因此 `SqlMethodAttribute` 继承了 `FillRowMethodName` 中的 `TableDefinition` 和 `SqlFunctionAttribute` 字段。 这意味着可以编写一个不属于此情况的表值方法。 方法将编译并部署程序集，但在运行时将`IEnumerable`引发有关返回类型的错误，并返回以下消息： "程序\<\<\<集>" 的类 "class>" 中的 "方法、属性或字段 ' 名称> ' 具有无效的返回类型。"  
  
 下表说明了可以在 UDT 方法中使用的部分相关 `Microsoft.SqlServer.Server.SqlMethodAttribute` 属性，并列出了其默认值。  
  
 DataAccess  
 指示函数是否需要访问存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地实例中的用户数据。 默认值为 `DataAccessKind`.`None`。  
  
 IsDeterministic  
 指示在输入值相同且数据库状态相同的情况下函数是否会生成相同的输出值。 默认为 `false`。  
  
 IsMutator  
 指示方法是否在 UDT 实例中引起状态变化。 默认为 `false`。  
  
 IsPrecise  
 指示函数是否涉及不精确的计算，如浮点运算。 默认为 `false`。  
  
 OnNullCall  
 指示在指定 Null 引用输入参数时是否调用此方法。 默认为 `true`。  
  
### <a name="example"></a>示例  
 使用 `Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator` 属性可以标记允许 UDT 实例状态改变的方法。 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 不允许在一个 UPDATE 语句的 SET 子句中设置两个 UDT 属性。 然而，您可以将一个方法标记为更改两个成员的赋值函数。  
  
> [!NOTE]  
>  在查询中不允许使用赋值函数方法。 这些方法只能在赋值语句或数据修改语句中调用。 如果标记为赋值函数的方法不返回 `void`（在 Visual Basic 中则是不为 `Sub`），则 CREATE TYPE 将失败并出错。  
  
 下面的语句假定存在一个具有 `Triangles` 方法的 `Rotate` UDT。 下面的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 更新语句调用该 `Rotate` 方法：  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 
  `Rotate` 方法是使用将 `SqlMethod` 设置为 `IsMutator` 的 `true` 属性来修饰的，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以将该方法标记为赋值函数方法。 该代码还将 `OnNullCall` 设置为 `false`，这将向服务器指示，如果任何输入参数为 Null 引用，该方法将返回 Null 引用（在 Visual Basic 中为 `Nothing`）。  
  
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
  
## <a name="implementing-a-udt-with-a-user-defined-format"></a>采用用户定义的格式实现 UDT  
 采用用户定义的格式实现 UDT 时，必须实现 `Read` 和 `Write` 方法，这两个方法实现了 Microsoft.SqlServer.Server.IBinarySerialize 接口以处理 UDT 数据的序列化和反序列化。 还必须指定 `MaxByteSize` 的 `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` 属性。  
  
### <a name="the-currency-udt"></a>Currency UDT  
 从 `Currency` 开始，随 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装的 CLR 示例附带了 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] UDT。  
  
 
  `Currency` UDT 支持采用特定区域性的货币体系来处理货币金额。 您必须定义两个字段：一个表示 `string` 的 `CultureInfo`，用于指定货币的发行者（例如 en-us）；一个表示 `decimal` 的 `CurrencyValue`，即货币金额。  
  
 尽管服务器并不使用它来执行比较，但 `Currency` UDT 实现了 `System.IComparable` 接口，该接口公开了一个方法 `System.IComparable.CompareTo`。 在需要精确比较或排序区域性中的货币值的情况下，在客户端会使用此方法。  
  
 在 CLR 中运行的代码将区域性与货币值分开比较。 对于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码，通过执行下列操作来确定如何比较：  
  
1.  将 `IsByteOrdered` 属性设置为 True，它指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用磁盘上的持久化二进制表示形式进行比较。  
  
2.  使用 `Write` UDT 的 `Currency` 方法确定 UDT 在磁盘上的保留方式，从而确定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 运算如何比较和排序 UDT 值。  
  
3.  采用以下二进制格式保存 `Currency` UDT：  
  
    1.  将区域性另存为 UTF-16 编码的字符串并用第 0-19 个字节表示，右侧以 Null 字符填充。  
  
    2.  使用第 20 个字节及以后的字节包含货币的十进制值。  
  
 填充的目的是为了确保区域性与货币值完全分开，以便在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码中将一个 UDT 与另一个 UDT 进行比较时，区域性字节与区域性字节相比较，货币字节值与货币字节值相比较。  
  
 有关`Currency` UDT 的完整代码列表，请按照[SQL Server 数据库引擎示例](https://msftengprodsamples.codeplex.com/)中有关安装 CLR 示例的说明进行操作。  
  
### <a name="currency-attributes"></a>Currency 属性  
 
  `Currency` UDT 定义有以下属性。  
  
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
  
## <a name="creating-read-and-write-methods-with-ibinaryserialize"></a>创建带有 IBinarySerialize 的 Read 和 Write 方法  
 当您选择 `UserDefined` 序列化格式时，还必须实现 `IBinarySerialize` 接口并创建您自己的 `Read` 和 `Write` 方法。 
  `Currency` UDT 中的下列过程使用 `System.IO.BinaryReader` 和 `System.IO.BinaryWriter` 来从 UDT 中读取数据和向其中写入数据。  
  
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
  
 有关`Currency` UDT 的完整代码列表，请参阅[SQL Server 数据库引擎示例](https://msftengprodsamples.codeplex.com/)。  
  
## <a name="see-also"></a>另请参阅  
 [Creating a User-Defined Type（创建用户定义类型）](creating-user-defined-types.md)  
  
