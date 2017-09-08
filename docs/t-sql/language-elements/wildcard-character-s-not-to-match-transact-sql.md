---
title: "（通配符的字符不到匹配项）(Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- wildcard
- '[^]_TSQL'
- '[^]'
- Not Match
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[^] (wildcard - character(s) not to match)'
ms.assetid: b970038f-f4e7-4a5d-96f6-51e3248c6aef
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 96749cb88e4d98b112de2ce1eb9bff4c7e156e42
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="wildcard---characters-not-to-match-transact-sql"></a>（通配符的字符不到匹配项）(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  匹配不在方括号之间指定的范围或集合内的任何单个字符。  
  
## <a name="examples"></a>示例  
 下面的示例使用 [^] 运算符在 `Contact` 表中查找所有名字以 `Al` 开头且第三个字母不是字母 `a` 的所有人。  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Al[^a]%'  
ORDER BY FirstName;  
```  
  
## <a name="see-also"></a>另请参阅  
 [如 &#40;Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [%&#40;通配符-字符 &#40; &#41;到匹配 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91;&#93;（通配符-到匹配项的字符）](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [_ （通配符-匹配一个字符）](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
  
  

