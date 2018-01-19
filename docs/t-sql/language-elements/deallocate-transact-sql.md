---
title: "释放 (Transact SQL) |Microsoft 文档"
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
- DEALLOCATE
- DEALLOCATE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- locking [SQL Server], cursors
- DEALLOCATE statement
- deallocations [SQL Server]
- deleting cursor references
- removing cursor references
ms.assetid: c75cf73d-0268-4c57-973d-b8a84ff801fa
caps.latest.revision: "26"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f7dd1a4deca2a3c6db7db7596c94f0def97934da
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="deallocate-transact-sql"></a>DEALLOCATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  删除游标引用。 包含光标的数据结构时的最后一个光标引用被释放时，将通过释放[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DEALLOCATE { { [ GLOBAL ] cursor_name } | @cursor_variable_name }  
```  
  
## <a name="arguments"></a>参数  
 *cursor_name*  
 已声明游标的名称。 全局和局部游标是否存在与*cursor_name*作为其名称， *cursor_name*引用到全局游标如果指定全局和局部游标，如果未指定全局。  
  
 @*cursor_variable_name*  
 是的名称**光标**变量。 @*cursor_variable_name*的类型必须为**光标**。  
  
## <a name="remarks"></a>注释  
 对游标进行操作的语句使用游标名称或游标变量引用游标。 DEALLOCATE 删除游标与游标名称或游标变量之间的关联。 如果一个名称或变量是最后引用游标的名称或变量，则将释放游标，游标使用的任何资源也随之释放。 用于保护提取隔离的滚动锁在 DEALLOCATE 上释放。 用于保护更新（包括通过游标进行的定位更新）的事务锁一直到事务结束才释放。  
  
 DECLARE CURSOR 语句分配游标并将其与游标名称关联。  
  
```  
DECLARE abc SCROLL CURSOR FOR  
SELECT * FROM Person.Person;  
```  
  
 游标名称与某个游标关联之后，该名称在游标释放之前不能用作相同作用域（GLOBAL 或 LOCAL）内另一个游标的名称。  
  
 游标变量使用下列两种方法之一与游标关联：  
  
-   通过名称，使用 SET 语句将游标设置为游标变量。  
  
    ```  
    DECLARE @MyCrsrRef CURSOR;  
    SET @MyCrsrRef = abc;  
    ```  
  
-   也可以不定义游标名称而创建游标并将其与变量关联。  
  
    ```  
    DECLARE @MyCursor CURSOR;  
    SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Person.Person;  
    ```  
  
 @ 释放*cursor_variable_name*语句中删除仅引用的已命名的变量到光标处。 直到批处理、存储过程或触发器结束时变量离开作用域，才释放变量。 @ 释放后*cursor_variable_name*语句，该变量可以与相关联使用 SET 语句的另一个游标。  
  
```  
USE AdventureWorks2012;  
GO  
  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
  
DEALLOCATE @MyCursor;  
  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
    SELECT * FROM Sales.SalesTerritory;  
GO  
```  
  
 不必显式释放游标变量。 变量在离开作用域时被隐式释放。  
  
## <a name="permissions"></a>权限  
 默认情况下，将 DEALLOCATE 权限授予任何有效用户。  
  
## <a name="examples"></a>示例  
 以下脚本显示如何游标存留直到最后一个名称，或直到已释放引用它们的变量。  
  
```  
USE AdventureWorks2012;  
GO  
-- Create and open a global named cursor that  
-- is visible outside the batch.  
DECLARE abc CURSOR GLOBAL SCROLL FOR  
    SELECT * FROM Sales.SalesPerson;  
OPEN abc;  
GO  
-- Reference the named cursor with a cursor variable.  
DECLARE @MyCrsrRef1 CURSOR;  
SET @MyCrsrRef1 = abc;  
-- Now deallocate the cursor reference.  
DEALLOCATE @MyCrsrRef1;  
-- Cursor abc still exists.  
FETCH NEXT FROM abc;  
GO  
-- Reference the named cursor again.  
DECLARE @MyCrsrRef2 CURSOR;  
SET @MyCrsrRef2 = abc;  
-- Now deallocate cursor name abc.  
DEALLOCATE abc;  
-- Cursor still exists, referenced by @MyCrsrRef2.  
FETCH NEXT FROM @MyCrsrRef2;  
-- Cursor finally is deallocated when last referencing  
-- variable goes out of scope at the end of the batch.  
GO  
-- Create an unnamed cursor.  
DECLARE @MyCursor CURSOR;  
SET @MyCursor = CURSOR LOCAL SCROLL FOR  
SELECT * FROM Sales.SalesTerritory;  
-- The following statement deallocates the cursor  
-- because no other variables reference it.  
DEALLOCATE @MyCursor;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [游标](../../relational-databases/cursors.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [提取 &#40;Transact SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [打开 &#40;Transact SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
