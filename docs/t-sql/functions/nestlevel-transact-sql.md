---
title: "@@NESTLEVEL (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@NESTLEVEL'
- '@@NESTLEVEL_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@NESTLEVEL function'
- nesting stored procedures
- stored procedure nesting levels [SQL Server]
ms.assetid: 8c0b2134-8616-44f6-addc-6583c432fb62
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 4945bbe718bd8561100a3dd8e296a9f1faa9d93a
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="x40x40nestlevel-transact-sql"></a>&#x40;&#x40; NESTLEVEL (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回在本地服务器上执行的当前存储过程的嵌套级别（初始值为 0）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@NESTLEVEL  
```  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>注释  
 每次一个存储过程通过引用公共语言运行时 (CLR) 例程、类型或聚合来调用另一个存储过程或执行托管代码时，嵌套级别都会增加。 超过最大级数 32 时，事务即被终止。  
  
 当 @@NESTLEVEL 中执行[!INCLUDE[tsql](../../includes/tsql-md.md)]字符串，则返回值 1 + 当前嵌套级别。 当 @@NESTLEVEL 执行动态通过使用 sp_executesql 返回的值是 2 + 的当前嵌套级别。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-nestlevel-in-a-procedure"></a>A. 使用 @@NESTLEVEL 在过程中  
 以下示例将创建两个过程：一个过程调用另一个过程，一个过程显示每个过程的 `@@NESTLEVEL` 设置。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'usp_OuterProc', N'P')IS NOT NULL  
    DROP PROCEDURE usp_OuterProc;  
GO  
IF OBJECT_ID (N'usp_InnerProc', N'P')IS NOT NULL  
    DROP PROCEDURE usp_InnerProc;  
GO  
CREATE PROCEDURE usp_InnerProc AS   
    SELECT @@NESTLEVEL AS 'Inner Level';  
GO  
CREATE PROCEDURE usp_OuterProc AS   
    SELECT @@NESTLEVEL AS 'Outer Level';  
    EXEC usp_InnerProc;  
GO  
EXECUTE usp_OuterProc;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Outer Level  
-----------  
1  
  
Inner Level  
-----------  
2
```  
  
### <a name="b-calling-nestlevel"></a>B. 调用 @@NESTLEVEL   
 下面的示例演示返回的值之间的差异`SELECT`， `EXEC`，和`sp_executesql`当每个调用`@@NESTLEVEL`。  
  
```  
CREATE PROC usp_NestLevelValues AS  
    SELECT @@NESTLEVEL AS 'Current Nest Level';  
EXEC ('SELECT @@NESTLEVEL AS OneGreater');   
EXEC sp_executesql N'SELECT @@NESTLEVEL as TwoGreater' ;  
GO  
EXEC usp_NestLevelValues;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Current Nest Level  
------------------  
1  
  
(1 row(s) affected)  
  
OneGreater  
-----------  
2  
  
(1 row(s) affected)  
  
TwoGreater  
-----------  
3  
  
(1 row(s) affected)
```  
  
## <a name="see-also"></a>另请参阅  
 [配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [创建存储过程](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [@@TRANCOUNT (Transact-SQL)](../../t-sql/functions/trancount-transact-sql.md)  
  
  

