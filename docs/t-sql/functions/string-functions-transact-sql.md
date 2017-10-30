---
title: "字符串函数 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/15/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], strings
- strings [SQL Server], functions
- string functions
- strings [SQL Server]
ms.assetid: 6940a83d-5374-4af3-bb27-5d89c8af83ac
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 33df9a7082ee7e637b60e3a1ca7911e127040a08
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="string-functions-transact-sql"></a>字符串函数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  以下标量函数对字符串输入值执行操作，并返回字符串或数值：  
  
||||  
|-|-|-| 
|[ASCII](../../t-sql/functions/ascii-transact-sql.md)|[CHAR](../../t-sql/functions/char-transact-sql.md)|[CHARINDEX](../../t-sql/functions/charindex-transact-sql.md)|
|[CONCAT](../../t-sql/functions/concat-transact-sql.md)|[CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md)|[差异](../../t-sql/functions/difference-transact-sql.md) |
|[格式](../../t-sql/functions/format-transact-sql.md)|[LEFT](../../t-sql/functions/left-transact-sql.md)|[LEN](../../t-sql/functions/len-transact-sql.md) |
|[较低](../../t-sql/functions/lower-transact-sql.md)|[LTRIM](../../t-sql/functions/ltrim-transact-sql.md)|[NCHAR](../../t-sql/functions/nchar-transact-sql.md) |
|[PATINDEX](../../t-sql/functions/patindex-transact-sql.md)|[QUOTENAME](../../t-sql/functions/quotename-transact-sql.md)|[REPLACE](../../t-sql/functions/replace-transact-sql.md) |
|[复制](../../t-sql/functions/replicate-transact-sql.md)|[REVERSE](../../t-sql/functions/reverse-transact-sql.md) |[RIGHT](../../t-sql/functions/right-transact-sql.md) |
|[RTRIM](../../t-sql/functions/rtrim-transact-sql.md)|[SOUNDEX](../../t-sql/functions/soundex-transact-sql.md) |[空间](../../t-sql/functions/space-transact-sql.md) |
|[STR](../../t-sql/functions/str-transact-sql.md)|[STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md)|[STRING_ESCAPE](../../t-sql/functions/string-escape-transact-sql.md) |
|[STRING_SPLIT](../../t-sql/functions/string-split-transact-sql.md)|[STUFF](../../t-sql/functions/stuff-transact-sql.md)|[SUBSTRING](../../t-sql/functions/substring-transact-sql.md) |
|[翻译](../../t-sql/functions/translate-transact-sql.md)|[TRIM](../../t-sql/functions/trim-transact-sql.md)|[UNICODE](../../t-sql/functions/unicode-transact-sql.md) |
|[上限](../../t-sql/functions/upper-transact-sql.md) | | |


  
 所有内置字符串函数除外`FORMAT`都具有确定性。 这意味着每次用一组特定的输入值调用它们时，都返回相同的值。 有关函数的确定性的详细信息，请参阅[Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
 将不是字符串值的参数传递给字符串函数时，输入类型会隐式地转换为文本数据类型。. 有关详细信息，请参阅[数据类型转换 &#40; 数据库引擎 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)。  
  
## <a name="see-also"></a>另请参阅  
 [内置函数 (Transact-SQL)](~/t-sql/functions/functions.md)  
  
  


