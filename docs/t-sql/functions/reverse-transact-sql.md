---
title: "反向 (Transact SQL) |Microsoft 文档"
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
- REVERSE_TSQL
- REVERSE
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], reverse
- REVERSE function
- reverse character expressions
ms.assetid: 555d8877-7cc7-4955-ae2c-6215aca313b7
caps.latest.revision: 46
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8696a2cff3589b9b756e2ddd9cc1160b465b70d8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="reverse-transact-sql"></a>REVERSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回字符串值的逆序。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
REVERSE ( string_expression )  
```  
  
## <a name="arguments"></a>参数  
 *string_expression*  
 *string_expression*是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的字符串或二进制数据类型。 *string_expression*可以是常量、 变量或列的字符或二进制数据。  
  
## <a name="return-types"></a>返回类型  
 **varchar**或**nvarchar**  
  
## <a name="remarks"></a>注释  
 *string_expression*的隐式转换为数据类型必须为**varchar**。 否则，请使用[强制转换](../../t-sql/functions/cast-and-convert-transact-sql.md)可以显式转换*string_expression*。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>补充字符（代理项对）  
 使用 SC 排序规则时，REVERSE 函数将不反转代理项对的两部分的顺序。  
  
## <a name="examples"></a>示例  
 以下示例返回字符被反转的所有联系人的名字。 此示例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库。  
  
```  
SELECT FirstName, REVERSE(FirstName) AS Reverse  
FROM Person.Person  
WHERE BusinessEntityID < 5  
ORDER BY FirstName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FirstName      Reverse
-------------- --------------
Ken            neK
Rob            boR
Roberto        otreboR
Terri          irreT

(4 row(s) affected)
```  
  
 以下示例反转变量中的字符。  
  
```  
DECLARE @myvar varchar(10);  
SET @myvar = 'sdrawkcaB';  
SELECT REVERSE(@myvar) AS Reversed ;  
GO  
```  
  
 下面的示例使隐式转换**int**数据类型到**varchar**数据类型，然后反转结果。  
  
```  
SELECT REVERSE(1234) AS Reversed ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例返回所有数据库的名称，其中包含的字符的名称取消。  
  
```  
SELECT name, REVERSE(name) FROM sys.databases;  
GO  
```  
  
 以下示例反转变量中的字符。  
  
```  
DECLARE @myvar varchar(10);  
SET @myvar = 'sdrawkcaB';  
SELECT REVERSE(@myvar) AS Reversed ;  
GO  
```  
  
 下面的示例使隐式转换**int**数据类型到**varchar**数据类型，然后反转结果。  
  
```  
SELECT REVERSE(1234) AS Reversed ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [强制转换和转换 &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


