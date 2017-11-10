---
title: "@@IDENTITY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@IDENTITY_TSQL'
- '@@IDENTITY'
dev_langs:
- TSQL
helpviewer_keywords:
- last-inserted identity values
- identity values [SQL Server], last-inserted
- '@@IDENTITY function'
ms.assetid: 912e4485-683c-41c2-97b3-8831c0289ee4
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 88cdaa1362e5d60b0f880c66c7fb7038ddb9f126
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40identity-transact-sql"></a>&#x40;&#x40; 标识 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回最后插入的标识值的系统函数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@IDENTITY  
```  
  
## <a name="return-types"></a>返回类型  
 **numeric(38,0)**  
  
## <a name="remarks"></a>注释  
 完成后插入、 SELECT INTO 或大容量复制语句，@@IDENTITY包含语句生成的最后一个标识值。 如果语句未影响任何表与标识列，@IDENTITY返回 NULL。 如果插入多个行时，生成多个标识值，@IDENTITY返回生成的最后一个标识值。 如果语句激发执行生成标识值的插入的一个或多个触发器，则调用@IDENTITY语句立即返回生成的触发器的最后一个标识值后。 如果在具有标识列的表上的某个插入操作后激发了触发器和 @ 没有标识列，另一个表中插入触发器@IDENTITY返回第一次插入的标识值。 @@IDENTITY值不会恢复到上一个设置，如果 INSERT 或 SELECT INTO 语句或大容量复制失败，或者如果回滚事务。  
  
 如果语句和事务失败，它们会更改表的当前标识，从而使标识列中的值出现不连贯现象。 即使未提交试图向表中插入值的事务，也永远无法回滚标识值。 例如，如果因 IGNORE_DUP_KEY 冲突而导致 INSERT 语句失败，表的当前标识值仍然会增加。  
  
 @@IDENTITY，SCOPE_IDENTITY 和 IDENT_CURRENT 是类似的功能，因为它们都返回插入到标识列的表的最后一个值。  
  
 @@IDENTITY和 SCOPE_IDENTITY 返回在当前会话中任何表中生成的最后一个标识值。 但是，SCOPE_IDENTITY 返回的值仅在当前作用域;@@IDENTITY并不局限于特定的作用域。  
  
 IDENT_CURRENT 不受作用域和会话的限制，而受限于指定的表。 IDENT_CURRENT 可以返回任何会话和任何作用域中为特定表生成的标识值。 有关详细信息，请参阅[IDENT_CURRENT &#40;Transact SQL &#41;](../../t-sql/functions/ident-current-transact-sql.md).  
  
 作用域 @@IDENTITY函数是在其执行本地服务器上的当前会话。 此函数不能应用于远程或链接服务器。 若要获得其他服务器上的标识值，请在远程服务器或链接服务器上执行存储过程，并使（在远程或链接服务器的环境中执行的）该存储过程收集标识值，并将其返回本地服务器上的发出调用的连接。  
  
 复制可能会影响 @@IDENTITY值，因为它正在使用中的复制触发器和存储的过程。 @@IDENTITY不是最新的用户创建标识的可靠指示器，如果列是复制项目的一部分。 你可以使用 scope_identity （） 函数的语法而不是 @@IDENTITY。 有关详细信息，请参阅[SCOPE_IDENTITY &#40;Transact SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)  
  
> [!NOTE]  
>  调用存储过程或[!INCLUDE[tsql](../../includes/tsql-md.md)]必须重写语句以使用`SCOPE_IDENTITY()`函数，返回该 user 语句、 作用域内使用的最新标识和不使用嵌套触发器的作用域内标识复制。  
  
## <a name="examples"></a>示例  
 以下示例向包含标识列 (`LocationID`) 的表中插入一行，并使用 `@@IDENTITY` 显示新行中使用的标识值。  
  
```  
USE AdventureWorks2012;  
GO  
--Display the value of LocationID in the last row in the table.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
INSERT INTO Production.Location (Name, CostRate, Availability, ModifiedDate)  
VALUES ('Damaged Goods', 5, 2.5, GETDATE());  
GO  
SELECT @@IDENTITY AS 'Identity';  
GO  
--Display the value of LocationID of the newly inserted row.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [System Functions (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)  
  
  

