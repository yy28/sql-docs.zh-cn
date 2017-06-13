---
title: "在 PATH 模式下格式化嵌套 JSON 输出 (SQL Server) | Microsoft Docs"
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
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 3a11cee5097ed686d20d3bb8fcc7894138700841
ms.contentlocale: zh-cn
ms.lasthandoff: 06/09/2017

---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>在 PATH 模式下格式化嵌套 JSON 输出 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  若要维持对 **FOR JSON** 子句的输出的完全控制，请指定 **PATH** 选项。  
  
 借助**PATH** 模式，你可以创建包装器对象，并嵌套复杂属性。 结果的格式设置为 JSON 对象的数组。  
  
替代方法是使用 **AUTO** 选项根据 **SELECT** 语句的结构自动格式化输出。
 -   有关 **AUTO** 选项的详细信息，请参阅[在 AUTO 模式下自动格式化 JSON 输出 (SQL Server)](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)。
 -   有关这两个选项的概述，请参阅[使用 FOR JSON 将查询结果格式化为 JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)。
 
下面的一些示例展示了如何使用 **PATH** 选项指定 **FOR JSON** 子句。 使用以点分隔的列名称或使用嵌套查询来格式化嵌套结果，如下面的示例所示。 默认情况下，**FOR JSON** 输出中不包括 null 值。  

## <a name="example---dot-separated-column-names"></a>示例 - 以点分隔的列名称  
 以下查询将 AdventureWorks Person 表的前五行格式化为 JSON。  

FOR JSON PATH 子句使用列别名或列名来确定 JSON 输出中的键名称。 如果别名中包含点，则 PATH 选项将创建嵌套对象。  

 **查询**  
  
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
    "LastName": "Sánchez",
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
 如果查询中引用了多个表，则 FOR JSON PATH 将使用列的别名嵌套每个列。 以下查询将为查询中联接的每个（OrderHeader，OrderDetails）对创建一个 JSON 对象。 
  
 **查询**  
  
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

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。

## <a name="see-also"></a>另请参阅  
 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)  

