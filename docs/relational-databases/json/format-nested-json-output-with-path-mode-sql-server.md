---
title: "在 PATH 模式下格式化嵌套 JSON 输出 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b1ae801441cdd683f32d36cccd859ecb21ba7198
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>在 PATH 模式下格式化嵌套 JSON 输出 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

若要保持对 FOR JSON 子句输出的完全控制，请指定 PATH 选项。  
  
借助**PATH** 模式，你可以创建包装器对象，并嵌套复杂属性。 结果会格式化为 JSON 对象数组。  
  
替代方法是使用 AUTO 选项根据 SELECT 语句的结构自动格式化输出。
 -   有关 AUTO 选项的详细信息，请参阅[在 AUTO 模式下自动格式化 JSON 输出](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)。
 -   有关这两个选项的概述，请参阅[使用 FOR JSON 将查询结果格式化为 JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)。
 
下面的一些示例展示了如何使用 **PATH** 选项指定 **FOR JSON** 子句。 使用以点分隔的列名称或使用嵌套查询来格式化嵌套结果，如下面的示例所示。 默认情况下，FOR JSON 输出中不包括 null 值。  

## <a name="example---dot-separated-column-names"></a>示例 - 以点分隔的列名称  
以下查询将 AdventureWorks `Person` 表的前五行格式化为 JSON。  

FOR JSON PATH 子句使用列别名或列名来确定 JSON 输出中的键名称。 如果别名中包含点，则 PATH 选项将创建嵌套对象。  

 **Query**  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON PATH   
```  
  
 **结果**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sanchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  
   
## <a name="example---multiple-tables"></a>示例 - 多个表  
如果查询中引用了多个表，FOR JSON PATH 将使用列别名嵌套每个列。 以下查询将为查询中联接的每个（OrderHeader，OrderDetails）对创建一个 JSON 对象。 
  
 **Query**  
  
```sql  
SELECT TOP 2 SalesOrderNumber AS 'Order.Number',  
        OrderDate AS 'Order.Date',  
        UnitPrice AS 'Product.Price',  
        OrderQty AS 'Product.Quantity'  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON PATH   
```  
  
 **结果**  
  
```json  
[{
    "Order": {
        "Number": "SO43659",
        "Date": "2011-05-31T00:00:00"
    },
    "Product": {
        "Price": 2024.9940,
        "Quantity": 1
    }
}, {
    "Order": {
        "Number": "SO43659"
    },
    "Product": {
        "Price": 2024.9940
    }
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解 SQL Server 中内置 JSON 支持的详细信息  
若要获取大量特定解决方案、用例和建议，请参阅 Microsoft 项目经理 Jovan Popovic 发表的 SQL Server 和 Azure SQL 数据库中的[内置 JSON 支持相关博客文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)。

## <a name="see-also"></a>另请参阅  
 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)  
