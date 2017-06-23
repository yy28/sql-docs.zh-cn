---
title: "在 AUTO 模式下自动格式化 JSON 输出 (SQL Server) | Microsoft Docs"
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
- FOR JSON AUTO
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: cba250a399bb3de87c9713ac600c9807527a1cd9
ms.contentlocale: zh-cn
ms.lasthandoff: 06/23/2017

---
# <a name="format-json-output-automatically-with-auto-mode-sql-server"></a>在 AUTO 模式下自动格式化 JSON 输出 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

若要根据 **SELECT** 语句的结构自动格式化 **FOR JSON** 子句的输出，请指定 **AUTO** 选项。  
  
使用 **AUTO** 选项时，可根据 SELECT 列表及其源表中的列顺序自动确定 JSON 输出的格式。 无法更改此格式。
 
 替代方法是使用 **PATH** 选项维持对输出的控制。
 -   有关 **PATH** 选项的详细信息，请参阅[在 PATH 模式下格式化嵌套 JSON 输出](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md)。
 -   有关这两个选项的概述，请参阅[使用 FOR JSON 将查询结果格式化为 JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)。
  
 使用 **FOR JSON AUTO** 选项的查询必须具有 **FROM** 子句。  
  
 下面的一些示例展示了如何使用 **AUTO** 选项指定 **FOR JSON** 子句。  
  
## <a name="examples"></a>示例  
 **查询 1**  
  
如果查询中仅使用了一个表，则 FOR JSON AUTO 子句的结果类似于 FOR JSON PATH 的结果。 在这种情况下，FOR JSON AUTO 不会创建嵌套对象。 唯一的区别是 FOR JSON AUTO 会将以点分隔的别名（例如以下示例中的 `Info.MiddleName`）输出为带有点的键，而不是输出为嵌套对象。  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON AUTO  
```  
  
 **结果 1**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sánchez",
    "Info.MiddleName": "J"
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info.MiddleName": "Lee"
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
    "Info.Title": "Ms.",
    "Info.MiddleName": "A"
}]
```  
  
 **查询 2**  
  
 联接表时，第一个表中的列会作为根对象的属性生成。 第二个表中的列会作为嵌套对象的属性生成。 第二个表的表名或别名（例如以下示例中的 `D`）用作嵌套数组的名称。  
  
```sql  
SELECT TOP 2 SalesOrderNumber,  
        OrderDate,  
        UnitPrice,  
        OrderQty  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON AUTO   
```  
  
 **结果 2**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO43659",
    "D": [{
        "UnitPrice": 34.40
    }, {
        "UnitPrice": 134.24,
        "OrderQty": 5
    }]
}]
```  
 
 **查询 3**  
 你可以在 SELECT 语句中嵌套 FOR JSON PATH 子查询，而不使用 FOR JSON AUTO，如以下示例中所示。 此示例输出与上一示例相同的结果。  
  
```sql  
SELECT TOP 2  
    SalesOrderNumber,  
    OrderDate,  
    (SELECT UnitPrice, OrderQty  
      FROM Sales.SalesOrderDetail AS D  
      WHERE H.SalesOrderID = D.SalesOrderID  
     FOR JSON PATH) AS D  
FROM Sales.SalesOrderHeader AS H  
FOR JSON PATH  
```  
  
 **结果 3**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO4390",
    "D": [{
        "UnitPrice": 24.99
    }]
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。

## <a name="see-also"></a>另请参阅  
 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)  

