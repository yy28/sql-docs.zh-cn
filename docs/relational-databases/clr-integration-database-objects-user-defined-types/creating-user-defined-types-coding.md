---
title: 编写用户定义类型的代码 |Microsoft Docs
description: 此示例演示如何实现在 SQL Server 数据库中使用的 UDT。 它将 UDT 作为结构实现。
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
ms.openlocfilehash: 5339a0d52754c19024a3774962d947bb4240ccba
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727823"
---
# <a name="creating-user-defined-types---coding"></a>创建用户定义类型 - 编码
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  编写用户定义类型 (UDT) 的定义时，必须根据是要将 UDT 作为类还是作为结构实现以及您所选择的格式和序列化选项来实现各种功能。  
  
 本节中的示例说明如何将**点**UDT 作为**结构**（或 Visual Basic 中的**结构**）实现。 **Point** UDT 包含作为属性过程实现的 X 和 Y 坐标。  
  
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
  
 **Microsoft SqlServer**命名空间包含 UDT 的各种属性所需的对象， **SqlTypes**命名空间包含表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用于程序集的本机数据类型的类。 当然，还可能存在程序集正常运行所需的其他命名空间。 **Point** UDT 还使用**system.web**命名空间来处理字符串。  
  
> [!NOTE]  
>  不支持执行用 **/clr： pure**编译的 Visual C++ 数据库对象（如 udt）。  
  
## <a name="specifying-attributes"></a>指定属性  
 属性确定如何使用序列化来构造 UDT 的存储表示形式以及如何按值将 UDT 传输到客户端。  
  
 **SqlUserDefinedTypeAttribute**是必需的。 **可序列化**属性是可选的。 你还可以指定**SqlFacetAttribute**以提供有关 UDT 的返回类型的信息。 有关详细信息，请参阅 [CLR 例程的自定义属性](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)。  
  
### <a name="point-udt-attributes"></a>Point UDT 属性  
 **SqlUserDefinedTypeAttribute**将**Point** UDT 的存储格式设置为 "**本机**"。 **IsByteOrdered**设置为**true**，这可保证 SQL Server 中比较的结果相同，就像在托管代码中进行相同的比较一样。 UDT 实现**SqlTypes. INullable**接口，使 udt 成为 null 感知。  
  
 下面的代码段显示了**Point** UDT 的特性。  
  
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
 除了为您的程序集正确指定属性外，UDT 还必须支持为 Null 性。 加载到中的 Udt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是可识别 null 的，但为使 udt 能够识别 null 值，udt 必须实现**SqlTypes. INullable**接口。  
  
 您必须创建一个名为**IsNull**的属性，该属性是在 CLR 代码内确定某个值是否为 null 所需要的。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发现 UDT 的 Null 实例时，会使用正常的 Null 处理方法来保留 UDT。 如果服务器不必序列化或反序列化 UDT，它不会在这些方面浪费时间；此外，它也不会浪费空间来存储 Null UDT。 每次从 CLR 中引入 UDT 时都会执行这种 Null 检查，也就是说，始终都应可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 构造来检查有无 Null UDT。 服务器还使用**IsNull**属性来测试实例是否为 null。 一旦服务器确定 UDT 为 Null，它便可以使用其本机 Null 处理方法。  
  
 **IsNull**的**get （）** 方法不以任何方式进行特殊大小写。 如果**点**变量** \@ p**为**Null**，则默认情况下，将计算为 "null"，而不是 "1 ** \@ "。** 这是因为**IsNull get （）** 方法的**SqlMethod （OnNullCall）** 特性默认为 false。 由于对象为**Null**，因此当请求属性时，对象未反序列化时，不会调用方法，并且返回默认值 "Null"。  
  
### <a name="example"></a>示例  
 在下面的示例中，`is_Null` 变量是私有的并且保存了 UDT 实例的 Null 状态。 您的代码必须保留 `is_Null` 的相应值。 UDT 还必须具有一个名为**null**的静态属性，该属性将返回 UDT 的 null 值实例。 这样，如果该实例在数据库中确实为 Null，UDT 便可返回 Null 值。  
  
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
 请考虑一个表，其中包含架构点（id int、位置点），其中**Point**是 CLR UDT，并且以下查询：  
  
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
  
 这两个查询都返回具有非**空**位置的点 id。 在 Query 1 中，使用的是正常 Null 处理方法，不需要反序列化 UDT。 另一方面，查询2必须反序列化每个非**Null**对象并调用 CLR 以获取**IsNull**属性的值。 显然，使用**IS NULL**将表现出更好的性能，并且永远不会有理由从代码中读取 UDT 的**IsNull**属性 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 那么，如何使用**IsNull**属性呢？ 首先，需要在 CLR 代码内确定某个值是否为**Null** 。 其次，服务器需要一种方法来测试实例是否为**Null**，因此服务器使用此属性。 确定为**Null**后，它可以使用其本机 Null 处理来处理它。  
  
## <a name="implementing-the-parse-method"></a>实现 Parse 方法  
 **Parse**和**ToString**方法允许与 UDT 的字符串表示形式相互转换。 **Parse**方法允许将字符串转换为 UDT。 它必须声明为**静态**（或在 Visual Basic 中**共享**），并采用**SqlTypes. SqlString**类型的参数。  
  
 下面的代码实现了用于**Point** UDT 的**Parse**方法，用于分离 X 和 Y 坐标。 **Parse**方法具有**SqlTypes. SqlString**类型的单个参数，并假定以逗号分隔的字符串形式提供 X 和 Y 值。 如果将**SqlMethodAttribute**属性设置为**false** ，则会阻止从 Point 的 null 实例调用**Parse**方法。  
  
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
 **ToString**方法将**Point** UDT 转换为字符串值。 在这种情况下，将为**点**类型的 NULL 实例返回字符串 "null"。 **ToString**方法使用 system.exception**返回以逗号**分隔的**system.string** ，其中包含 X 和 Y 坐标值，从而使**Parse**方法反转。 由于**InvokeIfReceiverIsNull**默认为 false，因此不需要检查是否为空的**Point**实例。  
  
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
 **Point** UDT 公开 X 和 Y 坐标，该坐标实现为类型为**system.object**的公共读写属性。  
  
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
  
 使用**SqlUserDefinedTypeAttribute 的 ValidationMethodName** **属性，可以**提供在将数据分配给 UDT 或转换为 udt 时服务器所运行的验证方法的名称，该方法由服务器运行。 在运行 bcp 实用工具 BULK INSERT、DBCC CHECKDB、DBCC CHECKFILEGROUP、DBCC CHECKTABLE、分布式查询和表格格式数据流（TDS）远程过程调用（RPC）操作期间也会调用**ValidationMethodName** 。 **ValidationMethodName**的默认值为 null，指示没有验证方法。  
  
### <a name="example"></a>示例  
 下面的代码段显示了**Point**类的声明，该声明指定了**ValidatePoint**的**ValidationMethodName** 。  
  
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
  
 验证方法可以具有任何范围，如果值有效，则应返回**true** ，否则返回**false** 。 如果该方法返回**false**或引发异常，则该值将被视为无效，并引发错误。  
  
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
  
 如果希望在所有情况下都执行验证方法，则必须从属性 setter 和**Parse**方法中显式调用验证方法。 并不要求这样做，在某些情况下可能甚至不需要这样做。  
  
### <a name="parse-validation-example"></a>Parse 验证示例  
 若要确保在**Point**类中调用**ValidatePoint**方法，必须从**Parse**方法和设置 X 和 Y 坐标值的属性过程中调用它。 下面的代码段演示如何从**Parse**函数调用**ValidatePoint**验证方法。  
  
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
 下面的代码段演示了如何从设置 X 和 Y 坐标的属性过程调用**ValidatePoint**验证方法。  
  
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
 编写 UDT 方法时，请考虑所用的算法是否可能会随时间的推移而改变。 如果可能改变的话，最好考虑为您的 UDT 所用的方法创建一个单独的类。 如果算法发生变化，则可以使用新代码重新编译该类并将程序集加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，而不会影响 UDT。 在许多情况下，都可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 语句重新加载 UDT，但这可能会使现有数据出现问题。 例如， **AdventureWorks**示例数据库附带的**Currency** UDT 使用**ConvertCurrency**函数转换货币值，该函数在单独的类中实现。 在未来，转换算法可能会发生不可预知的变化，或者可能需要新的功能。 在规划将来的更改时，将**ConvertCurrency**函数与**货币**UDT 实现分离可提供更大的灵活性。  
  
### <a name="example"></a>示例  
 **Point**类包含三种用于计算距离的简单方法：**距离**、 **DistanceFrom**和**DistanceFromXY**。 每个都返回一个**双精度**值，计算从**点**到零的距离、从指定点到**点**的距离，以及从指定的 X 和 Y 坐标到**点**的距离。 每个调用**DistanceFromXY**的**距离**和**DistanceFrom** ，并演示如何对每个方法使用不同的参数。  
  
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
 **SqlMethodAttribute**类提供自定义属性，这些属性可用于标记方法定义，以便指定确定性、调用 null 调用行为，并指定方法是否为赋值函数。 使用的是这些属性的默认值，仅在需要非默认值时才使用自定义特性。  
  
> [!NOTE]  
>  **SqlMethodAttribute**类继承自**SqlFunctionAttribute**类，因此**SqlMethodAttribute**继承了**TableDefinition**中的**FillRowMethodName**和**SqlFunctionAttribute**字段。 这意味着可以编写一个不属于此情况的表值方法。 方法会编译和程序集，但在运行时将引发关于**IEnumerable**返回类型的错误，并返回以下消息： "程序集" "的类" "中的" 方法、属性或字段 "" \<name> \<class> \<assembly> 具有无效的返回类型。 "  
  
 下表描述了可在 UDT 方法中使用的一些相关**SqlMethodAttribute**属性，并列出了这些属性的默认值。  
  
 DataAccess  
 指示函数是否需要访问存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地实例中的用户数据。 默认值为**dataaccesskind.read**。**无**。  
  
 IsDeterministic  
 指示在输入值相同且数据库状态相同的情况下函数是否会生成相同的输出值。 默认值为 **false**。  
  
 IsMutator  
 指示方法是否在 UDT 实例中引起状态变化。 默认值为 **false**。  
  
 IsPrecise  
 指示函数是否涉及不精确的计算，如浮点运算。 默认值为 **false**。  
  
 OnNullCall  
 指示在指定 Null 引用输入参数时是否调用此方法。 默认值为**true**。  
  
### <a name="example"></a>示例  
 **SqlMethodAttribute. IsMutator**属性允许您标记允许 UDT 实例状态发生变化的方法。）的类型为。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 不允许在一个 UPDATE 语句的 SET 子句中设置两个 UDT 属性。 然而，您可以将一个方法标记为更改两个成员的赋值函数。  
  
> [!NOTE]  
>  在查询中不允许使用赋值函数方法。 这些方法只能在赋值语句或数据修改语句中调用。 如果标记为赋值函数的方法不会返回**void** （或不是 Visual Basic 中的**Sub** ），则 CREATE TYPE 将失败并出现错误。  
  
 下面的语句假定存在具有**旋转**方法的**三角形**UDT。 下面的 [!INCLUDE[tsql](../../includes/tsql-md.md)] update 语句调用**旋转**方法：  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 **旋转**方法使用**SqlMethod**特性将**IsMutator**设置为**true** ，以便 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以将该方法标记为赋值函数方法。 此代码还会将**OnNullCall**设置为**false**，这向服务器指示，如果任何输入参数为 null 引用，则该方法返回 null 引用（在 Visual Basic 中为**Nothing** ）。  
  
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
 使用用户定义格式实现 UDT 时，必须实现用于实现 IBinarySerialize 接口的**读取**和**写入**方法，以处理序列化和反序列化 UDT 数据。 你还必须指定**SqlUserDefinedTypeAttribute**的**MaxByteSize**属性。  
  
### <a name="the-currency-udt"></a>Currency UDT  
 与一起安装的 CLR 示例附带了**货币**UDT [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，从开始 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。  
  
 **Currency** UDT 支持在特定区域性的货币系统中处理金钱量。 必须定义两个字段：用于**CultureInfo**的**字符串**，用于指定哪个用户颁发了货币（例如 en-us），并为**CurrencyValue**的**小**数值指定了货币。  
  
 尽管服务器不使用它来执行比较，但**货币**UDT 实现了**system.web**接口，该接口公开单一方法**CompareTo**。 在需要精确比较或排序区域性中的货币值的情况下，在客户端会使用此方法。  
  
 在 CLR 中运行的代码将区域性与货币值分开比较。 对于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码，通过执行下列操作来确定如何比较：  
  
1.  将**IsByteOrdered**属性设置为 true，这将告知 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用磁盘上保留的二进制表示形式进行比较。  
  
2.  使用**Currency** Udt 的**Write**方法来确定 udt 如何持久保存在磁盘上，进而确定如何比较和排序 [!INCLUDE[tsql](../../includes/tsql-md.md)] 操作。  
  
3.  使用以下二进制格式保存**货币**UDT：  

    1.  将区域性另存为 UTF-16 编码的字符串并用第 0-19 个字节表示，右侧以 Null 字符填充。  
  
    2.  使用第 20 个字节及以后的字节包含货币的十进制值。  
  
 填充的目的是为了确保区域性与货币值完全分开，以便在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码中将一个 UDT 与另一个 UDT 进行比较时，区域性字节与区域性字节相比较，货币字节值与货币字节值相比较。  
  
 有关**货币**UDT 的完整代码列表，请按照[SQL Server 数据库引擎示例](https://msftengprodsamples.codeplex.com/)中有关安装 CLR 示例的说明进行操作。  
  
### <a name="currency-attributes"></a>Currency 属性  
 用以下属性定义了**货币**UDT。  
  
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
 选择**用户**定义的序列化格式时，还必须实现**IBinarySerialize**接口，并创建自己**Read**的读**写**方法。 下面的从**货币**UDT 中的过程使用**BinaryReader**和**BinaryWriter**从 UDT 读取和向其写入。  
  
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
  
 有关**货币**UDT 的完整代码列表，请参阅[SQL Server 数据库引擎示例](https://msftengprodsamples.codeplex.com/)。  
  
## <a name="see-also"></a>另请参阅  
 [Creating a User-Defined Type（创建用户定义类型）](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
