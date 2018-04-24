---
title: CHARINDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CHARINDEX
- CHARINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], pattern searching
- CHARINDEX function
- pattern searching [SQL Server]
- starting point of expression in character string
ms.assetid: 78c10341-8373-4b30-b404-3db20e1a3ac4
caps.latest.revision: 52
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b0da42fc1b6a06c0a17f758bf692f065c1e3866c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="charindex-transact-sql"></a>CHARINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

在一个表达式中搜索另一个表达式并返回其起始位置（如果找到）。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
CHARINDEX ( expressionToFind , expressionToSearch [ , start_location ] )   
```  
  
## <a name="arguments"></a>参数  
expressionToFind  
包含要查找的序列的字符[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。 expressionToFind 限制在 8000 个字符以内。
  
expressionToSearch  
要搜索的字符表达式。
  
start_location  
表示搜索起始位置的 integer 或 bigint 表达式。 如果 start_location 未指定、为负数或为 0，则从 expressionToSearch 开头开始搜索。
  
## <a name="return-types"></a>返回类型
bigint（如果 expressionToSearch 的数据类型为 varchar(max)、nvarchar (max) 或 varbinary(max)）；否则为 int。
  
## <a name="remarks"></a>Remarks  
如果 expressionToFind 或 expressionToSearch 一个是 Unicode 数据类型（nvarchar 或 nchar），而另一个不是，则另一个会转换为 Unicode 数据类型。 在 CHARINDEX 中不能使用 text、ntext 和 image 数据类型。
  
如果 expressionToFind 或 expressionToSearch 为 NULL，则 CHARINDEX 返回 NULL。
  
如果在 expressionToSearch 中找不到 expressionToFind，则 CHARINDEX 返回 0。
  
CHARINDEX 根据输入的排序规则执行比较操作。 若要以指定排序规则进行比较，则可以使用 COLLATE 将显式排序规则应用于输入。
  
返回的起始位置从 1 开始，而不是从 0 开始。
  
0x0000 (char(0)) 是 Windows 排序规则中未定义的字符，不能包括在 CHARINDEX 中。
  
## <a name="supplementary-characters-surrogate-pairs"></a>补充字符（代理项对）  
在使用 SC 排序规则时，start_location 和返回值将代理项对计为一个字符，而不是计为两个字符。 有关详细信息，请参阅 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-starting-position-of-an-expression"></a>A. 返回表达式的起始位置  
以下示例返回字符序列 `bicycle` 在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `DocumentSummary` 表的 `Document` 列中的起始位置。
  
```sql
DECLARE @document varchar(64);  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bicycle', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
48            
```  
  
### <a name="b-searching-from-a-specific-position"></a>B. 从特定位置中搜索  
以下示例使用可选的 start_location 参数从 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `DocumentSummary` 列的第五个字符开始查找 `vital`。
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('vital', @document, 5);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
16            
  
(1 row(s) affected)  
```  
  
### <a name="c-searching-for-a-nonexistent-expression"></a>C. 搜索不存在的表达式  
以下示例显示在 expressionToSearch 中找不到 expressionToFind 时的结果集。
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bike', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
0
  
(1 row(s) affected)
```
  
### <a name="d-performing-a-case-sensitive-search"></a>D. 执行区分大小写的搜索  
以下示例在 `'This is a Test``'` 中执行区分大小写的字符串 `'TEST'` 搜索。
  
```sql
USE tempdb;  
GO  
--perform a case sensitive search  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
0
```  
  
以下示例在 `'This is a Test'` 中执行区分大小写的字符串 `'Test'` 搜索。
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'Test',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
13
```  
  
### <a name="e-performing-a-case-insensitive-search"></a>E. 执行不区分大小写的搜索  
以下示例在 `'TEST'` 中执行不区分大小写的字符串 `'This is a Test'` 搜索。
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CI_AS);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
13
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-searching-from-the-start-of-a-string-expression"></a>F. 从字符串表达式的开头搜索  
以下示例返回 `This is a string` 中 `is` 字符串的第一个位置，并从字符串中的位置 1（第一个字符）开始。
  
```sql
SELECT CHARINDEX('is', 'This is a string');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
3
```  
  
### <a name="g-searching-from-a-position-other-than-the-first-position"></a>G. 从第一个位置以外的位置搜索  
以下示例返回 `This is a string` 中 `is` 字符串的第一个位置，并从第四个位置开始。
  
```sql
SELECT CHARINDEX('is', 'This is a string', 4);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
 6
 ```  
  
### <a name="h-results-when-the-string-is-not-found"></a>H. 未找到字符串时的结果  
以下示例显示搜索字符串中找不到 string_pattern 时的返回值。
  
```sql
SELECT TOP(1) CHARINDEX('at', 'This is a string') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
0
```  
  
## <a name="see-also"></a>另请参阅
 [LEN (Transact-SQL)](../../t-sql/functions/len-transact-sql.md)  
 [PATINDEX (Transact-SQL)](../../t-sql/functions/patindex-transact-sql.md)  
 [字符串函数 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
 [+（字符串串联）(Transact-SQL)](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
 [排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  


