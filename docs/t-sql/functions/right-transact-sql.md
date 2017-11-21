---
title: "右 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RIGHT_TSQL
- RIGHT
dev_langs:
- TSQL
helpviewer_keywords:
- rightmost character of expression
- RIGHT function
- character strings [SQL Server], RIGHT
ms.assetid: 43f1fe1f-aa18-47e3-ba20-e03e32254a6d
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 19dcdea078648b6ff41e08fcf82c9a4c705abe4c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="right-transact-sql"></a>RIGHT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回字符串中从右边开始指定个数的字符。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
RIGHT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)字符或二进制数据。 *character_expression*可以是常量、 变量或列。 *character_expression*可以是任何数据类型，除**文本**或**ntext**，可以隐式转换为**varchar**或**nvarchar**。 否则，请使用[强制转换](../../t-sql/functions/cast-and-convert-transact-sql.md)函数可以显式转换*character_expression*。  
  
 *integer_expression*  
 是一个正整数，指定的多少个字符*character_expression*将返回。 如果*integer_expression*为负，则返回一个错误。 如果*integer_expression*是类型**bigint**和包含较大的值， *character_expression*必须是较大的数据类型的如**varchar （max)**.  
  
## <a name="return-types"></a>返回类型  
 返回**varchar**时*character_expression*是非 Unicode 字符数据类型。  
  
 返回**nvarchar**时*character_expression*是 Unicode 字符数据类型。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>补充字符（代理项对）  
 在使用 SC 排序规则时，RIGHT 函数将 UTF-16 代理项对计为一个字符。 有关详细信息，请参阅 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-right-with-a-column"></a>答： 使用列权限  
 以下示例返回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中每个联系人名字中最右边的五个字符。  
  
```  
SELECT RIGHT(FirstName, 5) AS 'First Name'  
FROM Person.Person  
WHERE BusinessEntityID < 5  
ORDER BY FirstName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
First Name  
----------  
Ken  
Terri  
berto  
Rob  
  
(4 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-right-with-a-column"></a>B. 使用列的权限  
 下面的示例返回每个中的最后一个名称的五个最右边字符`DimEmployee`表。  
  
```  
-- Uses AdventureWorks  
  
SELECT RIGHT(LastName, 5) AS Name  
FROM dbo.DimEmployee  
ORDER BY EmployeeKey;  
```  
  
 以下为部分结果集。  
  
 ```
Name
-----
lbert
Brown
rello
lters
 ```  
  
### <a name="c-using-right-with-a-character-string"></a>C. 字符字符串，使用权限  
 下面的示例使用`RIGHT`要返回的字符字符串的两个最右边字符`abcdefg`。  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(1) RIGHT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-------  
fg
```  
  
## <a name="see-also"></a>另请参阅  
 [强制转换和转换 &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


