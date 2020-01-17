---
title: 用于排除字符的 [^] 通配符
description: 用于不匹配字符的 T-SQL 通配符
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a55abc5a9554ec68df33310f4f041e9605961c7e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245279"
---
# <a name="-wildcard---characters-not-to-match-transact-sql"></a>\[^\]（通配符 - 无需匹配的字符）(Transact-SQL)
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
 [LIKE (Transact-SQL)](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX (Transact-SQL)](../../t-sql/functions/patindex-transact-sql.md)   
 [%（通配符 - 需匹配的字符）(Transact-SQL)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [（通配符 - 需匹配的字符）(Transact-SQL)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [\_（通配符 - 匹配一个字符）(Transact-SQL)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
  
  
