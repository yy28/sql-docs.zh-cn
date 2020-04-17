---
title: 编码用户定义类型 |微软文档
description: 此示例演示如何实现要在 SQL Server 数据库中使用的 UDT。 它实现 UDT 作为一个结构。
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
ms.openlocfilehash: a9d51cc0c33c8b656df176baa606a88a542ca4bc
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486948"
---
# <a name="creating-user-defined-types---coding"></a>创建用户定义类型 - 编码
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  编写用户定义类型 (UDT) 的定义时，必须根据是要将 UDT 作为类还是作为结构实现以及您所选择的格式和序列化选项来实现各种功能。  
  
 本节中的示例演示了将**点**UDT 实现为**结构**（或可视化基本**结构**）。 **点**UDT 由 X 和 Y 坐标组成，这些坐标作为属性过程实现。  
  
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
  
 **Microsoft.SqlServer.Server.Server**命名空间包含 UDT 的各种属性所需的对象，**而 System.Data.SqlType**命名空间包含表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可用于程序集的本机数据类型的类。 当然，还可能存在程序集正常运行所需的其他命名空间。 **点**UDT 还使用**System.Text**命名空间处理字符串。  
  
> [!NOTE]  
>  可视C++数据库对象（如 UDT）与 **/clr：pure**编译，不支持执行。  
  
## <a name="specifying-attributes"></a>指定属性  
 属性确定如何使用序列化来构造 UDT 的存储表示形式以及如何按值将 UDT 传输到客户端。  
  
 **需要 Microsoft.SqlServer.Server.SqlUser 定义类型属性**。 **可序列化**属性是可选的。 您还可以指定**Microsoft.SqlServer.Server.SqlFacet属性**，以提供有关 UDT 的返回类型的信息。 有关详细信息，请参阅 [CLR 例程的自定义属性](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)。  
  
### <a name="point-udt-attributes"></a>Point UDT 属性  
 **Microsoft.SqlServer.Server.SqlUser 定义类型属性**将**点**UDT 的存储格式设置为**本机**。 **IsByteOrdered**设置为**true**，这可确保 SQL Server 中的比较结果与托管代码中发生的相同比较相同。 UDT 实现**System.Data.SqlType.INull 接口**，使 UDT 为 null。  
  
 以下代码片段显示**点**UDT 的属性。  
  
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
 除了为您的程序集正确指定属性外，UDT 还必须支持为 Null 性。 加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 UDT 是 null 感知的，但为了 UDT 识别空值，UDT 必须实现**System.Data.SqlType.Inull 接口**。  
  
 您必须创建一个名为**IsNull**的属性 ，这是确定 CLR 代码中的值是否为空所必需的。 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发现 UDT 的 Null 实例时，会使用正常的 Null 处理方法来保留 UDT。 如果服务器不必序列化或反序列化 UDT，它不会在这些方面浪费时间；此外，它也不会浪费空间来存储 Null UDT。 每次从 CLR 中引入 UDT 时都会执行这种 Null 检查，也就是说，始终都应可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL 构造来检查有无 Null UDT。 服务器还使用**IsNull**属性来测试实例是否为空。 一旦服务器确定 UDT 为 Null，它便可以使用其本机 Null 处理方法。  
  
 **IsNull**的**get（）** 方法不是任何特殊大小写方法。 如果**Point** **\@** 变量 p 为**Null，** 则**\@默认情况下 p.IsNull**将计算为"NULL"，而不是"1"。 这是因为**IsNull get（）** 方法的**SqlMethod（OnNullCall）** 属性默认为 false。 由于对象为**Null，** 因此在请求该属性时，对象不会反序列化，因此不会调用该方法，并返回默认值"NULL"。  
  
### <a name="example"></a>示例  
 在下面的示例中，`is_Null` 变量是私有的并且保存了 UDT 实例的 Null 状态。 您的代码必须保留 `is_Null` 的相应值。 UDT 还必须具有名为**Null**的静态属性，该属性返回 UDT 的 null 值实例。 这样，如果该实例在数据库中确实为 Null，UDT 便可返回 Null 值。  
  
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
 请考虑包含架构点（id int，位置点）的表，其中**Point**是 CLR UDT，以及以下查询：  
  
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
  
 两个查询都返回具有非**空**位置的点的 ID。 在 Query 1 中，使用的是正常 Null 处理方法，不需要反序列化 UDT。 另一方面，查询 2 必须取消序列化每个非**空**对象，并调用 CLR 以获取**IsNull**属性的值。 显然，使用**IS NULL**将表现出更好的性能，并且不应有任何理由从[!INCLUDE[tsql](../../includes/tsql-md.md)]代码读取 UDT 的**IsNull**属性。  
  
 那么 **，IsNull**属性的使用是什么？ 首先，需要确定 CLR 代码中的值是否**为空**。 其次，服务器需要一种方法来测试实例是否**为 Null，** 因此服务器使用此属性。 在它确定为**Null**后，可以使用其本机 null 处理来处理它。  
  
## <a name="implementing-the-parse-method"></a>实现 Parse 方法  
 **分析**方法和**ToString**方法允许 UDT 的字符串表示和转换。 **解析**方法允许将字符串转换为 UDT。 它必须声明为**静态**（或在可视基本中**共享**），并采用**类型系统.Data.SqlType.SqlString 的**参数。  
  
 以下代码实现**点**UDT 的**Parse**方法，该方法分离出 X 坐标和 Y 坐标。 **Parse**方法具有**类型 System.Data.SqlType.SqlString**的单个参数，并假定 X 和 Y 值作为逗号分隔字符串提供。 将**Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall**属性设置为**false**可防止从 Point 的空实例调用**Parse**方法。  
  
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
 **ToString**方法将**点**UDT 转换为字符串值。 在这种情况下，为**Point**类型的 Null 实例返回字符串"NULL"。 **ToString**方法通过使用**System.Text.StringBuilder**返回逗号分隔**系统.String**组成的 X 和 Y 坐标值来反转**分析**方法。 由于**InvokeIfReceiverIsNull**默认为 false，因此不需要检查**Point**的空实例。  
  
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
 **点**UDT 公开 X 和 Y 坐标，这些坐标作为**类型系统**的公共读写属性实现。  
  
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
  
 **Microsoft.SqlServer.Server.Server.SqlUser定义类型属性.验证方法名称**属性的**Microsoft.SqlServer.Server.SqlUser 定义类型属性**允许您提供服务器在将数据分配给 UDT 或转换为 UDT 时运行的验证方法的名称。 **验证方法名称**在 bcp 实用程序、BULK INSERT、DBCC CHECKDB、DBCC CHECKFILEGROUP、DBCC CHECKTABLE、分布式查询和表格数据流 （TDS） 远程过程调用 （RPC） 操作的运行期间也调用。 **验证方法名称**的默认值为 null，表示没有验证方法。  
  
### <a name="example"></a>示例  
 以下代码片段显示**Point**类的声明，该类指定**验证点的验证****方法名称**。  
  
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
  
 验证方法可以具有任何范围，如果值有效，则应返回**true，** 否则**为 false。** 如果方法返回**false**或引发异常，则该值将被视为无效，并引发错误。  
  
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
  
 如果希望验证方法在所有情况下都执行，则必须从属性设置器和**Parse**方法显式调用验证方法。 并不要求这样做，在某些情况下可能甚至不需要这样做。  
  
### <a name="parse-validation-example"></a>Parse 验证示例  
 为了确保在**Point**类中调用**ValidatePoint**方法，必须从**Parse**方法和设置 X 和 Y 坐标值的属性过程调用它。 以下代码片段演示如何从**Parse**函数调用**验证点**验证方法。  
  
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
 以下代码片段演示如何从设置 X 和 Y 坐标的属性过程调用**验证点**验证方法。  
  
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
 编写 UDT 方法时，请考虑所用的算法是否可能会随时间的推移而改变。 如果可能改变的话，最好考虑为您的 UDT 所用的方法创建一个单独的类。 如果算法发生变化，则可以使用新代码重新编译该类并将程序集加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，而不会影响 UDT。 在许多情况下，都可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY 语句重新加载 UDT，但这可能会使现有数据出现问题。 例如 **，AdventureWorks**示例数据库中包含的**货币**UDT 使用**ConvertCurrency**函数来转换货币值，该币值在单独的类中实现。 在未来，转换算法可能会发生不可预知的变化，或者可能需要新的功能。 在规划未来更改时，将**ConvertCurrency**函数与**货币**UDT 实现分离提供了更大的灵活性。  
  
### <a name="example"></a>示例  
 **Point**类包含三种计算距离的简单方法：**距离**、**距离**和**距离距离。** 每个返回一**个双精度**值，计算从**点**到零的距离，从指定点到**点**的距离，以及从指定的 X 和 Y 坐标到**点**的距离。 **距离**和**距离从**每个调用**距离距离从XY，** 并演示如何使用不同的参数，每种方法。  
  
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
 **Microsoft.SqlServer.Server.SqlMethodattribute**类提供自定义属性，可用于标记方法定义，以便指定确定性、空调用行为以及指定方法是否为突变体。 使用的是这些属性的默认值，仅在需要非默认值时才使用自定义特性。  
  
> [!NOTE]  
>  **SqlMethodAttribute**类从**SqlFunctionattribute**类继承，因此**SqlMethodattribute**从**Sql功能属性**继承**FillRowMethodName 和****表定义**字段。 这意味着可以编写一个不属于此情况的表值方法。 该方法编译和程序集部署，但在运行时引发有关**IE5ble**返回类型的错误，并显示以下消息："程序集'\<\<\<程序集>'类'类>'中的方法、属性或字段'名称>'具有无效的返回类型。  
  
 下表描述了一些相关的**Microsoft.SqlServer.Server.SqlMethodAttribute**属性，这些属性可用于 UDT 方法，并列出了它们的默认值。  
  
 DataAccess  
 指示函数是否需要访问存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地实例中的用户数据。 默认值为**数据访问。****无**。  
  
 IsDeterministic  
 指示在输入值相同且数据库状态相同的情况下函数是否会生成相同的输出值。 默认值**为 false**。  
  
 IsMutator  
 指示方法是否在 UDT 实例中引起状态变化。 默认值**为 false**。  
  
 IsPrecise  
 指示函数是否涉及不精确的计算，如浮点运算。 默认值**为 false**。  
  
 OnNullCall  
 指示在指定 Null 引用输入参数时是否调用此方法。 默认值**为 true**。  
  
### <a name="example"></a>示例  
 **Microsoft.SqlServer.Server.SqlMethodattribute.IsMutator**属性允许您标记允许更改 UDT 实例状态的方法。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 不允许在一个 UPDATE 语句的 SET 子句中设置两个 UDT 属性。 然而，您可以将一个方法标记为更改两个成员的赋值函数。  
  
> [!NOTE]  
>  在查询中不允许使用赋值函数方法。 这些方法只能在赋值语句或数据修改语句中调用。 如果标记为突变体的方法不返回**void（** 或不是可视化基本中的**子），** 则 CREATE TYPE 失败，并出现错误。  
  
 以下语句假定存在具有**旋转**方法**的三角形**UDT。 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]更新语句调用**Rotate**方法：  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 **Rotate**方法使用**SqlMethod**属性设置**IsMutator** **进行**true[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]进行修饰，以便将该方法标记为突变器方法。 代码还将**OnNullCall**设置为**false**，它向服务器指示，如果任何输入参数为空引用，该方法将返回空引用（Visual Basic 中**没有任何内容**）。  
  
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
 实现具有用户定义的格式的 UDT 时，必须实现实现 Microsoft.SqlServer.Server.Server.IBinary 序列化接口的**读取**和**写入**方法，以处理序列化和反序列化 UDT 数据。 您还必须指定**Microsoft.SqlServer.Server.Server.SqlUser 定义类型属性**的**MaxByteSize**属性。  
  
### <a name="the-currency-udt"></a>Currency UDT  
 **货币**UDT 包含在 CLR 示例中，该示例可[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]随 安装[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，以 开头。  
  
 **货币**UDT 支持在特定区域性的货币系统中处理金额。 您必须定义两个字段：**区域性信息**的**字符串**，它指定货币的发行者（例如，en-us）和**货币价值****的小数，** 即货币金额。  
  
 虽然服务器不使用它执行比较，**但货币**UDT实现了**System.IThe接口**，该接口公开了单个方法**System.ICompbe.比较。** 在需要精确比较或排序区域性中的货币值的情况下，在客户端会使用此方法。  
  
 在 CLR 中运行的代码将区域性与货币值分开比较。 对于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码，通过执行下列操作来确定如何比较：  
  
1.  将**IsByteOrdered**属性设置为 true，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]该属性指示在磁盘上使用持久化二进制表示形式进行比较。  
  
2.  使用**货币**UDT 的**写入**方法确定 UDT 在磁盘上如何持久化，从而确定如何比较 UDT 值并为[!INCLUDE[tsql](../../includes/tsql-md.md)]操作排序。  
  
3.  使用以下二进制格式保存**货币**UDT：  

    1.  将区域性另存为 UTF-16 编码的字符串并用第 0-19 个字节表示，右侧以 Null 字符填充。  
  
    2.  使用第 20 个字节及以后的字节包含货币的十进制值。  
  
 填充的目的是为了确保区域性与货币值完全分开，以便在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码中将一个 UDT 与另一个 UDT 进行比较时，区域性字节与区域性字节相比较，货币字节值与货币字节值相比较。  
  
 有关**货币**UDT 的完整代码列表，请按照在[SQL Server 数据库引擎示例中](https://msftengprodsamples.codeplex.com/)安装 CLR 示例的说明进行操作。  
  
### <a name="currency-attributes"></a>Currency 属性  
 **货币**UDT 使用以下属性定义。  
  
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
 当您选择**用户定义的**序列化格式时，还必须实现**IBinary 序列化**接口并创建自己的**读****写**方法。 **货币**UDT 中的以下过程使用**System.IO.BinaryReader**和**System.IO.BinaryWriter**读取和写入 UDT。  
  
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
  
  
