---
title: "ASCII (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
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
- ASCII_TSQL
- ASCII
dev_langs: TSQL
helpviewer_keywords:
- ASCII function
- characters [SQL Server], ASCII
- code [SQL Server], ASCII
- leftmost character of expression
ms.assetid: 45c2044a-0593-4805-8bae-0fad4bde2e6b
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 02267e12891bf1ab237cd7bffb2fa89f4be32363
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="ascii-transact-sql"></a>ASCII (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回字符表达式中最左侧的字符的 ASCII 代码值。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
ASCII ( character_expression )  
```  
  
## <a name="arguments"></a>参数  
*character_expression*  
是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)类型的**char**或**varchar**。
  
## <a name="return-types"></a>返回类型
 **int**  
  
## <a name="remarks"></a>注释
ASCII 是美国信息交换的标准代码的缩写。 它是编码标准的计算机使用的字符。 ASCII 字符的列表，请参阅**可打印字符**部分[ASCII](https://www.wikipedia.org/wiki/ASCII)。

## <a name="examples"></a>示例  
下面的示例假定 ASCII 字符集，并返回`ASCII`6 个字符的值。
  
```sql
SELECT ASCII('A') AS A, ASCII('B') AS B,   
ASCII('a') AS a, ASCII('b') AS b,  
ASCII(1) AS [1], ASCII(2) AS [2];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
A           B           a           b           1           2  
----------- ----------- ----------- ----------- ----------- -----------  
65          66          97          98          49          50  
```  
  
## <a name="see-also"></a>另请参阅
[字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
  


