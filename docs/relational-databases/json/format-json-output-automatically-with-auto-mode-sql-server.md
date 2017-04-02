---
title: "在 AUTO 模式下自动格式化 JSON 输出 (SQL Server) | Microsoft Docs"
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
  - "FOR JSON AUTO"
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 15
---
# 在 AUTO 模式下自动格式化 JSON 输出 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  要根据 **SELECT** 语句的结构自动格式化 JSON 输出，请使用  **FOR JSON** 子句指定 **AUTO** 选项。  
  
 使用 **AUTO** 选项时，可根据 SELECT 列表及其源表中的列顺序自动确定 JSON 输出的格式。 无法更改此格式。  
  
 使用 **FOR JSON AUTO** 选项的查询必须具有 **FROM** 子句。  
  
 下面的一些示例展示了如何使用 **AUTO** 选项指定 **FOR JSON** 子句。  
  
## 示例  
 **查询 1**  
  
 如果只在查询中使用一个表，则 FOR JSON PATH 子句和 FOR JSON AUTO 子句的结果相似。 在这种情况下，FOR JSON AUTO 将不会创建嵌套对象。 唯一的区别是，将生成以点分隔的别名，就像以点分隔的密钥一样（即 FOR JSON AUTO 将不使用列别名格式）。  
  
```tsql  
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
[  
      {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info.MiddleName":"J"},  
      {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info.MiddleName":"Lee"},  
      {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
      {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
      {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info.Title":"Ms.","Info.MiddleName":"A"}  
]  
```  
  
 **查询 2**  
  
 联接表时，第一个表中的列会作为根对象的属性生成。 第二个表中的列会作为嵌套对象的属性生成。 第二个表的表名或别名将用作嵌套数组的名称。  
  
```tsql  
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
[  
  {  
       "SalesOrderNumber":"SO43659",  
        "OrderDate":"2011-05-31T00:00:00",  
        "D":[  
            {"UnitPrice":24.99, "OrderQty":1  }  
         ]  
  },  
  {  
       "SalesOrderNumber":"SO43659" ,  
       "D":[  
          { "UnitPrice":34.40  },  
          { "UnitPrice":134.24, "OrderQty":5 }  
        ]  
  }  
]  
  
```  
  
## 示例 - 生成嵌套 JSON 输出  
 与 FOR JSON AUTO 不同，你可以编写嵌套 FOR JSON 查询，该查询位于附带 FOR JSON PATH 子句的主查询中的 SELECT 部分，如下例所示。  
  
 **查询 1**  
  
```tsql  
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
  
 **结果 1**  
  
```json  
[  
  {  
       "SalesOrderNumber":"SO43659",  
        "OrderDate":"2011-05-31T00:00:00",  
        "D":[  
            { "UnitPrice":24.99,  "OrderQty":1 }  
         ]  
  },  
  {  
       "SalesOrderNumber":"SO4390" ,  
       "D":[  
            { "UnitPrice":24.99 }  
        ]  
  }  
]  
  
```  
  
## 另请参阅  
 [FOR 子句 (Transact-SQL)](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  