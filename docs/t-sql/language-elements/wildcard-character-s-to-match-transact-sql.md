---
title: "[] （通配符-到匹配项的字符） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 04fcf0d9e76db380430bfbf4c4ed6e5fadf14afb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="--wildcard---characters-to-match-transact-sql"></a>\[\] （通配符-到匹配项个字符） (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在指定的范围或括号之间指定集内的任何单个字符匹配`[ ]`。 可以在涉及模式匹配，如的字符串比较中使用这些通配符`LIKE`和`PATINDEX`。  
  
## <a name="examples"></a>示例  
### <a name="a-simple-example"></a>答： 简单的示例   
下面的示例返回的字母开头的名称`m`。 `[n-z]`指定，使用某处范围内必须是第二个字母`n`到`z`。 百分号通配符`%`允许使用 3 字符开头的任何或任何字符。 `model`和`msdb`数据库满足此条件。 `master`数据库不并且不包括在结果集。
 
```sql
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
  
```sql  
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
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [%&#40;通配符-字符 &#40; &#41;到匹配 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93;&#40;通配符-字符 &#40; &#41;不到匹配 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [\_&#40;通配符-匹配一个字符 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
