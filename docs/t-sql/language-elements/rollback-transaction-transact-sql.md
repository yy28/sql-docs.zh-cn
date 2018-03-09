---
title: "ROLLBACK TRANSACTION (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROLLBACK TRANSACTION
- ROLLBACK
- ROLLBACK_TSQL
- ROLLBACK_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- ROLLBACK TRANSACTION statement
- erasing data modifications [SQL Server]
- rolling back transactions, ROLLBACK TRANSACTION
- roll back transactions [SQL Server]
- savepoints [SQL Server]
ms.assetid: 6882c5bc-ff74-476a-984b-164aeb036c66
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0df2fdf3d3e4aa7915fbfef3ff921d12b2851044
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="rollback-transaction-transact-sql"></a>ROLLBACK TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  将显式事务或隐性事务回滚到事务的起点或事务内的某个保存点。 可以使用 ROLLBACK TRANSACTION 清除自事务的起点或到某个保存点所做的所有数据修改。 它还释放由事务控制的资源。  
  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ROLLBACK { TRAN | TRANSACTION }   
     [ transaction_name | @tran_name_variable  
     | savepoint_name | @savepoint_variable ]   
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *transaction_name*  
 是为 BEGIN TRANSACTION 上的事务分配的名称。 *transaction_name*必须符合标识符规则，但使用只有事务名称的前 32 个字符。 当嵌套事务， *transaction_name*必须是从最外面的 BEGIN TRANSACTION 语句的名称。 *transaction_name*始终是区分大小写，即使实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不区分大小写。  
  
 **@** *tran_name_variable*  
 用户定义的、含有有效事务名称的变量的名称。 必须使用声明变量**char**， **varchar**， **nchar**，或**nvarchar**数据类型。  
  
 *savepoint_name*  
 是*savepoint_name*从 SAVE TRANSACTION 语句。 *savepoint_name*必须符合标识符的规则。 使用*savepoint_name*条件回滚时应影响仅事务的一部分。  
  
 **@** *savepoint_variable*  
 是用户定义的、包含有效保存点名称的变量的名称。 必须使用声明变量**char**， **varchar**， **nchar**，或**nvarchar**数据类型。  
  
## <a name="error-handling"></a>错误处理  
 ROLLBACK TRANSACTION 语句不生成显示给用户的消息。 如果在存储过程或触发器中需要警告，请使用 RAISERROR 或 PRINT 语句。 RAISERROR 是用于指出错误的首选语句。  
  
## <a name="general-remarks"></a>一般备注  
 回滚事务，而无需*savepoint_name*或*transaction_name*回滚到事务开始。 嵌套事务时，该语句将所有内层事务回滚到最外面的 BEGIN TRANSACTION 语句。 在这两种情况下，ROLLBACK TRANSACTION 递减 @@TRANCOUNT为 0 的系统函数。 ROLLBACK TRANSACTION *savepoint_name*没有减少@TRANCOUNT。  
  
 不能引用 ROLLBACK TRANSACTION *savepoint_name*在分布式事务中显式使用开始分布式事务启动或从本地事务升级。  
  
 在执行 COMMIT TRANSACTION 语句后不能回滚事务，但是 COMMIT TRANSACTION 与包含在要回滚的事务中的嵌套事务关联时除外。 在此情况下，将嵌套的事务将回滚，即使已为其发出 COMMIT TRANSACTION。  
  
 在事务内允许有重复的保存点名称，但如果 ROLLBACK TRANSACTION 使用重复的保存点名称，则只回滚到最近的使用该保存点名称的 SAVE TRANSACTION。  
  
## <a name="interoperability"></a>互操作性  
 在存储过程中，而无需 ROLLBACK TRANSACTION 语句*savepoint_name*或*transaction_name*回滚到最外层的 BEGIN TRANSACTION 的所有语句。 中的存储过程的 @ 导致的 ROLLBACK TRANSACTION 语句@TRANCOUNT要具有不同的值，当存储的过程完成后比 @@TRANCOUNT值调用存储的过程时将产生一条信息性消息。 该信息不影响后面的处理。  
  
 如果在触发器中发出 ROLLBACK TRANSACTION：  
  
-   将回滚对当前事务中的那一点所做的所有数据修改，包括触发器所做的修改。  
  
-   触发器继续执行 ROLLBACK 语句之后的所有其余语句。 如果这些语句中的任意语句修改数据，则不回滚这些修改。 执行其余的语句不会激发嵌套触发器。  
  
-   在批处理中，不执行所有位于激发触发器的语句之后的语句。  
  
@@TRANCOUNT就会递增 1 时输入了触发器，即使是在自动提交模式。 （系统将触发器视为隐含的嵌套事务处理。）  
  
在存储过程中，ROLLBACK TRANSACTION 语句不影响调用该过程的批处理中的后续语句；将执行批处理中的后续语句。 在触发器中，ROLLBACK TRANSACTION 语句终止包含激发触发器的语句的批处理；不执行批处理中的后续语句。  
  
ROLLBACK 对游标的影响由下面三个规则定义：  
  
1.  当 CURSOR_CLOSE_ON_COMMIT 设置为 ON 时，ROLLBACK 关闭但不释放所有打开的游标。  
  
2.  当 CURSOR_CLOSE_ON_COMMIT 设置为 OFF 时，ROLLBACK 不影响任何打开的同步 STATIC 或 INSENSITIVE 游标，也不影响已完全填充的异步 STATIC 游标。 将关闭但不释放任何其他类型的打开的游标。  
  
3.  终止批处理并生成内部回滚的错误将释放在包含错误声明的批处理中声明的所有游标。 将释放所有游标，而不考虑它们的类型或 CURSOR_CLOSE_ON_COMMIT 的设置情况。 这包括在错误批处理调用的存储过程中声明的游标。 在错误批处理之前的批处理中声明的游标遵循规则 1 和 2。 死锁错误便是此类错误的一个示例。 在触发器中发出的 ROLLBACK 语句也将自动生成此类错误。  
  
## <a name="locking-behavior"></a>锁定行为  
 ROLLBACK TRANSACTION 语句指定*savepoint_name*释放超出的保存点，但升级和转换除外获取任何锁。 这些锁不会被释放，而且不会转换回先前的锁模式。  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例显示了回滚已命名事务的效果。 在创建表，以下语句将启动指定的事务，插入两行，并且然后回滚事务，在变量中名为@TransactionName。 在指定的事务之外的另一个语句中插入两行。 查询返回前面的语句的结果。   
  
```sql    
USE tempdb;  
GO  
CREATE TABLE ValueTable ([value] int);  
GO  
  
DECLARE @TransactionName varchar(20) = 'Transaction1';  
  
BEGIN TRAN @TransactionName  
       INSERT INTO ValueTable VALUES(1), (2);  
ROLLBACK TRAN @TransactionName;  
  
INSERT INTO ValueTable VALUES(3),(4);  
  
SELECT [value] FROM ValueTable;  
  
DROP TABLE ValueTable;  
```  
[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]  
```  
value  
-----   
3    
4  
```  
  
  
## <a name="see-also"></a>另请参阅  
 [BEGIN DISTRIBUTED TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION (Transact-SQL)](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [提交工作 &#40;Transact SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [回滚工作 &#40;Transact SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION (Transact-SQL)](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  
