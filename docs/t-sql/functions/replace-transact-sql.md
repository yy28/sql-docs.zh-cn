---
title: "REPLACE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REPLACE_TSQL
- REPLACE
dev_langs: TSQL
helpviewer_keywords:
- first string expression [SQL Server]
- replacing string expression
- third string expressions [SQL Server]
- second string expressions [SQL Server]
- REPLACE function
ms.assetid: 8a7aaaf2-62e3-46c0-8e44-fa22290dd86b
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a50c0b7220eba654df21349e2fd3cd57b9a0d7d3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="replace-transact-sql"></a>REPLACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  用另一个字符串值替换出现的所有指定字符串值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
REPLACE ( string_expression , string_pattern , string_replacement )  
```  
  
## <a name="arguments"></a>参数  
 *string_expression*  
 为字符串[表达式](../../t-sql/language-elements/expressions-transact-sql.md)要搜索。 *string_expression*可以是字符串或二进制数据类型。  
  
 *string_*模式  
 是要查找的子字符串。 *string_pattern*可以是字符串或二进制数据类型。 *string_pattern*不能为空字符串 （"），且不能超过每页显示的最大字节数。  
  
 *string_*替换  
 替换字符串。 *string_replacement*可以是字符串或二进制数据类型。  
  
## <a name="return-types"></a>返回类型  
 返回**nvarchar**如果输入自变量之一是**nvarchar**数据类型; 否则，将返回**varchar**。  
  
 如果任何一个参数为 NULL，则返回 NULL。  
  
 如果*string_expression*的类型不是**varchar （max)**或**nvarchar （max)，替换**截断返回值为 8000 个字节。 返回值大于 8000 个字节， *string_expression*必须显式转换为大型值数据类型。  
  
## <a name="remarks"></a>注释  
 REPLACE 根据输入的排序规则执行比较操作。 若要在指定的排序规则执行比较，可以使用[COLLATE](~/t-sql/statements/collations.md)将显式排序规则应用于输入。  
  
 0x0000 (**char(0)**) 是 Windows 排序规则中未定义的字符，不能包含在替换中。  
  
## <a name="examples"></a>示例  
 以下示例使用 `cde` 替换 `abcdefghi` 中的字符串 `xxx`。  
  
```sql  
SELECT REPLACE('abcdefghicde','cde','xxx');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
abxxxfghixxx  
(1 row(s) affected)  
```  
  
 下面的示例使用 `COLLATE` 函数。  
  
```sql  
SELECT REPLACE('This is a Test'  COLLATE Latin1_General_BIN,  
'Test', 'desk' );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
This is a desk  
(1 row(s) affected)  
```  

  
## <a name="see-also"></a>另请参阅  
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [字符串函数 &#40;Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
