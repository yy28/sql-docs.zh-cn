---
title: 处理 null 值
description: 演示如何在 SQL Server 和 .NET 中使用 GUID 和 uniqueidentifier 值。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 6ae2bc8d816dd2bc32572447483dacd76dd967f0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452185"
---
# <a name="handling-null-values"></a>处理 null 值

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

如果列中的值未知或缺失，则使用关系数据库中的 null 值。 Null 既不是空字符串（对于字符或日期/时间数据类型），也不是零值（对于数值数据类型）。 ANSI SQL-92 规范规定，所有数据类型的 null 值必须相同，以便一致地处理所有 null 值。 @No__t_0 命名空间通过实现 <xref:System.Data.SqlTypes.INullable> 接口提供 null 语义。 @No__t_0 中的每个数据类型都有自己的 `IsNull` 属性和可分配给该数据类型的实例的 `Null` 值。  
  
> [!NOTE]
>  .NET Framework 版本2.0 和 .NET Core 1.0 版本引入了对可以为 null 的类型的支持，这些类型使程序员可以扩展值类型来表示基础类型的所有值。 这些 CLR 可以为 null 的类型表示 <xref:System.Nullable> 结构的实例。 当对值类型进行装箱和取消装箱时，此功能特别有用，从而增强了与对象类型的兼容性。 CLR 可以为 null 的类型不用于存储数据库 null 值，因为 ANSI SQL null 与 `null` 引用（或 Visual Basic 中 `Nothing`）的行为方式不同。 若要使用数据库 ANSI SQL null 值，请使用 <xref:System.Data.SqlTypes> null 值，而不是 <xref:System.Nullable>。 有关使用C#中的 CLR 可以为 null 的类型的详细信息，请参阅可为[null](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/)的类型; 有关[使用可以为 null](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/using-nullable-types/)的C#类型。  
  
## <a name="nulls-and-three-valued-logic"></a>空值和三值逻辑  
允许列定义中的 null 值在应用程序中引入了三值逻辑。 比较的计算结果可以为以下三种情况之一：  
  
- True  
  
- False  
  
- Unknown  
  
由于 null 被视为未知，因此两个 null 值之间的比较不被视为相等。 在使用算术运算符的表达式中，如果有任何操作数为 null，则结果也为 null。  
  
## <a name="nulls-and-sqlboolean"></a>Null 和 SqlBoolean  
任何 <xref:System.Data.SqlTypes> 之间的比较将返回一个 <xref:System.Data.SqlTypes.SqlBoolean>。 每个 `SqlType` 的 `IsNull` 函数都返回 <xref:System.Data.SqlTypes.SqlBoolean>，并可用于检查 null 值。 以下事实数据表显示了 AND、OR 和 NOT 运算符在是否存在 null 值的情况下的工作方式。 （T = true、F = false、U = 未知或 null。）  
  
![真值表](../media/truthtable-bpuedev11.gif "|::ref1::|")  
  
### <a name="understanding-the-ansi_nulls-option"></a>了解 ANSI_NULLS 选项  
<xref:System.Data.SqlTypes> 提供与在 SQL Server 中设置 ANSI_NULLS 选项时相同的语义。 如果上述任何操作数或自变量为 NULL，则所有算术运算符（+、-、*、/、%）、位运算符（~、&、&#124）和大多数函数都返回 NULL，只有属性 `IsNull` 除外。  
  
ANSI SQL-92 标准不支持 WHERE 子句中的 columnName = NULL  。 在 SQL Server 中，ANSI_NULLS 选项控制数据库中的默认为空性，并计算针对 null 值的比较。 如果 ANSI_NULLS 处于打开状态（默认值），则在测试 NULL 值时，必须在表达式中使用 IS NULL 运算符。 例如，当 ANSI_NULLS 为开启状态时，以下比较总是生成未知：  
  
```console
colname > NULL  
```  
  
比较包含 null 值的变量也会产生未知的：  
  
```console
colname > @MyVariable  
```  
  
使用 IS NULL 或 IS NOT NULL 谓词测试 NULL 值。 这将增加 WHERE 子句的复杂性。 例如，AdventureWorks Customer 表中的 TerritoryID 列允许 null 值。 如果 SELECT 语句不仅用于测试其他值，还用于测试 NULL 值，则该语句必须包括 IS NULL 谓词：  
  
```sql
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
如果在 SQL Server 中将 ANSI_NULLS 设置为 off，则可以创建使用相等运算符来与 null 进行比较的表达式。 但是，您不能阻止不同的连接为该连接设置 null 选项。 使用 IS NULL 测试 null 值始终有效，而不考虑连接的 ANSI_NULLS 设置。  
  
@No__t_0 中不支持设置 ANSI_NULLS off，这始终遵循用于处理 <xref:System.Data.SqlTypes> 中的 null 值的 ANSI SQL-92 标准。  
  
## <a name="assigning-null-values"></a>分配 null 值  
空值是特殊值，其存储和分配语义在不同类型系统和存储系统之间有所不同。 @No__t_0 旨在与不同的类型和存储系统一起使用。  
  
本部分介绍用于将 null 值分配给不同类型系统中 <xref:System.Data.DataRow> 的 <xref:System.Data.DataColumn> 的 null 语义。  
  
`DBNull.Value`  
此分配对于任何类型的 `DataColumn` 都有效。 如果类型 `INullable` 实现，则将 `DBNull.Value` 强制转换为相应的强类型 Null 值。  
  
`SqlType.Null`  
所有 <xref:System.Data.SqlTypes> 的数据类型都实现 `INullable`。 如果可使用隐式强制转换运算符将强类型的 null 值转换为列的数据类型，则应进行赋值。 否则，将引发无效的强制转换异常。  
  
`null`  
如果 "null" 是给定 `DataColumn` 数据类型的合法值，则会将其强制转换为与 `INullable` 类型（`SqlType.Null`）关联的相应 `DbNull.Value` 或 `Null`  
  
`derivedUdt.Null`  
对于 UDT 列，将始终基于与 `DataColumn` 关联的类型存储 null 值。 请考虑与 `DataColumn` 关联的 UDT 的情况，该 UDT 不实现 `INullable` 的子类。 在这种情况下，如果分配了与派生类关联的强类型 null 值，则会将其存储为非类型化 `DbNull.Value`，因为 null 存储始终与 DataColumn 的数据类型一致。  
  
> [!NOTE]
>  @No__t_2 当前不支持 `Nullable<T>` 或 <xref:System.Nullable> 结构。  
  
### <a name="multiple-column-row-assignment"></a>多列（行）赋值  
`DataTable.Add`、`DataTable.LoadDataRow` 或接受映射到行的 <xref:System.Data.DataRow.ItemArray%2A> 的其他 Api，请将 "null" 映射到 DataColumn 的默认值。 如果数组中的对象包含 `DbNull.Value` 或其强类型对应项，则将应用上述规则。  
  
此外，以下规则适用于 `DataRow.["columnName"]` null 赋值的实例：  
  
- 对于所有列，默认值为 `DbNull.Value`，但强类型 NULL 列除外，强类型 NULL 列的默认值是相应的强类型 NULL 值  。  
  
- 在序列化为 XML 文件的过程中，空值永远不会写出（如在 "xsi： nil" 中）。  
  
- 在序列化为 XML 时，所有非 null 值（包括默认值）始终写出。 这不同于 XSD/XML 语义，其中 null 值（xsi： nil）是显式的，默认值是隐式的（如果在 XML 中不存在，验证分析器可以从关联的 XSD 架构获取它）。 与 `DataTable` 相反： null 值是隐式的，默认值是显式的。  
  
- 从 XML 输入读取的行的所有缺少列值都将分配为 NULL。 使用 <xref:System.Data.DataTable.NewRow%2A> 或类似方法创建的行被分配给 DataColumn 的默认值。  
  
- @No__t_0 方法返回 `DbNull.Value` 和 `INullable.Null` 的 `true`。  
  
## <a name="assigning-null-values"></a>分配 null 值  
任何 <xref:System.Data.SqlTypes> 实例的默认值均为 null。  
  
@No__t_0 中的 null 值是特定类型的，不能由单个值表示，如 `DbNull`。 使用 `IsNull` 属性检查是否有 null 值。  
  
空值可以分配给 <xref:System.Data.DataColumn>，如下面的代码示例中所示。 可以直接将 null 值分配给 `SqlTypes` 变量，而不会触发异常。  
  
### <a name="example"></a>示例  
下面的代码示例创建一个 <xref:System.Data.DataTable>，其中两列定义为 <xref:System.Data.SqlTypes.SqlInt32> 和 <xref:System.Data.SqlTypes.SqlString>。 该代码将添加一行已知值、一行 null 值，然后循环访问 <xref:System.Data.DataTable>，将值分配给变量并在控制台窗口中显示输出。  
  
[!code-csharp[DataWorks SqlInt32_IsNull#1](~/../sqlclient/doc/samples/SqlInt32_IsNull.cs#1)]
  
此示例显示以下结果：  
  
```console
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a>将 null 值与 SqlTypes 和 CLR 类型进行比较  
比较 null 值时，请务必了解 `Equals` 方法计算 <xref:System.Data.SqlTypes> 中 null 值的方式之间的差异，与它与 CLR 类型的工作方式相比。 所有 <xref:System.Data.SqlTypes> `Equals` 方法都使用数据库语义计算 null 值：如果两个值中的一个或两个都为 null，则比较结果为 null。 另一方面，如果两个都为 null，则对两个 <xref:System.Data.SqlTypes> 使用 CLR `Equals` 方法将产生 true。 这反映了使用实例方法（如 CLR `String.Equals` 方法）和使用静态/共享方法 `SqlString.Equals` 的差异。  
  
下面的示例演示 `SqlString.Equals` 方法与 `String.Equals` 方法之间的不同之处，当每个传递一对 null 值，然后是一对空字符串时。  
  
[!code-csharp[DataWorks SqlString_Equals#1](~/../sqlclient/doc/samples/SqlString_Equals.cs#1)]
  
此代码将产生以下输出：  
  
```console
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True   
```  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 数据类型和 ADO.NET](sql-server-data-types.md)
