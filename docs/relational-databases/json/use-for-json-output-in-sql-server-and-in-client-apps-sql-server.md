---
title: "在 SQL Server 和客户端应用中使用 FOR JSON 输出 (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR JSON, 在客户端应用中使用"
  - "FOR JSON, 在 SQL Server 中使用"
ms.assetid: 302e5397-b499-4ea3-9a7f-c24ccad698eb
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# 在 SQL Server 和客户端应用中使用 FOR JSON 输出 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  下面的示例演示了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或客户端应用中使用 **FOR JSON** 子句或其输出的几种方式。  
  
## 在 SQL Server 变量中使用 FOR JSON 输出  
 FOR JSON 子句的输出类型为 NVARCHAR(MAX)，因此可以将它赋给任何变量，如下面的示例中所示。  
  
```tsql  
DECLARE @x NVARCHAR(MAX) = (SELECT TOP 10 * FROM Sales.SalesOrderHeader FOR JSON AUTO)  
```  
  
## 在 SQL Server 用户定义函数中使用 FOR JSON 输出  
 你可以创建将结果集格式化为 JSON 并返回此 JSON 输出的用户定义函数。 下面的示例创建一个用户定义函数，该函数提取一些销售订单详细信息行，并将它们格式化为 JSON 数组。  
  
```tsql  
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
  
```tsql  
DECLARE @x NVARCHAR(MAX) = dbo.GetSalesOrderDetails(43659)  
PRINT dbo.GetSalesOrderDetails(43659)  
SELECT TOP 10 H.*, dbo.GetSalesOrderDetails(H.SalesOrderId) AS Details  
FROM Sales.SalesOrderHeader H  
```  
  
## 将父数据和子数据合并到单个表中  
 在下面的示例中，每一组子行将格式化为 JSON 数组，并且变成父表中“详细信息”列的值。  
  
```tsql  
select top 10 SalesOrderId, OrderDate,  
     (select top 3 UnitPrice, OrderQty  
        from Sales.SalesOrderDetail D  
        where H.SalesOrderId = D.SalesOrderID  
        for json auto) as Details  
into SalesOrder  
from Sales.SalesOrderHeader H  
```  
  
## 更新 JSON 列中的数据  
 下面的示例演示你可以更新包含 JSON 文本的列的值。  
  
```tsql  
UPDATE SalesOrder  
SET Details =  
    (SELECT TOP 1 UnitPrice, OrderQty  
      FROM Sales.SalesOrderDetail D  
      WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
     FOR JSON AUTO)  
```  
  
## 在 C# 客户端应用中使用 FOR JSON 输出  
 下面的示例演示如何在 C# 客户端应用中将查询的 JSON 输出检索到 StringBuilder 对象中。 假设变量 queryWithForJson 包含带有 FOR JSON 子句的 SELECT 语句的文本。  
  
```csharp  
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
  
## 另请参阅  
 [借助 FOR JSON 将查询结果的格式设置为 JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  