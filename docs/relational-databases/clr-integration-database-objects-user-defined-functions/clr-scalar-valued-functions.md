---
title: CLR 标量值函数 |Microsoft Docs
description: 标量值函数返回单个值。 在 SQL Server CLR 集成中，可以在托管代码中编写标量值用户定义函数。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- SVF
- scalar-valued functions
ms.assetid: 20dcf802-c27d-4722-9cd3-206b1e77bee0
author: rothja
ms.author: jroth
ms.openlocfilehash: e69f48867cc5dd66d72d30f6fa72b2d44d5fc54c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719899"
---
# <a name="clr-scalar-valued-functions"></a>CLR 标量值函数
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  标量值函数 (SVF) 返回单个值，例如字符串、整数或位值。 您可以使用任何 .NET Framework 的编程语言在托管代码中创建标量值用户定义函数。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他托管代码可访问这些函数。 有关 CLR 集成的优点以及如何在托管代码和之间进行选择的信息 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，请参阅[Clr 集成概述](../../relational-databases/clr-integration/clr-integration-overview.md)。  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>CLR 标量值函数的要求  
 在 .NET Framework 程序集中 .NET Framework  SVF 将实现为类的方法。 输入参数和从 SVF 返回的类型可以是支持的任何标量数据类型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ， **varchar**、 **char**、 **rowversion**、 **text**、 **ntext**、 **image**、 **timestamp**、 **table**或**cursor**除外。 SVF 必须确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和实现方法的返回数据类型相匹配。 有关类型转换的详细信息，请参阅[映射 CLR 参数数据](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。  
  
 使用 .NET Framework 语言实现 .NET Framework SVF 时，可以指定**SqlFunction**自定义属性以包括有关函数的其他信息。 **SqlFunction**特性指示函数是否访问或修改数据（如果该函数是确定性的），以及该函数是否涉及浮点运算。  
  
 标量值用户定义函数可以是确定性函数也可以是不确定性函数。 如果使用一组特定的输入参数调用某个确定性函数，则该确定性函数始终返回相同的结果。 如果使用一组特定的输入参数调用某个不确定性函数，则该不确定性函数返回的结果可能会不同。  
  
> [!NOTE]  
>  在输入值相同且数据库状态相同的情况下，如果某函数并不总是产生相同的输出值，请不要将该函数标记为确定性函数。 如果函数不具备真正的确定性而将其标记为确定性函数，将可能产生损坏的索引视图和计算列。 可以通过将**IsDeterministic**属性设置为 true，将函数标记为确定性函数。  
  
### <a name="table-valued-parameters"></a>表值参数  
 表值参数 (TVP) 即传递到某一过程或函数的用户定义表类型，它提供了一种将多行数据传递到服务器的高效方法。 TVP 提供与参数数组类似的功能，但灵活性更高并且与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成更紧密。 它们还提供提升性能的潜力。 TVP 还有助于减少到服务器的往返次数。 可以将数据作为 TVP 发送到服务器，而不是向服务器发送多个请求（例如，对于标量参数列表）。 用户定义表类型不能作为表值参数传递到在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中执行的托管存储过程或函数，也不能从这些存储过程或函数中返回。 有关 Tvp 的详细信息，请参阅[&#40;数据库引擎使用表值参数&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
## <a name="example-of-a-clr-scalar-valued-function"></a>CLR 标量值函数示例  
 下面是访问数据并返回一个整数值的 SVF 示例：  
  
```csharp  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public class T  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static int ReturnOrderCount()  
    {  
        using (SqlConnection conn   
            = new SqlConnection("context connection=true"))  
        {  
            conn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
            return (int)cmd.ExecuteScalar();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public Class T  
    <SqlFunction(DataAccess:=DataAccessKind.Read)> _  
    Public Shared Function ReturnOrderCount() As Integer  
        Using conn As New SqlConnection("context connection=true")  
            conn.Open()  
            Dim cmd As New SqlCommand("SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
            Return CType(cmd.ExecuteScalar(), Integer)  
        End Using  
    End Function  
End Class  
```  
  
 第一行代码引用 SqlClient 来**访问**ADO.NET 命名空间，以访问属性和**System.Data.SqlClient** 。 （此命名空间包含**SqlClient**，它是的 .NET Framework 数据提供程序 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。）  
  
 接下来，该函数接收在**SqlFunction** **命名空间**中找到的自定义属性。 该自定义属性指示用户定义函数 (UDF) 是否使用进程内访问接口来读取服务器中的数据。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许 UDF 更新、插入或删除数据。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以优化执行不使用进程内访问接口的 UDF。 这可通过将**dataaccesskind.read**设置为**dataaccesskind.read**来指示。 在下一行中，目标方法为公共静态方法（在 Visual Basic .NET 中为 shared）。  
  
 然后，位于 SqlContext**命名空间中的** **SqlContext**类可以使用连接到已设置的实例的连接来访问**SqlCommand**对象 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 尽管此处未使用，但当前事务上下文还可通过**System.** transaction 应用程序编程接口（API）来使用。  
  
 编写使用**SqlClient**命名空间中的类型的客户端应用程序的开发人员应熟悉函数体中的大部分代码行。  
  
 [C#]  
  
```csharp
using(SqlConnection conn = new SqlConnection("context connection=true"))   
{  
   conn.Open();  
   SqlCommand cmd = new SqlCommand(  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
   return (int) cmd.ExecuteScalar();  
}    
```  
  
 [Visual Basic]  
  
```vb
Using conn As New SqlConnection("context connection=true")  
   conn.Open()  
   Dim cmd As New SqlCommand( _  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
   Return CType(cmd.ExecuteScalar(), Integer)  
End Using  
```  
  
 通过初始化**SqlCommand**对象指定适当的命令文本。 前面的示例对表**SalesOrderHeader**中的行数进行计数。 接下来，调用**cmd**对象的**ExecuteScalar**方法。 这将基于查询返回**int**类型的值。 最后，将订单计数返回给调用方。  
  
 如果此代码保存在名为 FirstUdf.cs 的文件中，则它将能够编译到如下的程序集中：  
  
 [C#]  
  
```  
csc.exe /t:library /out:FirstUdf.dll FirstUdf.cs   
```  
  
 [Visual Basic]  
  
```  
vbc.exe /t:library /out:FirstUdf.dll FirstUdf.vb  
```  
  
> [!NOTE]  
>  `/t:library` 指示应生成一个库，而非可执行程序。 可执行程序无法在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中进行注册。  
  
> [!NOTE]  
>  不支持在上执行的 Visual C++ 用 **/clr： pure**编译的数据库对象 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 例如，此类数据库对象包含标量值函数。  
  
 用于注册程序集和 UDF 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询及示例调用如下：  
  
```sql
CREATE ASSEMBLY FirstUdf FROM 'FirstUdf.dll';  
GO  
  
CREATE FUNCTION CountSalesOrderHeader() RETURNS INT   
AS EXTERNAL NAME FirstUdf.T.ReturnOrderCount;   
GO  
  
SELECT dbo.CountSalesOrderHeader();  
GO  
  
```  
  
 请注意，[!INCLUDE[tsql](../../includes/tsql-md.md)] 中显示的函数名称不需要与目标公共静态方法的名称匹配。  
  
## <a name="see-also"></a>另请参阅  
 [映射 CLR 参数数据](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [CLR 集成自定义特性概述](https://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)   
 [用户定义函数](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 [从 CLR 数据库对象进行数据访问](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
