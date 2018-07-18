---
title: CLR 标量值函数 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- SVF
- scalar-valued functions
ms.assetid: 20dcf802-c27d-4722-9cd3-206b1e77bee0
caps.latest.revision: 81
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6de41e4ceecc281515250812dd85ec439afaf2b8
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37353519"
---
# <a name="clr-scalar-valued-functions"></a>CLR 标量值函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  标量值函数 (SVF) 返回单个值，例如字符串、整数或位值。您可以使用任何 .NET Framework 编程语言以托管代码形式创建标量值用户定义函数。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他托管代码可访问这些函数。 有关优点的 CLR 集成和托管代码之间进行选择并[!INCLUDE[tsql](../../includes/tsql-md.md)]，请参阅[CLR 集成概述](../../relational-databases/clr-integration/clr-integration-overview.md)。  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>CLR 标量值函数的要求  
 在 .NET Framework 程序集中 .NET Framework  SVF 将实现为类的方法。 输入的参数和 svf 返回的类型可以是任何支持的标量数据类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，除非**varchar**， **char**， **rowversion**， **文本**， **ntext**，**图像**，**时间戳**，**表**，或**游标**. SVF 必须确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和实现方法的返回数据类型相匹配。 有关类型转换的详细信息，请参阅[映射 CLR 参数数据](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。  
  
 在.NET Framework 语言中，实现.NET Framework SVF 时**SqlFunction**可以指定自定义特性来包含有关该函数的其他信息。 **SqlFunction**属性指示函数是否访问或修改数据，是否是确定性的并且该函数是否涉及浮点运算。  
  
 标量值用户定义函数可以是确定性函数也可以是不确定性函数。 如果使用一组特定的输入参数调用某个确定性函数，则该确定性函数始终返回相同的结果。 如果使用一组特定的输入参数调用某个不确定性函数，则该不确定性函数返回的结果可能会不同。  
  
> [!NOTE]  
>  在输入值相同且数据库状态相同的情况下，如果某函数并不总是产生相同的输出值，请不要将该函数标记为确定性函数。 如果函数不具备真正的确定性而将其标记为确定性函数，将可能产生损坏的索引视图和计算列。 通过设置标记为确定性函数**IsDeterministic**属性设为 true。  
  
### <a name="table-valued-parameters"></a>表值参数  
 表值参数 (TVP) 即传递到某一过程或函数的用户定义表类型，它提供了一种将多行数据传递到服务器的高效方法。 TVP 提供与参数数组类似的功能，但灵活性更高并且与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成更紧密。 它们还提供提升性能的潜力。 TVP 还有助于减少到服务器的往返次数。 可以将数据作为 TVP 发送到服务器，而不是向服务器发送多个请求（例如，对于标量参数列表）。 用户定义表类型不能作为表值参数传递到在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中执行的托管存储过程或函数，也不能从这些存储过程或函数中返回。 有关 Tvp 的详细信息，请参阅[使用表值参数&#40;数据库引擎&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
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
  
 代码引用的第一行**Microsoft.SqlServer.Server**以访问属性和**System.Data.SqlClient**以访问 ADO.NET 命名空间。 (此命名空间包含**SqlClient**，用于.NET Framework 数据提供程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。)  
  
 接下来，该函数收到**SqlFunction**自定义属性，它位于**Microsoft.SqlServer.Server**命名空间。 该自定义属性指示用户定义函数 (UDF) 是否使用进程内访问接口来读取服务器中的数据。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许 UDF 更新、插入或删除数据。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以优化执行不使用进程内访问接口的 UDF。 这会指示通过设置**DataAccessKind**到**DataAccessKind.None**。 在下一行中，目标方法为公共静态方法（在 Visual Basic .NET 中为 shared）。  
  
 **SqlContext**类，位于**Microsoft.SqlServer.Server**命名空间，然后，可以访问**SqlCommand**连接到的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已设置的实例。 虽然这里未使用当前事务上下文也是可通过**System.Transactions**应用程序编程接口 (API)。  
  
 在函数体中的代码行的大多数来说应该很熟悉的开发人员可以编写客户端应用程序中找到类型使用**System.Data.SqlClient**命名空间。  
  
 [C#]  
  
```  
using(SqlConnection conn = new SqlConnection("context connection=true"))   
{  
   conn.Open();  
   SqlCommand cmd = new SqlCommand(  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
   return (int) cmd.ExecuteScalar();  
}    
```  
  
 [Visual Basic]  
  
```  
Using conn As New SqlConnection("context connection=true")  
   conn.Open()  
   Dim cmd As New SqlCommand( _  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
   Return CType(cmd.ExecuteScalar(), Integer)  
End Using  
```  
  
 初始化指定相应的命令文本**SqlCommand**对象。 前面的示例对表中的行数进行计数**SalesOrderHeader**。 下一步， **ExecuteScalar**方法**cmd**调用对象。 这将返回类型的值**int**基于查询。 最后，将订单计数返回给调用方。  
  
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
>  使用 visual c + + 数据库对象编译 **/clr: pure**上不支持执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 例如，此类数据库对象包含标量值函数。  
  
 用于注册程序集和 UDF 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询及示例调用如下：  
  
```  
CREATE ASSEMBLY FirstUdf FROM 'FirstUdf.dll';  
GO  
  
CREATE FUNCTION CountSalesOrderHeader() RETURNS INT   
AS EXTERNAL NAME FirstUdf.T.ReturnOrderCount;   
GO  
  
SELECT dbo.CountSalesOrderHeader();  
GO  
  
```  
  
 请注意，[!INCLUDE[tsql](../../includes/tsql-md.md)] 中显示的函数名称不需要与目标公共静态方法的名称匹配。  
  
## <a name="see-also"></a>请参阅  
 [映射 CLR 参数数据](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [CLR 集成自定义属性的概述](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)   
 [用户定义的函数](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 [从 CLR 数据库对象进行数据访问](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
