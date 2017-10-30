---
title: "（通配符-到匹配项的字符）(Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Match
- wildcard
- '[ ]'
- '[_]_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[ ] (wildcard - character(s) to match)'
ms.assetid: 57817576-0bf1-49ed-b05d-fac27e8fed7a
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18688c96cd0369905844d79a1a109f4e5032bce3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="wildcard---characters-to-match-transact-sql"></a>（通配符-到匹配项的字符）(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在指定的范围或括号之间指定集内的任何单个字符匹配`[ ]`。 可以在涉及模式匹配，如的字符串比较中使用这些通配符`LIKE`和`PATINDEX`。  
  
## <a name="examples"></a>示例  
### <a name="a-simple-example"></a>答： 简单的示例   
下面的示例返回的字母开头的名称`m`。 `[n-z]`指定，使用某处范围内必须是第二个字母`n`到`z`。 百分号通配符`%`允许使用 3 字符开头的任何或任何字符。 `model`和`msdb`数据库满足此条件。 `master`数据库不并且不包括在结果集。
 
```tsql
SELECT name FROM sys.databases
WHERE name LIKE 'm[n-z]%';
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
name
-----
model
msdb
```   
 您可能必须安装的其他符合条件的数据库。


### <a name="b-more-complex-example"></a>B： 更复杂示例   
 以下示例使用 [] 运算符查找其地址中有四位邮政编码的所有 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 雇员的 ID 和姓名。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT e.BusinessEntityID, p.FirstName, p.LastName, a.PostalCode  
FROM HumanResources.Employee AS e  
INNER JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
INNER JOIN Person.Address AS a ON a.AddressID = ea.AddressID  
WHERE a.PostalCode LIKE '[0-9][0-9][0-9][0-9]';  
```  
  
 下面是结果集：  
  
```  
EmployeeID      FirstName      LastName      PostalCode  
----------      ---------      ---------     ----------  
290             Lynn           Tsoflias      3000  
```  



  
## <a name="see-also"></a>另请参阅  
 [如 &#40;Transact SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [%（通配符-字符到匹配项）](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93;（通配符的字符不到匹配项）](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_ （通配符-匹配一个字符）](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  

