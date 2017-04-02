---
title: "在 PATH 模式下格式化嵌套 JSON 输出 (SQL Server) | Microsoft Docs"
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
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# 在 PATH 模式下格式化嵌套 JSON 输出 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  若要维持对 JSON 输出格式的完全控制，请使用 **FOR JSON** 子句指定 **PATH** 选项。  
  
 借助**PATH** 模式，你可以创建包装器对象，并嵌套复杂属性。 结果会格式化为 JSON 对象数组。  
  
 下面的一些示例展示了如何使用 **PATH** 选项指定 **FOR JSON** 子句。 使用以点分隔的列名称或使用嵌套查询来格式化嵌套结果，如下面的示例所示。 默认情况下，输出中不包括 NULL 值。  
  
## 示例 - 以点分隔的列名称  
 以下查询将 AdventureWorks Person 表的前五行格式化为 JSON。  
  
 **Query**  
  
```tsql  
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
[  
    {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info":{"MiddleName":"J"}},  
    {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info":{"MiddleName":"Lee"}},  
    {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
    {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
    {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info":{"Title":"Ms.","MiddleName":"A"}}  
]  
```  
  
 FOR JSON PATH 子句将使用列别名或列名来确定 JSON 输出中的密钥名称。 如果某些别名包含点，FOR JSON PATH 子句将创建嵌套对象。 请注意，输出中将不生成具有 NULL 值的单元格。  
  
## 示例 - 多个表  
 如果查询中引用多个表，结果将呈现在一个平面列表中，然后 FOR JSON PATH 会使用其别名嵌套每一列。 以下查询将为加入查询的每个 (OrderHeader，OrderDetails) 对创建一个 JSON 对象：  
  
 **Query**  
  
```tsql  
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
[  
  {  
    "Order":{  
        "Number":"SO43659",  
        "Date":"2011-05-31T00:00:00"  
      },  
    "Product":{  
         "Price":2024.9940,  
         "Quantity":1  
     }  
  },  
  {  
    "Order":{ "Number":"SO43659“ },  
    "Product":{"Price":2024.9940}  
  }  
]  
```  
  
## 另请参阅  
 [FOR 子句 (Transact-SQL)](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  