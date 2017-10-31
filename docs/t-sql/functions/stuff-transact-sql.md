---
title: "内容 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STUFF
- STUFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting characters
- STUFF function
- length characters
- removing characters
- replacing characters
- characters [SQL Server], replacing
- inserting data
ms.assetid: abb0afa9-44f6-42a2-a871-5f471dfb222b
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: df9a3d019f22ec8a0ba610f2dd694e45a8bd9da3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/08/2017

---
# <a name="stuff-transact-sql"></a>STUFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  STUFF 函数将字符串插入到另一个字符串中。 它从第一个字符串的开始位置删除指定长度的字符；然后将第二个字符串插入到第一个字符串的开始位置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
STUFF ( character_expression , start , length , replaceWith_expression )  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的字符数据。 *character_expression*可以是常量、 变量或列的字符或二进制数据。  
  
 *启动*  
 一个整数值，指定删除和插入的开始位置。 如果*启动*或*长度*为负，则返回一个 null 字符串。 如果*启动*长于第一个*character_expression*，则返回 null 字符串。 *启动*可以是类型**bigint**。  
  
 *length*  
 一个整数，指定要删除的字符数。 如果*长度*长于第一个*character_expression*，则最多删除到最后一个字符在最后一个*character_expression*。 *长度*可以是类型**bigint**。  
  
 *replaceWith_expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)的字符数据。 *character_expression*可以是常量、 变量或列的字符或二进制数据。 此表达式替换*长度*字符*character_expression*开始*启动*。 提供`NULL`作为*replaceWith_expression*，删除字符，而不插入任何内容。   
  
## <a name="return-types"></a>返回类型  
 返回字符数据，如果*character_expression*是一种受支持的字符数据类型。 如果返回二进制数据*character_expression*是支持的二进制数据类型之一。  
  
## <a name="remarks"></a>注释  
 如果开始位置或长度值是负数，或者开始位置大于第一个字符串的长度，则返回 Null 字符串。 如果开始位置为 0，则返回 Null 值。 如果要删除的长度大于第一个字符串的长度，则删除到第一个字符串中的第一个字符。  

如果结果值大于返回类型支持的最大值，则会引发错误。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>补充字符（代理项对）  
 当使用 SC 排序规则，同时*character_expression*和*replaceWith_expression*可以包含代理项对。 长度参数对每个代理项计数*character_expression*单个字符的形式。  
  
## <a name="examples"></a>示例  
 以下示例从第一个字符串 `abcdef` 的第 `2` 个位置 (`b`) 开始删除三个字符，然后在删除位置插入第二个字符串，从而创建并返回一个字符串。  
  
```  
SELECT STUFF('abcdef', 2, 3, 'ijklmn');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
aijklmnef   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  

