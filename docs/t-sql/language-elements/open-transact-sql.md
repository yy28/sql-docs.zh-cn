---
title: "打开 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPEN_TSQL
- OPEN
dev_langs: TSQL
helpviewer_keywords:
- opening cursors
- cursors [SQL Server], opening
- populating cursors [SQL Server]
- OPEN statement
- Transact-SQL cursors, opening
ms.assetid: fd1c5e3b-6045-4a42-b646-3fca76e874c1
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: aec83ff9ef56b4d4ae02867d4055d0b1e38f41ec
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="open-transact-sql"></a>OPEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  打开[!INCLUDE[tsql](../../includes/tsql-md.md)]服务器游标通过执行填充游标[!INCLUDE[tsql](../../includes/tsql-md.md)]DECLARE CURSOR 或组上指定语句*cursor_variable*语句。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
OPEN { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>参数  
 GLOBAL  
 指定*cursor_name*指全局游标。  
  
 *cursor_name*  
 已声明的游标的名称。 如果全局和局部游标存在与*cursor_name*作为其名称， *cursor_name*全局是否指定; 否则为是指全局游标*cursor_name*指局部游标。  
  
 *cursor_variable_name*  
 游标变量的名称，该变量引用一个游标。  
  
## <a name="remarks"></a>注释  
 如果使用 INSENSITIVE 或 STATIC 选项声明了游标，那么 OPEN 将创建一个临时表以保留结果集。 如果结果集中任意行的大小超过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表的最大行大小，OPEN 将失败。 如果使用 KEYSET 选项声明了游标，那么 OPEN 将创建一个临时表以保留键集。 临时表存储在 tempdb 中。  
  
 打开一个游标后，使用 @@CURSOR_ROWS函数来接收数符合条件的行中最后一个打开的游标。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持异步生成由键集驱动的或静态的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标操作（如 OPEN 或 FETCH）均为批处理，所以无需异步生成 [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 由于每个游标操作都需要进行客户端往返，因此继续支持异步的由键集驱动的或静态的应用程序编程接口 (API) 服务器游标，对于这些游标，OPEN 实现低延迟时间很重要。  
  
## <a name="examples"></a>示例  
 以下示例打开一个游标并提取所有的行。  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN Employee_Cursor;  
  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM Employee_Cursor  
END;  
  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
```  
  
## <a name="see-also"></a>另请参阅  
 [关闭 &#40;Transact SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [@@CURSOR_ROWS (Transact-SQL)](../../t-sql/functions/cursor-rows-transact-sql.md)   
 [释放 &#40;Transact SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR (Transact-SQL)](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [提取 &#40;Transact SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
