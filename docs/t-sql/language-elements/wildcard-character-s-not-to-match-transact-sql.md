---
title: "[^]（通配符 - 无需匹配的字符）(Transact-SQL)| Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cef479bc6f0368a2d08a99265551cf7860b677e6
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
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
  
  
