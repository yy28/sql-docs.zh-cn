---
title: "RTRIM (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RTRIM_TSQL
- RTRIM
dev_langs: TSQL
helpviewer_keywords:
- RTRIM function
- character strings [SQL Server], trailing blanks
- blank characters [SQL Server]
- trailing blanks
ms.assetid: 52fd6e8d-650c-4f66-abcf-67765aa5aa83
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 25675a181225e600a16738f50322fdabcae839a4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="rtrim-transact-sql"></a>RTRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  截断所有尾随空格后返回的字符串。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
RTRIM ( character_expression )  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的字符数据。 *character_expression*可以是常量、 变量或列的字符或二进制数据。  
  
 *character_expression*的隐式转换为数据类型必须为**varchar**。 否则，请使用[强制转换](../../t-sql/functions/cast-and-convert-transact-sql.md)可以显式转换*character_expression*。  
  
## <a name="return-types"></a>返回类型  
 **varchar**或**nvarchar**  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-example"></a>A. 简单示例  
 以下示例将接受一个在句子结尾包含空格的字符串，并返回在句子结尾没有空格的文本。  
  
```  
SELECT RTRIM('Removes trailing spaces.   ');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
  `Removes trailing spaces.`  
  
### <a name="b-simple-example"></a>B： 简单的示例  
 下面的示例演示如何使用`RTRIM`删除尾随空格。 存在此时间是另一个连接到要显示空格都消失了第一个字符串的字符串。  
  
```  
SELECT RTRIM('Four spaces are after the period in this sentence.    ') + 'Next string.';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
`Four spaces are after the period in this sentence.Next string.`  

### <a name="c-using-rtrim-with-a-variable"></a>C. 将 RTRIM 用于变量  
 以下示例显示如何使用 `RTRIM` 删除字符变量中的尾随空格。  
  
```  
DECLARE @string_to_trim varchar(60);  
SET @string_to_trim = 'Four spaces are after the period in this sentence.    ';  
SELECT @string_to_trim + ' Next string.';  
SELECT RTRIM(@string_to_trim) + ' Next string.';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```sql   
 -------------------------------------------------------------------------  
 Four spaces are after the period in this sentence.     Next string.  
 
 (1 row(s) affected)`  
 
 -------------------------------------------------------------------------  
 Four spaces are after the period in this sentence. Next string.  
 
 (1 row(s) affected)
 ```  
  

  
## <a name="see-also"></a>另请参阅  
 [强制转换和转换 &#40;Transact SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
 [TRIM &#40;Transact SQL &#41;](../../t-sql/functions/trim-transact-sql.md)  
 [LTRIM &#40;Transact SQL &#41;](../../t-sql/functions/ltrim-transact-sql.md)  
  
  


