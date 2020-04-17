---
title: CLR Scalar 值函数 |微软文档
description: 标量值函数返回单个值。 在 SQL Server CLR 集成中，可以在托管代码中编写标量值用户定义的函数。
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
ms.openlocfilehash: a44187fc41409d149501c4cda7e99817be034a12
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488414"
---
# <a name="clr-scalar-valued-functions"></a>CLR 标量值函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  标量值函数 (SVF) 返回单个值，例如字符串、整数或位值。 您可以使用任何 .NET Framework 编程语言在托管代码中创建标量值用户定义的函数。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他托管代码可访问这些函数。 有关 CLR 集成的优点以及托管代码和[!INCLUDE[tsql](../../includes/tsql-md.md)]之间的选择，请参阅[CLR 集成概述](../../relational-databases/clr-integration/clr-integration-overview.md)。  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>CLR 标量值函数的要求  
 在 .NET Framework 程序集中 .NET Framework  SVF 将实现为类的方法。 从 SVF 返回的输入参数和类型可以是 支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的任何标量数据类型，但**varchar、char、****char****行版本**、**文本****、ntext、****图像**、**时间戳**、**表**或**游标**除外。 SVF 必须确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和实现方法的返回数据类型相匹配。 有关类型转换的详细信息，请参阅[映射 CLR 参数数据](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。  
  
 在 .NET Framework 语言中实现 .NET 框架 SVF 时，可以指定**SqlFunction**自定义属性以包含有关该函数的其他信息。 **SqlFunction**属性指示函数是否访问或修改数据（如果是确定性数据），以及函数是否涉及浮点操作。  
  
 标量值用户定义函数可以是确定性函数也可以是不确定性函数。 如果使用一组特定的输入参数调用某个确定性函数，则该确定性函数始终返回相同的结果。 如果使用一组特定的输入参数调用某个不确定性函数，则该不确定性函数返回的结果可能会不同。  
  
> [!NOTE]  
>  在输入值相同且数据库状态相同的情况下，如果某函数并不总是产生相同的输出值，请不要将该函数标记为确定性函数。 如果函数不具备真正的确定性而将其标记为确定性函数，将可能产生损坏的索引视图和计算列。 通过将 **"确定"** 属性设置为 true，将函数标记为确定性。  
  
### <a name="table-valued-parameters"></a>表值参数  
 表值参数 (TVP) 即传递到某一过程或函数的用户定义表类型，它提供了一种将多行数据传递到服务器的高效方法。 TVP 提供与参数数组类似的功能，但灵活性更高并且与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成更紧密。 它们还提供提升性能的潜力。 TVP 还有助于减少到服务器的往返次数。 可以将数据作为 TVP 发送到服务器，而不是向服务器发送多个请求（例如，对于标量参数列表）。 用户定义表类型不能作为表值参数传递到在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中执行的托管存储过程或函数，也不能从这些存储过程或函数中返回。 有关 TVP 的详细信息，请参阅[使用表值参数&#40;数据库引擎&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
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
  
 第一行代码引用**Microsoft.SqlServer.Server.Server**访问属性和**系统.Data.SqlClient**以访问ADO.NET命名空间。 （此命名空间包含**SqlClient**，.NET 框架数据提供程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 接下来，该函数接收**SqlFunction**自定义属性，该属性位于**Microsoft.SqlServer.Server**命名空间中。 该自定义属性指示用户定义函数 (UDF) 是否使用进程内访问接口来读取服务器中的数据。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许 UDF 更新、插入或删除数据。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以优化执行不使用进程内访问接口的 UDF。 这是通过设置**数据访问金德****数据访问金指示的。** 在下一行中，目标方法为公共静态方法（在 Visual Basic .NET 中为 shared）。  
  
 **SqlContext**类位于**Microsoft.SqlServer.Server.Server**命名空间中，然后可以访问**SqlCommand**对象，该对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与已设置的实例连接。 虽然此处未使用，但当前事务上下文也可通过**System.事务**应用程序编程接口 （API） 获得。  
  
 函数体中的大多数代码行应该看起来熟悉那些编写了使用**System.Data.SqlClient**命名空间中找到类型的客户端应用程序的开发人员。  
  
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
  
 通过初始化**SqlCommand**对象指定相应的命令文本。 前面的示例计算表**SalesOrderHeader**中的行数。 接下来，调用**cmd**对象的**ExecuteScalar**方法。 这将返回基于查询的类型**int**的值。 最后，将订单计数返回给调用方。  
  
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
>  使用 **/clr：pure**编译的可视C++数据库对象不支持在 上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行。 例如，此类数据库对象包含标量值函数。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [映射 CLR 参数数据](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [CLR 集成自定义属性概述](https://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)   
 [用户定义的函数](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 [从 CLR 数据库对象进行数据访问](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
