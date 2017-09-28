---
title: "其中 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WHERE_TSQL
- WHERE
dev_langs:
- TSQL
helpviewer_keywords:
- retrieving rows
- clauses [SQL Server], WHERE
- WHERE clause, about WHERE clause
- row retrieval [SQL Server], WHERE clause
- WHERE clause
ms.assetid: a8430421-7bce-4fab-a2d2-56c00a3c6fa4
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5835510f37f52d57d2c23918a30dde10e7496a5d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="where-transact-sql"></a>WHERE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定查询返回的行的搜索条件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
[ WHERE <search_condition> ]  
```  
  
## <a name="arguments"></a>参数  
\<*search_condition* > 用于定义要返回的行，需满足的条件。 对搜索条件中可以包含的谓词数量没有限制。 有关搜索条件和谓词的详细信息，请参阅[搜索条件 &#40;Transact SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
## <a name="examples"></a>示例  
 下面的示例演示如何在 `WHERE` 子句中使用某些常见的搜索条件。  
  
### <a name="a-finding-a-row-by-using-a-simple-equality"></a>A. 使用简单等式查找行  
  
```  
USE AdventureWorks2012  
GO  
SELECT ProductID, Name  
FROM Production.Product  
WHERE Name = 'Blade' ;  
GO  
```  
  
### <a name="b-finding-rows-that-contain-a-value-as-a-part-of-a-string"></a>B. 查找包含作为字符串一部分的值的行  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE Name LIKE ('%Frame%');  
GO  
```  
  
### <a name="c-finding-rows-by-using-a-comparison-operator"></a>C. 使用比较运算符查找行  
  
```  
SELECT ProductID, Name  
FROM Production.Product  
WHERE ProductID <= 12 ;  
GO  
```  
  
### <a name="d-finding-rows-that-meet-any-of-three-conditions"></a>D. 查找满足三个条件当中的任何一个条件的行  
  
```  
SELECT ProductID, Name  
FROM Production.Product  
WHERE ProductID = 2  
OR ProductID = 4   
OR Name = 'Spokes' ;  
GO  
```  
  
### <a name="e-finding-rows-that-must-meet-several-conditions"></a>E. 查找必须满足若干个条件的行  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE Name LIKE ('%Frame%')  
AND Name LIKE ('HL%')  
AND Color = 'Red' ;  
GO  
```  
  
### <a name="f-finding-rows-that-are-in-a-list-of-values"></a>F. 查找位于值列表中的行  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE Name IN ('Blade', 'Crown Race', 'Spokes');  
GO  
```  
  
### <a name="g-finding-rows-that-have-a-value-between-two-values"></a>G. 查找含有两个值之间的一个值的行  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE ProductID BETWEEN 725 AND 734;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例演示如何在 `WHERE` 子句中使用某些常见的搜索条件。  
  
### <a name="h-finding-a-row-by-using-a-simple-equality"></a>H. 使用简单等式查找行  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName = 'Smith' ;  
```  
  
### <a name="i-finding-rows-that-contain-a-value-as-part-of-a-string"></a>I. 查找作为字符串的一部分包含的值的行  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE ('%Smi%');  
```  
  
### <a name="j-finding-rows-by-using-a-comparison-operator"></a>J. 使用比较运算符查找行  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey  <= 500;  
```  
  
### <a name="k-finding-rows-that-meet-any-of-three-conditions"></a>K. 查找满足三个条件当中的任何一个条件的行  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey = 1 OR EmployeeKey = 8 OR EmployeeKey = 12;  
```  
  
### <a name="l-finding-rows-that-must-meet-several-conditions"></a>L. 查找必须满足若干个条件的行  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey <= 500 AND LastName LIKE '%Smi%' AND FirstName LIKE '%A%';  
```  
  
### <a name="m-finding-rows-that-are-in-a-list-of-values"></a>M. 查找位于值列表中的行  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName IN ('Smith', 'Godfrey', 'Johnson');  
```  
  
### <a name="n-finding-rows-that-have-a-value-between-two-values"></a>N. 查找含有两个值之间的一个值的行  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey Between 100 AND 200;  
```  
  
## <a name="see-also"></a>另请参阅  
 [DELETE (Transact-SQL)](../../t-sql/statements/delete-transact-sql.md)   
 [谓词 &#40;Transact SQL &#41;](~/t-sql/queries/predicates.md)   
 [搜索条件 &#40;Transact SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [MERGE (Transact-SQL)](../../t-sql/statements/merge-transact-sql.md)  
  
  



