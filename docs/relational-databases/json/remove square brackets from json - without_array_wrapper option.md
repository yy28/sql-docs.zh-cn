---
title: "使用 WITHOUT_ARRAY_WRAPPER 选项 (SQL Server) 从 JSON 输出中删除方括号 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WITHOUT_ARRAY_WRAPPER"
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# 使用 WITHOUT_ARRAY_WRAPPER 选项 (SQL Server) 从 JSON 输出中删除方括号
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  若要删除默认括住 **FOR JSON** 子句的 JSON 输出的方括号，请指定 **WITHOUT_ARRAY_WRAPPER** 选项。 使用此选项可以生成单个 JSON 对象作为输出。  
  
 如果不指定此选项，JSON 输出将括在方括号中。  
  
## 示例  
 以下示例介绍了在指定和未指定 **WITHOUT_ARRAY_WRAPPER** 选项的情况下 **FOR JSON** 子句的输出。  
  
 **Query**  
  
```tsql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER  
```  
  
 指定 **WITHOUT_ARRAY_WRAPPER** 选项的**结果**  
  
```json  
{ "year":2015, "month":12, "day":15 }  
```  
  
 未指定 **WITHOUT_ARRAY_WRAPPER** 选项的**结果**  
  
```json  
[ { "year":2015, "month":12, "day":15 } ]  
```  
  
 下面又通过一个示例介绍了在指定 **WITHOUT_ARRAY_WRAPPER** 选项的情况下 **FOR JSON** 子句的输出。  
  
 **Query**  
  
```tsql  
SELECT TOP 1 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER  
```  
  
 指定 **WITHOUT_ARRAY_WRAPPER** 选项的**结果**  
  
```json  
{  
    "SalesOrderNumber":"SO43660",  
    "OrderDate":"2011-05-31T00:00:00",  
    "Status":5  
}  
```  
  
 未指定 **WITHOUT_ARRAY_WRAPPER** 选项的**结果**  
  
```json  
[  
    {  
        "SalesOrderNumber":"SO43660",  
        "OrderDate":"2011-05-31T00:00:00",  
        "Status":5  
    }  
]  
```  
  
## 另请参阅  
 [FOR 子句 (Transact-SQL)](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  