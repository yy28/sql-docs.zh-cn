---
title: "ASCII (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASCII_TSQL
- ASCII
dev_langs:
- TSQL
helpviewer_keywords:
- ASCII function
- characters [SQL Server], ASCII
- code [SQL Server], ASCII
- leftmost character of expression
ms.assetid: 45c2044a-0593-4805-8bae-0fad4bde2e6b
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d2c65df1f005b3d624f6a56f689f4125ec8175a7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="ascii-transact-sql"></a>ASCII (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
  
  



