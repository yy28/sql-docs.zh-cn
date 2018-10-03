---
title: 用户定义类型编码 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a0647d1e0f7dd082b3ce3aab668d8af8d5673efb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47795765"
---
# <a name="creating-user-defined-types---coding"></a>创建用户定义类型 - 编码
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  编写用户定义类型 (UDT) 的定义时，必须根据是要将 UDT 作为类还是作为结构实现以及您所选择的格式和序列化选项来实现各种功能。  
  
 在本部分中的示例说明了实现**点**UDT 作为**结构**(或**结构**在 Visual Basic 中)。 **点**UDT 由 X 和 Y 坐标作为属性过程。  
  
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
  
 **Microsoft.SqlServer.Server**命名空间包含您的 UDT 的各种属性所需的对象和**System.Data.SqlTypes**命名空间包含表示类[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可用于该程序集的本机数据类型。 当然，还可能存在程序集正常运行所需的其他命名空间。 **点**UDT 还使用**System.Text**用于处理字符串的命名空间。  
  
> [!NOTE]  
>  Visual c + + 数据库对象，例如使用编译的 Udt **/clr: pure**不再支持执行。  
  
## <a name="specifying-attributes"></a>指定属性  
 属性确定如何使用序列化来构造 UDT 的存储表示形式以及如何按值将 UDT 传输到客户端。  
  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**是必需的。 **Serializable**属性是可选的。 此外可以指定**Microsoft.SqlServer.Server.SqlFacetAttribute**提供有关 UDT 的返回类型的信息。 有关详细信息，请参阅 [CLR 例程的自定义属性](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)。  
  
### <a name="point-udt-attributes"></a>Point UDT 属性  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**设置的存储格式**点**UDT 到**本机**。 **IsByteOrdered**设置为**true**，这样可以保证的比较结果进行相同 SQL Server 中相同的比较好像在托管代码中执行的位置。 UDT 实现**System.Data.SqlTypes.INullable**接口以使 UDT 为 null 的注意。  
  
 下面的代码段显示了有关的特性**点**UDT。  
  
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
 除了为您的程序集正确指定属性外，UDT 还必须支持为 Null 性。 加载到 Udt[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是可识别 null 的但为了使 UDT 能够识别 null 值，UDT 必须实现**System.Data.SqlTypes.INullable**接口。  
  
 必须创建一个名为属性**IsNull**，需要确定值是否为 null 从 CLR 代码中。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发现 UDT 的 Null 实例时，会使用正常的 Null 处理方法来保留 UDT。 如果服务器不必序列化或反序列化 UDT，它不会在这些方面浪费时间；此外，它也不会浪费空间来存储 Null UDT。 每次从 CLR 中引入 UDT 时都会执行这种 Null 检查，也就是说，始终都应可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 构造来检查有无 Null UDT。 **IsNull**属性还由服务器用来测试实例是否为 null。 一旦服务器确定 UDT 为 Null，它便可以使用其本机 Null 处理方法。  
  
 **Get （)** 方法**IsNull**不以任何方式的特殊情况。 如果**点**变量**@p**是**Null**，然后**@p.IsNull** ，默认情况下，计算结果将为"NULL"，不是"1"。 这是因为**SqlMethod(OnNullCall)** 的属性**IsNull get （)** 方法默认值为 false。 因为对象是**Null**，该对象不反序列化，不调用该方法，并返回默认值为"NULL"请求属性时。  
  
### <a name="example"></a>示例  
 在下面的示例中，`is_Null` 变量是私有的并且保存了 UDT 实例的 Null 状态。 您的代码必须保留 `is_Null` 的相应值。 UDT 还必须具有一个名为的静态属性**Null**返回 UDT 的 null 值实例。 这样，如果该实例在数据库中确实为 Null，UDT 便可返回 Null 值。  
  
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
  
### <a name="is-null-vs-isnull"></a>IS NULL 与IsNull  
 请考虑一个表，其中包含架构 Points (id int，定位点)，该表**点**是 CLR UDT，并且有如下查询：  
  
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
  
 这两个查询返回的点与非的 Id**Null**位置。 在 Query 1 中，使用的是正常 Null 处理方法，不需要反序列化 UDT。 查询 2，但是，必须反序列化每个非**Null**对象并调入 CLR 以获取的值**IsNull**属性。 很明显，使用**IS NULL**会表现出更好的性能，并且应该永远不会有理由继续阅读**IsNull** UDT 来自属性[!INCLUDE[tsql](../../includes/tsql-md.md)]代码。  
  
 那么，什么是使用**IsNull**属性？ 首先，需要它来确定某个值是否**Null**从 CLR 代码中。 其次，服务器需要通过某种方式来测试实例是否为**Null**，因此服务器使用此属性。 它确定后**Null**，则它可以使用其本机 null 处理来对其进行处理。  
  
## <a name="implementing-the-parse-method"></a>实现 Parse 方法  
 **分析**并**ToString**方法允许用户定义的类型的字符串表示形式之间的转换。 **分析**方法允许将字符串转换为 UDT。 它必须声明为**静态**(或**共享**在 Visual Basic 中)，并且采用的类型参数**System.Data.SqlTypes.SqlString**。  
  
 下面的代码实现**分析**方法**点**UDT，分隔开的 X 和 Y 坐标。 **分析**方法具有一个类型的参数**System.Data.SqlTypes.SqlString**，并假定，一个以逗号分隔的字符串形式提供 X 和 Y 值。 设置**Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall**归于**false**阻止**分析**的 null 实例从被调用的方法点。  
  
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
 **ToString**方法将**点**UDT 到一个字符串值。 在这种情况下，字符串"NULL"返回的 Null 实例**点**类型。 **ToString**方法相反**分析**方法通过使用**System.Text.StringBuilder**返回以逗号分隔**System.String**包含的 X 和 Y 坐标值。 因为**InvokeIfReceiverIsNull**默认值为 false，对的 null 实例的检查**点**是不必要的。  
  
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
 **点**UDT 公开作为类型的公共读写属性实现的 X 和 Y 坐标**System.Int32**。  
  
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
 处理 UDT 数据时，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]会自动将二进制值转换为 UDT 值。 该转换过程包括检查值是否符合类型的序列化格式和确保可以正确地反序列化值。 这可确保，值可以转换回二进制形式。 对于采用字节顺序的 UDT，这样还可以确保产生的二进制值与原始二进制值匹配。 这会防止在数据库中保留无效值。 在某些情况下，只进行这种级别的检查可能是不够的。 当要求 UDT 值在预期的域或范围之内时可能需要进行其他验证。 例如，实现日期的 UDT 可能要求日值为特定的有效值范围内的正数。  
  
 **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.ValidationMethodName**的属性**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**可用于提供名称服务器在运行时的验证方法的数据是分配给 UDT 或转换为 UDT。 **ValidationMethodName**运行 bcp 实用工具、 BULK INSERT、 DBCC CHECKDB、 DBCC CHECKFILEGROUP、 DBCC CHECKTABLE、 分布式的查询和表格格式数据流 (TDS) 远程过程调用 (RPC) 操作期间也名为。 默认值为**ValidationMethodName**为空，表示没有验证方法。  
  
### <a name="example"></a>示例  
 下面的代码段演示了用于声明**点**类，该类指定**ValidationMethodName**的**ValidatePoint**。  
  
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
  
 验证方法可以具有任意作用域，应返回 **，则返回 true**如果值有效，并且**false**否则为。 如果该方法返回**false**或引发异常，值被视为引发无效或错误。  
  
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
  
 必须显式从属性 setter 调用验证方法和**分析**方法如果你想要在所有情况下执行的验证方法。 并不要求这样做，在某些情况下可能甚至不需要这样做。  
  
### <a name="parse-validation-example"></a>Parse 验证示例  
 若要确保**ValidatePoint**方法中调用**点**类，则必须调用它从**分析**方法和从设置 X 和 Y 属性过程坐标值。 下面的代码段演示如何调用**ValidatePoint**验证方法，从**分析**函数。  
  
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
 下面的代码段演示如何调用**ValidatePoint**从设置 X 和 Y 坐标的属性过程的验证方法。  
  
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
 编写 UDT 方法时，请考虑所用的算法是否可能会随时间的推移而改变。 如果可能改变的话，最好考虑为您的 UDT 所用的方法创建一个单独的类。 如果算法发生变化，则可以使用新代码重新编译该类并将程序集加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，而不会影响 UDT。 在许多情况下，都可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 语句重新加载 UDT，但这可能会使现有数据出现问题。 例如，**货币**UDT 附带**AdventureWorks**示例数据库使用**ConvertCurrency**函数转换货币值，这实现在单独的类。 在未来，转换算法可能会发生不可预知的变化，或者可能需要新的功能。 分隔**ConvertCurrency**函数从**货币**UDT 实现规划的未来更改时提供更大的灵活性。  
  
### <a name="example"></a>示例  
 **点**类包含三个简单的方法来计算距离：**距离**， **DistanceFrom**并**DistanceFromXY**。 每个返回**双**计算的距离**点**为零，到指定点的距离**点**，并且从指定 X 和 Y 坐标向**点**。 **距离**并**DistanceFrom**每次调用**DistanceFromXY**，并演示如何使用不同的每个方法的参数。  
  
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
 **Microsoft.SqlServer.Server.SqlMethodAttribute**类提供可用于标记方法定义以便指定 null 调用行为的确定性，以及指定的方法是否是赋值函数的自定义属性。 使用的是这些属性的默认值，仅在需要非默认值时才使用自定义特性。  
  
> [!NOTE]  
>  **SqlMethodAttribute**类继承自**SqlFunctionAttribute**类，因此**SqlMethodAttribute**继承**FillRowMethodName**并**TableDefinition**字段从**SqlFunctionAttribute**。 这意味着可以编写一个不属于此情况的表值方法。 方法能够编译并且程序集部署，但出现错误有关**IEnumerable**返回类型是在运行时出现以下消息:"方法、 属性或字段 '\<名称 >' 中类\<类> 中的程序集\<程序集 > 具有无效的返回类型。"  
  
 下表介绍的部分相关**Microsoft.SqlServer.Server.SqlMethodAttribute**属性可在 UDT 方法，并列出其默认值。  
  
 DataAccess  
 指示函数是否需要访问存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地实例中的用户数据。 默认值是**DataAccessKind**。**无**。  
  
 IsDeterministic  
 指示在输入值相同且数据库状态相同的情况下函数是否会生成相同的输出值。 默认值是**false**。  
  
 IsMutator  
 指示方法是否在 UDT 实例中引起状态变化。 默认值是**false**。  
  
 IsPrecise  
 指示函数是否涉及不精确的计算，如浮点运算。 默认值是**false**。  
  
 OnNullCall  
 指示在指定 Null 引用输入参数时是否调用此方法。 默认值是 **，则返回 true**。  
  
### <a name="example"></a>示例  
 **Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator**属性可以标记允许 UDT 实例状态的更改的方法。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 不允许在一个 UPDATE 语句的 SET 子句中设置两个 UDT 属性。 然而，您可以将一个方法标记为更改两个成员的赋值函数。  
  
> [!NOTE]  
>  在查询中不允许使用赋值函数方法。 这些方法只能在赋值语句或数据修改语句中调用。 如果一个方法标记为赋值函数不会返回**void** (或不是**Sub**在 Visual Basic 中)，CREATE TYPE 失败并出现错误。  
  
 下面的语句假定存在**三角形**UDT 具有**旋转**方法。 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]更新语句调用**旋转**方法：  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 **旋转**方法用修饰**SqlMethod**属性设置**IsMutator**到**true**以便[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以将标记形式的赋值函数方法的方法。 此代码还设置**OnNullCall**到**false**，其中向服务器指示该方法返回空引用 (**Nothing**在 Visual Basic 中) 如果任何输入参数为 null 引用。  
  
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
 在实现时采用用户定义的格式的 UDT，必须实现**读**并**编写**实现了 Microsoft.SqlServer.Server.IBinarySerialize 接口以处理序列化的方法和反序列化 UDT 数据。 此外必须指定**MaxByteSize**的属性**Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**。  
  
### <a name="the-currency-udt"></a>Currency UDT  
 **货币**UDT 是可以使用安装的 CLR 示例附带[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]开始， [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。  
  
 **货币**UDT 支持中的特定区域性的货币体系处理大量的资金。 必须定义两个字段：**字符串**有关**CultureInfo**，它指定货币的颁发者 (en-我们示例中) 和一个**十进制**为**CurrencyValue**，货币量。  
  
 尽管不使用由服务器来执行比较，但**货币**UDT 实现**System.IComparable**接口，公开了一个方法， **System.IComparable.CompareTo**。 在需要精确比较或排序区域性中的货币值的情况下，在客户端会使用此方法。  
  
 在 CLR 中运行的代码将区域性与货币值分开比较。 对于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码，通过执行下列操作来确定如何比较：  
  
1.  设置**IsByteOrdered**属性为 true，它会告知[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用磁盘上保留的二进制表示形式进行比较。  
  
2.  使用**编写**方法**货币**UDT 便可确定如何保持 UDT 在磁盘上，因此如何比较和排序的 UDT 值[!INCLUDE[tsql](../../includes/tsql-md.md)]操作。  
  
3.  保存**货币**使用以下二进制格式的 UDT:  
  
    1.  将区域性另存为 UTF-16 编码的字符串并用第 0-19 个字节表示，右侧以 Null 字符填充。  
  
    2.  使用第 20 个字节及以后的字节包含货币的十进制值。  
  
 填充的目的是为了确保区域性与货币值完全分开，以便在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码中将一个 UDT 与另一个 UDT 进行比较时，区域性字节与区域性字节相比较，货币字节值与货币字节值相比较。  
  
 有关完整代码清单**货币**UDT，按照中示例的说明安装 CLR [SQL Server 数据库引擎示例](http://msftengprodsamples.codeplex.com/)。  
  
### <a name="currency-attributes"></a>Currency 属性  
 **货币**UDT 定义具有以下属性。  
  
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
 当你选择**UserDefined**序列化格式，还必须实现**IBinarySerialize**接口，并创建您自己**读取**和**编写**方法。 以下过程从**货币**UDT 使用**System.IO.BinaryReader**并**System.IO.BinaryWriter**读取和写入 UDT。  
  
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
  
 有关完整代码清单**货币**UDT，请参阅[SQL Server 数据库引擎示例](http://msftengprodsamples.codeplex.com/)。  
  
## <a name="see-also"></a>请参阅  
 [创建用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
