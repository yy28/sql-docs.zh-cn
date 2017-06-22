---
title: "在 SQL Server 和客户端应用中使用 FOR JSON 输出 (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, using in client apps
- FOR JSON, using in SQL Server
ms.assetid: 302e5397-b499-4ea3-9a7f-c24ccad698eb
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 9383b62ac3413b0e4dc8780413bdde09bfc04af3
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="use-for-json-output-in-sql-server-and-in-client-apps-sql-server"></a>在 SQL Server 和客户端应用中使用 FOR JSON 输出 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

下面的示例演示了几种用于**FOR JSON**子句和其 JSON 输出中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或客户端应用中。  
  
## <a name="use-for-json-output-in-sql-server-variables"></a>在 SQL Server 变量中使用 FOR JSON 输出  
FOR JSON 子句的输出类型 nvarchar (MAX)，因此可以分配给任何变量，如下面的示例中所示。  
  
```sql  
DECLARE @x NVARCHAR(MAX) = (SELECT TOP 10 * FROM Sales.SalesOrderHeader FOR JSON AUTO)  
```  
  
## <a name="use-for-json-output-in-sql-server-user-defined-functions"></a>在 SQL Server 用户定义函数中使用 FOR JSON 输出  
 你可以创建将结果集格式化为 JSON 并返回此 JSON 输出的用户定义函数。 下面的示例创建一个用户定义函数，该函数提取一些销售订单详细信息行，并将它们格式化为 JSON 数组。  
  
```sql  
CREATE FUNCTION GetSalesOrderDetails(@salesOrderId int)  
 RETURNS NVARCHAR(MAX)  
AS  
BEGIN  
   RETURN (SELECT UnitPrice, OrderQty  
           FROM Sales.SalesOrderDetail  
           WHERE SalesOrderID = @salesOrderId  
           FOR JSON AUTO)  
END
```  
  
 你可以在批或查询中使用此函数，如下面的示例中所示。  
  
```sql  
DECLARE @x NVARCHAR(MAX) = dbo.GetSalesOrderDetails(43659)

PRINT dbo.GetSalesOrderDetails(43659)

SELECT TOP 10
  H.*, dbo.GetSalesOrderDetails(H.SalesOrderId) AS Details
FROM Sales.SalesOrderHeader H
```  
  
## <a name="merge-parent-and-child-data-into-a-single-table"></a>将父数据和子数据合并到单个表中  
在下面的示例中，每个组子行将格式化为 JSON 数组。 JSON 数组将成为父表中的详细信息列的值。  
  
```sql  
SELECT TOP 10 SalesOrderId, OrderDate,  
      (SELECT TOP 3 UnitPrice, OrderQty  
         FROM Sales.SalesOrderDetail D  
         WHERE H.SalesOrderId = D.SalesOrderID  
         FOR JSON AUTO) AS Details  
INTO SalesOrder  
FROM Sales.SalesOrderHeader H  
```  
  
## <a name="update-the-data-in-json-columns"></a>更新 JSON 列中的数据  
 下面的示例演示你可以更新包含 JSON 文本的列的值。  
  
```sql  
UPDATE SalesOrder  
SET Details =  
     (SELECT TOP 1 UnitPrice, OrderQty  
       FROM Sales.SalesOrderDetail D  
       WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
      FOR JSON AUTO 
```  
  
## <a name="use-for-json-output-in-a-c-client-app"></a>在 C# 客户端应用中使用 FOR JSON 输出  
 下面的示例演示如何在 C# 客户端应用中将查询的 JSON 输出检索到 StringBuilder 对象中。 假定变量`queryWithForJson`包含带有 FOR JSON 子句的 SELECT 语句的文本。  
  
```csharp  
var queryWithForJson = "SELECT ... FOR JSON";
var conn = new SqlConnection("<connection string>");
var cmd = new SqlCommand(queryWithForJson, conn);
conn.Open();
var jsonResult = new StringBuilder();
var reader = cmd.ExecuteReader();
if (!reader.HasRows)
{
    jsonResult.Append("[]");
}
else
{
    while (reader.Read())
    {
        jsonResult.Append(reader.GetValue(0).ToString());
    }
}
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。
 
## <a name="see-also"></a>另请参阅  
 [借助 FOR JSON 将查询结果的格式设置为 JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  

