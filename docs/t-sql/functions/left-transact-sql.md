---
title: "左 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LEFT
- LEFT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- character strings [SQL Server], LEFT
- characters [SQL Server], leftmost
- LEFT function
- leftmost character of expression
ms.assetid: 44a8c71b-63d8-458b-8b5d-99d570067c3c
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0b0ec58ed9e8bbaae6f4f4ae90834f415476b039
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="left-transact-sql"></a>LEFT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回字符串中从左边开始指定个数的字符。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
LEFT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)字符或二进制数据。 *character_expression*可以是常量、 变量或列。 *character_expression*可以是任何数据类型，除**文本**或**ntext**，可以隐式转换为**varchar**或**nvarchar**。 否则，请使用[强制转换](../../t-sql/functions/cast-and-convert-transact-sql.md)函数可以显式转换*character_expression*。  
  
 *integer_expression*  
 是一个正整数，指定的多少个字符*character_expression*将返回。 如果*integer_expression*为负，则返回一个错误。 如果*integer_expression*是类型**bigint**和包含较大的值， *character_expression*必须是较大的数据类型的如**varchar （max)**.  
  
 *Integer_expression*参数计数为一个字符的 utf-16 代理项字符。  
  
## <a name="return-types"></a>返回类型  
 返回**varchar**时*character_expression*是非 Unicode 字符数据类型。  
  
 返回**nvarchar**时*character_expression*是 Unicode 字符数据类型。  
  
## <a name="remarks"></a>注释  
 使用 SC 排序规则时*integer_expression*参数计数为一个字符的 utf-16 代理项对。 有关详细信息，请参阅 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-left-with-a-column"></a>A. 带列使用 LEFT  
 以下示例返回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `Product` 表中每个产品名称中最左边的五个字符。  
  
```  
SELECT LEFT(Name, 5)   
FROM Production.Product  
ORDER BY ProductID;  
GO  
```  
  
### <a name="b-using-left-with-a-character-string"></a>B. 带字符串使用 LEFT  
 以下示例使用 `LEFT` 函数返回字符串 `abcdefg` 中最左边的两个字符。  
  
```  
SELECT LEFT('abcdefg',2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab   
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-left-with-a-column"></a>C. 带列使用 LEFT  
 以下示例返回每个产品名中最左边的五个字符。  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT(EnglishProductName, 5)   
FROM dbo.DimProduct  
ORDER BY ProductKey;  
```  
  
### <a name="d-using-left-with-a-character-string"></a>D. 带字符串使用 LEFT  
 以下示例使用 `LEFT` 函数返回字符串 `abcdefg` 中最左边的两个字符。  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab  
```  
  
## <a name="see-also"></a>另请参阅  
 [强制转换和转换 &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


