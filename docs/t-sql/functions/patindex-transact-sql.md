---
title: "PATINDEX (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/19/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PATINDEX
- PATINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first occurrence of pattern [SQL Server]
- searches [SQL Server], pattern starting position
- starting position of patten search
- pattern searching [SQL Server]
- PATINDEX function
ms.assetid: c0dfb17f-2230-4e36-98da-a9b630bab656
caps.latest.revision: 53
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: abf357840512c1447f0977a151ca742b148f45d2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="patindex-transact-sql"></a>PATINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回模式在指定表达式中第一次出现的起始位置；如果在所有有效的文本和字符数据类型中都找不到该模式，则返回零。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## <a name="arguments"></a>参数  
 *模式*  
 包含要查找的序列的字符表达式。 可以使用通配符;但是，字符 %必须早于并遵循*模式*（除外，当您搜索的第一个或最后一个字符）。 *模式*字符字符串数据类型类别的表达式。 *模式*限制为 8000 个字符。  
  
 *expression*  
 是[表达式](../../t-sql/language-elements/expressions-transact-sql.md)，通常会为指定的模式搜索的列。 *表达式*的字符字符串数据类型类别。  
  
## <a name="return-types"></a>返回类型  
 **bigint**如果*表达式*的**varchar （max)**或**nvarchar (max)**数据类型; 否则为**int**。  
  
## <a name="remarks"></a>注释  
 如果任一*模式*或*表达式*为 NULL，PATINDEX 返回 NULL。  
  
 PATINDEX 基于输入的排序规则执行比较。 若要以指定排序规则进行比较，则可以使用 COLLATE 将显式排序规则应用于输入。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>补充字符（代理项对）  
 在使用 SC 排序规则时，返回计数的值将任何 utf-16 代理项对*表达式*单个字符的形式的参数。 有关详细信息，请参阅 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
 0x0000 (**char(0)**) 是 Windows 排序规则中未定义的字符，不能包含在 PATINDEX。  
  
## <a name="examples"></a>示例  
  
### <a name="a-simple-patindex-example"></a>A. 简单 PATINDEX 示例  
 下面的示例检查短字符串 (`interesting data`) 字符的起始位置`ter`。  
  
```  
SELECT PATINDEX('%ter%', 'interesting data');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `3`  
  
### <a name="b-using-a-pattern-with-patindex"></a>B. 在 PATINDEX 中使用模式  
 以下示例查找模式 `ensure` 在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库的 `DocumentSummary` 表中 `Document` 列特定行中的开始位置。  
  
```  
SELECT PATINDEX('%ensure%',DocumentSummary)  
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
GO   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
64  
(1 row(s) affected)
```  
  
 如果未使用 `WHERE` 子句限制要搜索的行，查询将返回表中的所有行，对找到该模式的行报告非零值，对未找到该模式的行报告零值。  
  
### <a name="c-using-wildcard-characters-with-patindex"></a>C. 在 PATINDEX 中使用通配符  
 以下示例使用 % 和 _ 通配符查找模式 `'en'`（后跟任意一个字符和 `'ure'`）在指定字符串中的开始位置（索引从 1 开始）：  
  
```  
SELECT PATINDEX('%en_ure%', 'please ensure the door is locked');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
8  
```  
  
 `PATINDEX` 的作用与 `LIKE` 类似，因此，您可以使用任何通配符。 不必将模式放在百分号之间。 `PATINDEX('a%', 'abc')` 将返回 1；`PATINDEX('%a', 'cba')` 将返回 3。  
  
 与 `LIKE` 不同的是，`PATINDEX` 返回一个位置，这与 `CHARINDEX` 类似。  
  
### <a name="d-using-collate-with-patindex"></a>D. 在 PATINDEX 中使用 COLLATE  
 以下示例使用 `COLLATE` 函数显式指定要搜索的表达式的排序规则。  
  
```  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
  
### <a name="e-using-a-variable-to-specify-the-pattern"></a>E. 使用变量指定模式  
 下面的示例使用变量来传递到值*模式*参数。 此示例使用[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]数据库。  
  
```  
DECLARE @MyValue varchar(10) = 'safety';   
SELECT PATINDEX('%' + @MyValue + '%', DocumentSummary)   
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------------  
 22
 ```  
  

  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [&#40;通配符-字符 &#40; &#41;到匹配 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#40;通配符-字符 &#40; &#41;不到匹配 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)   
 [_ &#40;通配符-匹配一个字符 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)   
 [百分比字符 &#40;通配符-字符 &#40; &#41;到匹配 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)  
  
  



