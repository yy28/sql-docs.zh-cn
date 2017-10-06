---
title: "较低 (Transact SQL) |Microsoft 文档"
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
- LOWER
- LOWER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- characters [SQL Server], lowercase
- LOWER function
- uppercase characters [SQL Server]
- characters [SQL Server], uppercase
- lowercase characters
- converting uppercase to lowercase characters
ms.assetid: 1783352b-6852-4658-9d94-51963c59b9bf
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 545d3b5a0635c80f55aeb5b0a7a4e1804098e19c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lower-transact-sql"></a>LOWER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  将大写字符数据转换为小写字符数据后返回字符表达式。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
LOWER ( character_expression )  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)字符或二进制数据。 *character_expression*可以是常量、 变量或列。 *character_expression*的隐式转换为数据类型必须为**varchar**。 否则，请使用[强制转换](../../t-sql/functions/cast-and-convert-transact-sql.md)可以显式转换*character_expression*。  
  
## <a name="return-types"></a>返回类型  
 **varchar**或**nvarchar**  
  
## <a name="examples"></a>示例  
 以下示例将使用 `LOWER` 函数、`UPPER` 函数，并将 `UPPER` 函数嵌套在 `LOWER` 函数中，选择价格在 $11 到 $20 之间的产品名称。 此示例使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库。  
  
```  
SELECT LOWER(SUBSTRING(Name, 1, 20)) AS Lower,   
   UPPER(SUBSTRING(Name, 1, 20)) AS Upper,   
   LOWER(UPPER(SUBSTRING(Name, 1, 20))) As LowerUpper  
FROM Production.Product  
WHERE ListPrice between 11.00 and 20.00;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Lower                    Upper                    LowerUpper  
---------------------    ---------------------    --------------------  
minipump                 MINIPUMP                 minipump 
taillights - battery     TAILLIGHTS - BATTERY     taillights - battery  
  
(2 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 以下示例将使用 `LOWER` 函数、`UPPER` 函数，并将 `UPPER` 函数嵌套在 `LOWER` 函数中，选择价格在 $11 到 $20 之间的产品名称。  
  
```  
-- Uses AdventureWorks  
  
SELECT LOWER(SUBSTRING(EnglishProductName, 1, 20)) AS Lower,   
       UPPER(SUBSTRING(EnglishProductName, 1, 20)) AS Upper,   
       LOWER(UPPER(SUBSTRING(EnglishProductName, 1, 20))) As LowerUpper  
FROM dbo.DimProduct  
WHERE ListPrice between 11.00 and 20.00;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Lower                 Upper                  LowerUpper  
--------------------  ---------------------  --------------------  
minipump              MINIPUMP               minipump  
taillights – battery  TAILLIGHTS – BATTERY   taillights - battery
```  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


