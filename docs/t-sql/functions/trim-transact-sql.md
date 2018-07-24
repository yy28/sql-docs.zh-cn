---
title: TRIM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
caps.latest.revision: 4
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: a880c9de5b763386504a4163ffe44aaf62c136b4
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37981376"
---
# <a name="trim-transact-sql"></a>TRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

从字符串的开头或末尾删除空格字符 `char(32)` 或其他指定字符。  
 
## <a name="syntax"></a>语法   
```
TRIM ( [ characters FROM ] string ) 
```
[//]: # "[ BOTH | LEADING | TRAILING ] 尚不可用。"

## <a name="arguments"></a>参数   

字符   
任何非 LOB 字符类型（`nvarchar`、`varchar`、`nchar` 或 `char`）的文本、变量或函数调用，其中包含应删除的字符。 不允许 `nvarchar(max)` 和 `varchar(max)` 类型。

string   
任何字符类型（`nvarchar`、`varchar`、`nchar` 或 `char`）的表达式，其中应删除字符。

## <a name="return-types"></a>返回类型   
返回一个字符串参数类型的字符表达式，其中已从两侧删除空格字符 `char(32)` 或其他指定字符。 如果输入字符串是 `NULL`，则返回 `NULL`。

## <a name="remarks"></a>Remarks   
默认情况下，`TRIM` 函数会删除 `char(32)` 两侧的空格字符。 这等效于 `LTRIM(RTRIM(@string))`。 具有指定字符的 `TRIM ` 函数的行为与 `REPLACE` 函数（其中开头或末尾处的字符替换为空字符串）的行为相同。


## <a name="examples"></a>示例
### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  删除字符串两侧的空格字符   
以下示例删除了 `test` 一词前后的空格。   
```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>B.  删除字符串两侧的指定字符   
以下示例删除了尾随句点和尾随空格。
```sql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>另请参阅
 [LEFT (Transact-SQL)](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM (Transact-SQL)](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT (Transact-SQL)](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM (Transact-SQL)](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT (Transact-SQL)](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING (Transact-SQL)](../../t-sql/functions/substring-transact-sql.md)  
 [字符串函数 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
