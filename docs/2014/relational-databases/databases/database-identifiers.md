---
title: 数据库标识符 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- regular identifiers [SQL Server]
- identifiers [SQL Server]
- names [SQL Server], identifiers
- identifiers [SQL Server], about identifiers
- SQL Server identifiers
- Transact-SQL identifiers
- database objects [SQL Server], names
ms.assetid: 171291bb-f57f-4ad1-8cea-0b092d5d150c
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ec8e78ebf44a325490e937bea070cb4fc4d59178
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231257"
---
# <a name="database-identifiers"></a>数据库标识符
  数据库对象的名称即为其标识符。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的所有内容都可以有标识符。 服务器、数据库和数据库对象（例如表、视图、列、索引、触发器、过程、约束及规则等）都可以有标识符。 大多数对象要求有标识符，但对有些对象（例如约束），标识符是可选的。  
  
 对象标识符是在定义对象时创建的。 标识符随后用于引用该对象。 例如，下列语句创建一个标识符为 `TableX`的表，该表中有两列的标识符分别是 `KeyCol` 和 `Description`：  
  
```  
CREATE TABLE TableX  
(KeyCol INT PRIMARY KEY, Description nvarchar(80))  
```  
  
 此表还有一个未命名的约束。 `PRIMARY KEY` 约束没有标识符。  
  
 标识符的排序规则取决于定义标识符的级别。 为实例级对象（如登录名和数据库名）的标识符分配实例的默认排序规则。 为数据库对象（如表、视图和列名）的标识符分配数据库的默认排序规则。 例如，对于名称差别仅在于大小写的两个表，可在使用区分大小写排序规则的数据库中创建，但不能在使用不区分大小写排序规则的数据库中创建。  
  
> [!NOTE]  
>  变量的名称或函数和存储过程的参数必须符合 [!INCLUDE[tsql](../../includes/tsql-md.md)] 标识符的规则。  
  
## <a name="classes-of-identifiers"></a>标识符的种类  
 有两类标识符：  
  
 常规标识符  
 符合标识符的格式规则。 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用常规标识符时不用将其分隔开。  
  
```  
SELECT *  
FROM TableX  
WHERE KeyCol = 124  
```  
  
 分隔标识符  
 包含在双引号 (") 或者方括号 ([ ]) 内。 不会分隔符合标识符格式规则的标识符。 例如：  
  
```  
SELECT *  
FROM [TableX]         --Delimiter is optional.  
WHERE [KeyCol] = 124  --Delimiter is optional.  
```  
  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中，必须对不符合所有标识符规则的标识符进行分隔。 例如：  
  
```  
SELECT *  
FROM [My Table]      --Identifier contains a space and uses a reserved keyword.  
WHERE [order] = 10   --Identifier is a reserved keyword.  
```  
  
 常规标识符和分隔标识符包含的字符数都必须在 1 到 128 之间。 对于本地临时表，标识符最多可以有 116 个字符。  
  
## <a name="rules-for-regular-identifiers"></a>常规标识符规则  
 变量、函数和存储过程的名称必须符合 [!INCLUDE[tsql](../../includes/tsql-md.md)] 标识符的规则。  
  
1.  第一个字符必须是下列字符之一：  
  
    -   Unicode 标准 3.2 定义的字母， Unicode 中定义的字母包括拉丁字符 a-z 和 A-Z，以及来自其他语言的字母字符。  
  
    -   下划线 (_)、at 符号 (@) 或数字符号 (#)。  
  
         在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，某些位于标识符开头位置的符号具有特殊意义。 以 at 符号开头的常规标识符始终表示局部变量或参数，并且不能用作任何其他类型的对象的名称。 以一个数字符号开头的标识符表示临时表或过程。 以两个数字符号 (##) 开头的标识符表示全局临时对象。 虽然数字符号或两个数字符号字符可用作其他类型对象名的开头，但是我们建议不要这样做。  
  
         某些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数的名称以两个 at 符号 (@@) 开头。 为了避免与这些函数混淆，不应使用以 @@ 开头的名称。  
  
2.  后续字符可以包括：  
  
    -   Unicode 标准 3.2 定义的字母。  
  
    -   基本拉丁字符或其他国家/地区字符中的十进制数字。  
  
    -   at 符号、美元符号 ($)、数字符号或下划线。  
  
3.  标识符必须不能是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 保留字。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保留保留字的大写和小写版本。 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用标识符时，不符合这些规则的标识符必须由双引号或括号分隔。 保留字依赖于数据库兼容级别。 可通过使用 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) 语句设置该级别。  
  
4.  不允许嵌入空格或特殊字符。  
  
5.  不允许使用增补字符。  
  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用标识符时，不符合这些规则的标识符必须由双引号或括号分隔。  
  
> [!NOTE]  
>  一些常规标识符格式规则取决于数据库兼容级别。 该级别可以使用 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)设置。  
  
## <a name="see-also"></a>请参阅  
 [ALTER TABLE (Transact-SQL)](/sql/t-sql/statements/alter-table-transact-sql)   
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [CREATE DEFAULT (Transact-SQL)](/sql/t-sql/statements/create-default-transact-sql)   
 [CREATE PROCEDURE (Transact-SQL)](/sql/t-sql/statements/create-procedure-transact-sql)   
 [CREATE RULE (Transact-SQL)](/sql/t-sql/statements/create-rule-transact-sql)   
 [CREATE TABLE (Transact-SQL)](/sql/t-sql/statements/create-table-transact-sql)   
 [CREATE TRIGGER (Transact-SQL)](/sql/t-sql/statements/create-trigger-transact-sql)   
 [CREATE VIEW (Transact-SQL)](/sql/t-sql/statements/create-view-transact-sql)   
 [DECLARE @local_variable (Transact-SQL)](/sql/t-sql/language-elements/declare-local-variable-transact-sql)   
 [DELETE (Transact-SQL)](/sql/t-sql/statements/delete-transact-sql)   
 [INSERT (Transact-SQL)](/sql/t-sql/statements/insert-transact-sql)   
 [保留关键字 (Transact-SQL)](/sql/t-sql/language-elements/reserved-keywords-transact-sql)   
 [SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql)   
 [UPDATE (Transact-SQL)](/sql/t-sql/queries/update-transact-sql)  
  
  
