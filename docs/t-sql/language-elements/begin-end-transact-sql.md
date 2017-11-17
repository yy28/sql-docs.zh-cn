---
title: "开始...结束 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
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
- BEGIN
- BEGIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- enclosing statements [SQL Server]
- BEGIN statement
- control-of-flow language [SQL Server], BEGIN...END statement
- BEGIN...END keyword
- grouping statements, BEGIN...END statement
- executing Transact-SQL statements together [SQL Server]
- statements [SQL Server], grouping
ms.assetid: fc2c7f76-f1f9-4f91-beef-bc8ef0da2feb
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1045a89eb41a7f84b4b2a2a5cbe305c67e776fb1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="beginend-transact-sql"></a>BEGIN...END (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  包括一系列的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，从而可以执行一组 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 BEGIN 和 END 是控制流语言的关键字。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
BEGIN  
    { sql_statement | statement_block }   
END  
```  
  
## <a name="arguments"></a>参数  
 { *sql_statement* | *statement_block* }  
 使用语句块定义的任何有效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或语句组。  
  
## <a name="remarks"></a>注释  
 BEGIN...END 语句块允许嵌套。  
  
 虽然所有的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句在 BEGIN...END 块内都有效，但有些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句不应分组在同一批处理或语句块中。  
  
## <a name="examples"></a>示例  
 在下面的示例中，`BEGIN` 和 `END` 定义一系列一起执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 如果不包括 `BEGIN...END` 块，则将执行两个 `ROLLBACK TRANSACTION` 语句，并返回两条 `PRINT` 消息。  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
GO  
IF @@TRANCOUNT = 0  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM Person.Person WHERE LastName = 'Adams';  
    ROLLBACK TRANSACTION;  
    PRINT N'Rolling back the transaction two times would cause an error.';  
END;  
ROLLBACK TRANSACTION;  
PRINT N'Rolled back the transaction.';  
GO  
/*  
Rolled back the transaction.  
*/  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 在下面的示例中，`BEGIN`和`END`定义的一系列[!INCLUDE[DWsql](../../includes/dwsql-md.md)]一起运行的语句。 如果`BEGIN...END`块不包括，下面的示例将在连续循环中。  
  
```  
-- Uses AdventureWorks  
  
DECLARE @Iteration Integer = 0  
WHILE @Iteration <10  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM dbo.DimCustomer WHERE LastName = 'Adams';  
SET @Iteration += 1  
END;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TRIGGER (Transact-SQL)](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [控制流语言 &#40;Transact SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)   
 [结束 &#40;开始...结束 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/end-begin-end-transact-sql.md)  
  
  



