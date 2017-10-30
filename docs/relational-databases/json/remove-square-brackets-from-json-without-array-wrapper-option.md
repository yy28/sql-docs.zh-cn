---
title: "从 JSON 中删除方括号 - WITHOUT_ARRAY_WRAPPER 选项 | Microsoft Docs"
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
- WITHOUT_ARRAY_WRAPPER
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: bf0d7645df22c9a7540650e3c7f2ca2d0db8e1cc
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>从 JSON 中删除方括号 - WITHOUT_ARRAY_WRAPPER 选项
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

若要删除默认括住 **FOR JSON** 子句的 JSON 输出的方括号，请指定 **WITHOUT_ARRAY_WRAPPER** 选项。 将此选项用于单行结果，生成单个 JSON 对象作为输出，而不是生成具有单个元素的数组。

如果将此选项用于多行结果，生成的输出将不会是有效的 JSON，因为存在多个元素并且缺少方括号。  
  
## <a name="example-single-row-result"></a>示例（单行结果）  
以下示例介绍了在指定和未指定 **WITHOUT_ARRAY_WRAPPER** 选项的情况下 **FOR JSON** 子句的输出。  
  
 **Query**  
  
```sql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  

 指定**结果** with the **结果**   
  
```json  
{
    "year": 2015,
    "month": 12,
    "day": 15
} 
```  
  
 未指定 WITHOUT_ARRAY_WRAPPER 选项的结果（默认）  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  

## <a name="example-multiple-row-result"></a>示例（多行结果）
下面又通过一个示例介绍了在指定 **FOR JSON** 选项的情况下 **WITHOUT_ARRAY_WRAPPER** 选项。 本示例生成多行结果。 输出不是有效的 JSON，因为存在多个元素并且缺少方括号。
  
 **Query**  
  
```sql  
SELECT TOP 3 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 指定**结果** with the **结果**   
  
```json  
{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 未指定 WITHOUT_ARRAY_WRAPPER 选项的结果（默认）  
  
```json  
[{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解 SQL Server 中内置 JSON 支持的详细信息  
若要获取大量特定解决方案、用例和建议，请参阅 Microsoft 项目经理 Jovan Popovic 发表的 SQL Server 和 Azure SQL 数据库中的[内置 JSON 支持相关博客文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)。
  
## <a name="see-also"></a>另请参阅  
 [FOR 子句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

