---
title: "结束 （开始...结束） (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- END
- END_TSQL
dev_langs: TSQL
helpviewer_keywords:
- enclosing statements [SQL Server]
- END keyword
- BEGIN...END keyword
- END (BEGIN...END) keyword
ms.assetid: 354c4935-1375-4141-8195-61326662f4d2
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e15aaa9fc6d4ea9b3c8a3c8b89826c85f0a4810f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="end-beginend-transact-sql"></a>END (BEGIN...END) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  括号中包含一系列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，这些语句作为一个组执行。 BEGIN...END 语句块允许嵌套。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
BEGIN   
     { sql_statement | statement_block }   
END   
```  
  
## <a name="arguments"></a>参数  
 { *sql_statement*| *statement_block*}  
 任何有效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或用语句块定义的语句分组。 若要定义语句块（批处理），请使用控制流语言关键字 BEGIN 和 END。 虽然所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句在 BEGIN...END 块内都有效，但有些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句不能组合到同一个批（语句块）中。  
  
## <a name="result-types"></a>结果类型  
 **Boolean**  
  
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
 [开始...结束 &#40;Transact SQL &#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [控制流语言 &#40;Transact SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)   
 [其他 &#40; 如果...其他 &#41;&#40;Transact SQL &#41;](../../t-sql/language-elements/else-if-else-transact-sql.md)   
 [如果...其他 &#40;Transact SQL &#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [WHILE (Transact-SQL)](../../t-sql/language-elements/while-transact-sql.md)  
  
  


