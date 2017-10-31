---
title: "TRIM (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
caps.latest.revision: 4
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 64cef84a613d71e65b33bed1c1e740dc59eeed9d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="trim-transact-sql"></a>TRIM (Transact SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

删除空格字符`char(32)`或其他指定的字符开始或字符串末尾。  
 
## <a name="syntax"></a>语法   
```
TRIM ( [ characters FROM ] string ) 
```
[//]: # "[同时 |前导 |尾随] 不尚未可用。"

## <a name="arguments"></a>参数   

字符   
是文本、 变量或函数调用的任何非 LOB 字符类型 (`nvarchar`， `varchar`， `nchar`，或`char`) 包含应删除的字符。 `nvarchar(max)`和`varchar(max)`不允许类型。

string   
是任何字符类型的表达式 (`nvarchar`， `varchar`， `nchar`，或`char`) 应删除字符。

## <a name="return-types"></a>返回类型   
返回类型为字符串自变量的字符表达式中的空白字符`char(32)`或其他指定的字符会从双方。 返回`NULL`输入的字符串是否`NULL`。

## <a name="remarks"></a>注释   
默认情况下`TRIM`函数将移除空白字符`char(32)`从双方。 这等效于 `LTRIM(RTRIM(@string))`。 行为`TRIM `具有对指定字符函数等同于行为`REPLACE`函数其中将从开始或结束处的字符替换为空字符串。


## <a name="examples"></a>示例
### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  从字符串两端移除空白字符   
下面的示例中删除空格，从之前和之后单词`test`。   
```tsql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>B.  移除指定的字符从字符串两端   
下面的示例删除一个尾随句点和尾随空格。
```tsql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>另请参阅
[字符串函数 (TRANSACT-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
[LTRIM (Transact SQL)](../../t-sql/functions/ltrim-transact-sql.md)   
[RTRIM (Transact SQL)](../../t-sql/functions/rtrim-transact-sql.md)   
[REPLACE (Transact SQL)](../../t-sql/functions/replace-transact-sql.md)   

