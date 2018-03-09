---
title: "_ （通配符-匹配一个字符） (Transact SQL) |Microsoft 文档"
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
- Match
- wildcard
- _TSQL
- Match One
- _
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 01bc0c4c006ae55395d752a0377575fa680dffaa
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="-wildcard---match-one-character-transact-sql"></a>_（通配符 - 匹配一个字符）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

使用下划线字符 _ 如涉及模式匹配的字符串比较操作中任何单个字符相匹配`LIKE`和`PATINDEX`。  
  
## <a name="examples"></a>示例  

## <a name="a-simple-example"></a>答： 简单的示例   

下面的示例返回所有数据库以字母开头的名称`m`和有号`d`作为第三个字母。 下划线字符指定名称的第二个字符可以是任何字母。 `model`和`msdb`数据库满足此条件。 `master`不是数据库。

```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm_d%';
```   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-----
model
msdb
```   
您可能必须满足此条件的其他数据库。

可以使用多个下划线来表示多个字符。 更改`LIKE`条件以包括两个下划线`'m__%`结果中包括 master 数据库。

### <a name="b-more-complex-example"></a>B： 更复杂示例
 下面的示例使用 _ 运算符查找中的所有人`Person`表中，有三个字母名字以结尾`an`。  
  
```sql  
-- USE AdventureWorks2012
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C： 转义下划线字符   
下面的示例返回的固定的数据库角色，如名称`db_owner`和`db_ddladmin`，但它还返回`dbo`用户。 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

中的第三个的字符位置下划线作为通配符，和仅开头字母的主体不筛选`db_`。 进行转义下划线请将其括在方括号内`[_]`。 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
现在`dbo`排除用户。   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>另请参阅  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [%（通配符-字符到匹配项）](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91;&#93;（通配符-到匹配项的字符）](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93;（通配符的字符不到匹配项）](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  
