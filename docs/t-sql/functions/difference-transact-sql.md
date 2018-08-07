---
title: DIFFERENCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DIFFERENCE
- DIFFERENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DIFFERENCE function
- comparing SOUNDEX values
- SOUNDEX values
ms.assetid: c58ca25d-d6ea-48fa-93bb-c9374b0b2a2b
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 91a9bb5b8dad50ac23c114188bde61e3650ec554
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39456981"
---
# <a name="difference-transact-sql"></a>DIFFERENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

该函数返回一个整数值，用于度量两个不同字符表达式的 [SOUNDEX()](./soundex-transact-sql.md) 值之间的差异。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DIFFERENCE ( character_expression , character_expression )  
```  
  
## <a name="arguments"></a>参数  
*character_expression*  
字符数据的字母数字[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。 character_expression 可以是常量、变量或列。  
  
## <a name="return-types"></a>返回类型  
**int**  
 
## <a name="remarks"></a>Remarks  
`DIFFERENCE` 比较两个不同的 `SOUNDEX` 值，并返回一个整数值。 该值用于度量 `SOUNDEX` 值匹配的程度，范围为 0 到 4。 值为 0 表示 SOUNDEX 值之间的相似性较弱或不相似；4 表示与 SOUNDEX 值非常相似，甚至完全相同。  
  
`DIFFERENCE` 和 `SOUNDEX` 具有排序规则敏感度。  
  
## <a name="examples"></a>示例  
本示例的第一部分比较两个非常相似的字符串的 `SOUNDEX` 值。 对于 Latin1_General 排序规则，`DIFFERENCE` 返回的值为 `4`。 示例的第二部分比较两个差异较大的字符串的 `SOUNDEX` 值，对于 Latin1_General 排序规则，`DIFFERENCE` 返回的值为 `0`。  
  
```  
-- Returns a DIFFERENCE value of 4, the least possible difference.  
SELECT SOUNDEX('Green'), SOUNDEX('Greene'), DIFFERENCE('Green','Greene');  
GO  
-- Returns a DIFFERENCE value of 0, the highest possible difference.  
SELECT SOUNDEX('Blotchet-Halls'), SOUNDEX('Greene'), DIFFERENCE('Blotchet-Halls', 'Greene');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----- ----- -----------   
G650  G650  4             
  
(1 row(s) affected)  
  
----- ----- -----------   
B432  G650  0             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [SOUNDEX (Transact-SQL)](../../t-sql/functions/soundex-transact-sql.md)   
 [字符串函数 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

