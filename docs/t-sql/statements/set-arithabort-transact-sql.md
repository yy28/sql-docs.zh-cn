---
title: "集 ARITHABORT (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ARITHABORT_TSQL
- ARITHABORT
- SET ARITHABORT
- SET_ARITHABORT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- terminating queries
- queries [SQL Server], terminating
- overflow errors [SQL Server]
- ARITHABORT option
- divide-by-zero errors
- SET ARITHABORT statement
- ending queries [SQL Server]
- stopping queries
ms.assetid: f938a666-fdd1-4233-b97f-719f27b1a0e6
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 97f65f734e68cc0a1ec4c019d50ce72b9c7e1bde
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="set-arithabort-transact-sql"></a>SET ARITHABORT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在查询执行过程中发生溢出或被零除错误时终止查询。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET ARITHABORT { ON | OFF }  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ARITHABORT ON   
[ ; ]  
```  
  
## <a name="remarks"></a>注释  
 在登录会话中，应始终将 ARITHABORT 设置为 ON。 设置 ARITHABORT 为 OFF 可以产生负面影响查询优化的性能问题。  
  
> [!WARNING]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的默认 ARITHABORT 设置为 ON。 客户端应用程序将 ARITHABORT 设置为 OFF 可以接收不同的查询计划，使得对性能较差的查询进行故障排除变得困难。 即，同一个查询可以在 Management Studio 中快速执行，但在应用程序中却比较慢。 使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 排除查询故障时始终与客户端 ARITHABORT 设置匹配。  
  
 如果 SET ARITHABORT 为 ON，并且 SET ANSI WARNINGS 也为 ON，则这些错误情况将导致查询终止。  
  
 如果 SET ARITHABORT 为 ON，但 SET ANSI WARNINGS 为 OFF，则这些错误情况将导致批处理终止。 如果在事务内发生错误，则回滚事务。 如果 SET ARITHABORT 为 OFF 并且发生了这些错误之一，则显示一条警告消息，并将 NULL 赋予算术运算的结果。  
  
 如果 SET ARITHABORT 和 SET ANSI WARNINGS 为 OFF 并且发生了这些错误之一，则显示一条警告消息，并将 NULL 赋给算术运算的结果。  
  
> [!NOTE]  
>  如果 SET ARITHABORT 和 SET ARITHIGNORE 都没有设置，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将在执行查询后返回 NULL 和一条警告消息。  
  
 当数据库兼容级别设置为 90 或更高时，如果将 ANSI_WARNINGS 设置为 ON，则将使 ARITHABORT 隐式设置为 ON。 如果数据库兼容级别设置为 80 或更低，则必须将 ARITHABORT 选项显式设置为 ON。  
  
 如果 SET ARITHABORT 为 OFF，并且在对表达式求值的过程中 INSERT、DELETE 或 UPDATE 语句遇到算术错误（溢出、被零除或域错误），[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将插入或更新一个 NULL 值。 如果目标列不可为空，则插入或更新操作将失败，用户将收到错误消息。  
  
 如果 SET ARITHABORT 或 SET ARITHIGNORE 为 OFF，而 SET ANSI_WARNINGS 为 ON，则遇到被零除或溢出错误时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仍会返回错误消息。  
  
 如果 SET ARITHABORT 设置为 OFF，并且对 IF 语句的 Boolean 条件求值过程中发生中止错误，则将执行 FALSE 分支。  
  
 在对计算列或索引视图创建或更改索引时，SET ARITHABORT 必须为 ON。 如果 SET ARITHABORT 为 OFF，则对包含计算列或索引视图索引的表执行 CREATE、UPDATE、INSERT 和 DELETE 语句时将失败。  
  
 SET ARITHABORT 的设置是在执行或运行时设置的，而不是在分析时设置的。  
  
 要查看此设置的当前设置，请运行以下查询。  
  
```  
DECLARE @ARITHABORT VARCHAR(3) = 'OFF';  
IF ( (64 & @@OPTIONS) = 64 ) SET @ARITHABORT = 'ON';  
SELECT @ARITHABORT AS ARITHABORT;  
  
```  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 下例说明了在两种 `SET ARITHABORT` 设置下的被零除错误和溢出错误。  
  
```  
-- SET ARITHABORT  
-------------------------------------------------------------------------------  
-- Create tables t1 and t2 and insert data values.  
CREATE TABLE t1 (  
   a TINYINT,   
   b TINYINT  
);  
CREATE TABLE t2 (  
   a TINYINT  
);  
GO  
INSERT INTO t1   
VALUES (1, 0);  
INSERT INTO t1   
VALUES (255, 1);  
GO  
  
PRINT '*** SET ARITHABORT ON';  
GO  
-- SET ARITHABORT ON and testing.  
SET ARITHABORT ON;  
GO  
  
PRINT '*** Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab   
FROM t1;  
GO  
  
PRINT '*** Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
  
PRINT '*** Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '*** Resulting data - should be no data';  
GO  
SELECT *   
FROM t2;  
GO  
  
-- Truncate table t2.  
TRUNCATE TABLE t2;  
GO  
  
-- SET ARITHABORT OFF and testing.  
PRINT '*** SET ARITHABORT OFF';  
GO  
SET ARITHABORT OFF;  
GO  
  
-- This works properly.  
PRINT '*** Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab    
FROM t1;  
GO  
  
-- This works as if SET ARITHABORT was ON.  
PRINT '*** Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
PRINT '*** Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '*** Resulting data - should be 0 rows';  
GO  
SELECT *   
FROM t2;  
GO  
  
-- Drop tables t1 and t2.  
DROP TABLE t1;  
DROP TABLE t2;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [设置 ARITHIGNORE &#40;Transact SQL &#41;](../../t-sql/statements/set-arithignore-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  

