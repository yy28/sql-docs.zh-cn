---
title: "UPPER (Transact SQL) |Microsoft 文档"
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
- UPPER_TSQL
- UPPER
dev_langs:
- TSQL
helpviewer_keywords:
- UPPER function
- characters [SQL Server], lowercase
- converting lowercase to uppercase
- uppercase characters [SQL Server]
- characters [SQL Server], uppercase
- lowercase characters
ms.assetid: 5ced55f7-ac89-4cf2-9465-f63f4dc480db
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7572e82178b211fba9967a88cb16c20d059c7b52
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="upper-transact-sql"></a>UPPER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回小写字符数据转换为大写的字符表达式。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
UPPER ( character_expression )  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的字符数据。 *character_expression*可以是常量、 变量或列的字符或二进制数据。  
  
 *character_expression*的隐式转换为数据类型必须为**varchar**。 否则，请使用[强制转换](../../t-sql/functions/cast-and-convert-transact-sql.md)可以显式转换*character_expression*。  
  
## <a name="return-types"></a>返回类型  
 **varchar**或**nvarchar**  
  
## <a name="examples"></a>示例  
 以下示例使用 `UPPER` 和 `RTRIM` 函数返回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `Person` 表中人员的姓氏，以便使它大写、得到修整并与名字连在一起。  
  
```  
SELECT UPPER(RTRIM(LastName)) + ', ' + FirstName AS Name  
FROM Person.Person  
ORDER BY LastName;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例使用`UPPER`和`RTRIM`函数以返回中的人员的姓氏`dbo.DimEmployee`表，以便它在大写、 修整，和串联的第一个名称。  
  
```  
-- Uses AdventureWorks  
  
SELECT UPPER(RTRIM(LastName)) + ', ' + FirstName AS Name  
FROM dbo.DimEmployee  
ORDER BY LastName;  
```  
  
 以下为部分结果集。  
  
 `Name`  
  
 `------------------------------`  
  
 `ABBAS, Syed`  
  
 `ABERCROMBIE, Kim`  
  
 `ABOLROUS, Hazem`  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


