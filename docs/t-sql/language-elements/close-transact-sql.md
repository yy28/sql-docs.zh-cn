---
title: "关闭 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLOSE_TSQL
- CLOSE
dev_langs:
- TSQL
helpviewer_keywords:
- closing cursors
- cursors [SQL Server], closing
- CLOSE statement
ms.assetid: 21546874-97e3-4b93-970f-87c27f6b78c7
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7315b45fa3b13b96fa01c7833ed1370f72e4bab8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="close-transact-sql"></a>CLOSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  释放当前结果集，然后解除定位游标的行上的游标锁定，从而关闭一个开放的游标。 CLOSE 将保留数据结构以便重新打开，但在重新打开游标之前，不允许提取和定位更新。 必须对打开的游标发布 CLOSE；不允许对仅声明或已关闭的游标执行 CLOSE。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CLOSE { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>参数  
 GLOBAL  
 指定*cursor_name*指全局游标。  
  
 *cursor_name*  
 打开的游标的名称。 如果全局和局部游标存在与*cursor_name*作为其名称， *cursor_name*全局时指定; 否则为是指全局游标*cursor_name*指局部游标。  
  
 *cursor_variable_name*  
 与打开的游标关联的游标变量的名称。  
  
## <a name="examples"></a>示例  
 以下示例将显示 `CLOSE` 语句在基于游标的进程中的正确位置。  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT EmployeeID, Title FROM AdventureWorks2012.HumanResources.Employee;  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [游标](../../relational-databases/cursors.md)   
 [游标 (Transact-SQL)](../../t-sql/language-elements/cursors-transact-sql.md)   
 [释放 &#40;Transact SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [提取 &#40;Transact SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [打开 &#40;Transact SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  

