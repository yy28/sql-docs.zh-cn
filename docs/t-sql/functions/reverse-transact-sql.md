---
title: REVERSE (Transact-SQL) | Microsoft Docs
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
- REVERSE_TSQL
- REVERSE
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], reverse
- REVERSE function
- reverse character expressions
ms.assetid: 555d8877-7cc7-4955-ae2c-6215aca313b7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c14fb9f1e0f6e7b3f0cb224036af37e6a7b19e23
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="reverse-transact-sql"></a>REVERSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回字符串值的逆序。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
REVERSE ( string_expression )  
```  
  
## <a name="arguments"></a>参数  
 string_expression  
 string_expression 是字符串或二进制数据类型的[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。 string_expression 可以是常量、变量，也可以是字符列或二进制数据列。  
  
## <a name="return-types"></a>返回类型  
 varchar 或 nvarchar  
  
## <a name="remarks"></a>Remarks  
 string_expression 的数据类型必须可隐式转换为 varchar。 否则，请使用 [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) 显式转换 string_expression。  
  
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
  
 以下示例从 int 数据类型隐式转换为 varchar 数据类型，然后反转结果。  
  
```  
SELECT REVERSE(1234) AS Reversed ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例返回所有数据库的名称，以及字符被反转的名称。  
  
```  
SELECT name, REVERSE(name) FROM sys.databases;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS (Transact-SQL)](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE (Transact-SQL)](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME (Transact-SQL)](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE (Transact-SQL)](../../t-sql/functions/replace-transact-sql.md)  
 [STRING_AGG (Transact-SQL)](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE (Transact-SQL)](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF (Transact-SQL)](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE (Transact-SQL)](../../t-sql/functions/translate-transact-sql.md)  
 [CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

