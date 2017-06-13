---
title: "使用内置函数验证、查询和更改 JSON 数据 (SQL Server) | Microsoft Docs"
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
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: e2b7d75694080b52e9c31e58ffd1e1f738b1035c
ms.contentlocale: zh-cn
ms.lasthandoff: 06/09/2017

---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>使用内置函数 (SQL Server) 验证、查询和更改 JSON 数据
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  JSON 的内置支持包括本主题所述的下列内置函数。  
  
-   [ISJSON](#ISJSON) 测试字符串是否包含有效 JSON。  
  
-   [JSON_VALUE](#VALUE) 从 JSON 字符串中提取标量值。  
  
-   [JSON_QUERY](#QUERY) 从 JSON 字符串中提取对象或数组。  
  
-   [JSON_MODIFY](#MODIFY) 更新 JSON 字符串中属性的值，并返回已更新的 JSON 字符串。  
 
## <a name="json-text-for-the-examples-on-this-page"></a>此页上的示例 JSON 文本
此页上的示例使用以下包含复杂元素的 JSON 文本。

```json  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }' 
``` 

##  <a name="ISJSON"></a> 使用 ISJSON 函数验证 JSON 文本  
 **ISJSON** 函数测试字符串是否包含有效 JSON。  
  
 如果列包含有效 JSON，则下面的示例将返回 JSON 文本。  
  
```sql  
SELECT id,json_col
FROM tab1
WHERE ISJSON(json_col)>0 
```  
  
 有关详细信息，请参阅 [ISJSON (Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md)。  
  
##  <a name="VALUE"></a> 使用 JSON_VALUE 函数从 JSON 文本中提取值  
 **JSON_VALUE** 函数从 JSON 字符串中提取标量值。  
  
 下面的示例将 JSON 属性的值提取到本地变量。  
  
```sql  
SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')  
```  
  
 有关详细信息，请参阅 [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)。  
  
##  <a name="QUERY"></a> 使用 JSON_QUERY 函数从 JSON 文本中提取对象或数组  
 **JSON_QUERY** 函数从 JSON 字符串中提取对象或数组。  
 
 下面的示例演示了如何在查询结果中返回 JSON 片段。  
  
```sql  
SELECT FirstName,LastName,JSON_QUERY(jsonInfo,'$.info.address') AS Address
FROM Person.Person
ORDER BY LastName
```  
  
 有关详细信息，请参阅 [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)。  
  
##  <a name="JSONCompare"></a> 对比 JSON_VALUE 与 JSON_QUERY  
 **JSON_VALUE** 和 **JSON_QUERY** 之间的主要区别在于 **JSON_VALUE** 返回标量值，而 **JSON_QUERY** 返回数组或对象。  
  
 请参考以下示例 JSON 文本。  
  
```json  
{
    "a": "[1,2]",
    "b": [1, 2],
    "c": "hi"
}  
```  
  
 在此示例 JSON 文本中，数据成员“a”和“c”是字符串值，而数据成员“b”是数组。 **JSON_VALUE** 和 **JSON_QUERY** 返回以下结果：  
  
|Query|**JSON_VALUE** 返回|**JSON_QUERY** 返回|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL 或错误|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL 或错误|  
|**$.b**|NULL 或错误|[1,2]|  
|**$.b[0]**|1|NULL 或错误|  
|**$.c**|hi|NULL 或错误|  
  
## <a name="test-jsonvalue-and-jsonquery-with-the-adventureworks-sample-database"></a>使用 AdventureWorks 示例数据库测试 JSON_VALUE 和 JSON_QUERY  
 通过使用包含 JSON 数据的 AdventureWorks 示例数据库运行以下示例，对本主题中所述的内置函数进行测试。 若要获取 AdventureWorks 示例数据库， [请单击此处](http://www.microsoft.com/en-us/download/details.aspx?id=49502)。  
  
 在下面的示例中，SalesOrder_json 表中的 Info 列包含了 JSON 文本。  
  
### <a name="example-1---return-both-standard-columns-and-json-data"></a>示例 1 - 返回标准列和 JSON 数据  
 下面的查询返回将返回标准关系列以及 JSON 列的值。  
  
```sql  
SELECT SalesOrderNumber,OrderDate,Status,ShipDate,Status,AccountNumber,TotalDue,
 JSON_QUERY(Info,'$.ShippingInfo') ShippingInfo,
 JSON_QUERY(Info,'$.BillingInfo') BillingInfo,
 JSON_VALUE(Info,'$.SalesPerson.Name') SalesPerson,
 JSON_VALUE(Info,'$.ShippingInfo.City') City,
 JSON_VALUE(Info,'$.Customer.Name') Customer,
 JSON_QUERY(OrderItems,'$') OrderItems
FROM Sales.SalesOrder_json
WHERE ISJSON(Info)>0
```  
  
### <a name="example-2--aggregate-and-filter-json-values"></a>示例 2 - 聚合和筛选 JSON 值  
 下面的查询将按客户名称（存储在 JSON 中）和状态（存储在普通列中）来汇总小计。 然后将按市/县（存储在 JSON 中）和 OrderDate（存储在普通列中）来筛选结果。  
  
```sql  
DECLARE @territoryid INT;
DECLARE @city NVARCHAR(32);

SET @territoryid=3;

SET @city=N'Seattle';

SELECT JSON_VALUE(Info,'$.Customer.Name') AS Customer,Status,SUM(SubTotal) AS Total
FROM Sales.SalesOrder_json
WHERE TerritoryID=@territoryid
 AND JSON_VALUE(Info,'$.ShippingInfo.City')=@city
 AND OrderDate>'1/1/2015'
GROUP BY JSON_VALUE(Info,'$.Customer.Name'),Status
HAVING SUM(SubTotal)>1000
```  
  
##  <a name="MODIFY"></a> 使用 JSON_MODIFY 函数更新 JSON 文本中的属性值  
 **JSON_MODIFY**  函数更新 JSON 字符串中属性的值，并返回已更新的 JSON 字符串。  
  
 以下示例将更新包含 JSON 的变量中的属性的值。  
  
```sql  
SET @info=JSON_MODIFY(@jsonInfo,"$.info.address[0].town",'London')    
```  
  
 有关详细信息，请参阅 [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md)。  
  
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。
  
## <a name="see-also"></a>另请参阅  
 [ISJSON (Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md)   
 [JSON 路径表达式 (SQL Server)](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  

