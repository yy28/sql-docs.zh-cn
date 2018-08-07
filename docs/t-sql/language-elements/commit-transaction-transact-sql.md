---
title: COMMIT TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COMMIT
- COMMIT TRANSACTION
- COMMIT_TSQL
- COMMIT_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- user-defined transactions [SQL Server]
- committed transactions
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- implicit transactions
- distributed transactions [SQL Server], committed
- transactions [SQL Server], committed
- COMMIT TRANSACTION statement
- rolling back transactions, COMMIT TRANSACTION
ms.assetid: f8fe26a9-7911-497e-b348-4e69c7435dc1
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 65e2a3aab16232dfefdb6429c690da2712ab4b5e
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39453274"
---
# <a name="commit-transaction-transact-sql"></a>COMMIT TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  标志一个成功的隐性事务或显式事务的结束。 如果 @@TRANCOUNT 为 1，COMMIT TRANSACTION 使得自从事务开始以来所执行的所有数据修改成为数据库的永久部分，释放事务所占用的资源，并将 @@TRANCOUNT 减少到 0。 如果 @@TRANCOUNT 大于 1，则 COMMIT TRANSACTION 使 @@TRANCOUNT 按 1 递减并且事务将保持活动状态。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Applies to SQL Server (starting with 2008) and Azure SQL Database
  
COMMIT [ { TRAN | TRANSACTION }  [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]  
[ ; ]  
```  
 
```  
-- Applies to Azure SQL Data Warehouse and Parallel Data Warehouse Database
  
COMMIT [ TRAN | TRANSACTION ] 
[ ; ]  
``` 
 
  
## <a name="arguments"></a>参数  
 transaction_name  
 适用范围：SQL Server 和 Azure SQL 数据库
 
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]忽略此参数。 transaction_name 指定由前面的 BEGIN TRANSACTION 分配的事务名称。 transaction_name 必须符合标识符规则，但不能超过 32 个字符。 transaction_name 通过向程序员指明 COMMIT TRANSACTION 与哪些 BEGIN TRANSACTION 相关联，可作为帮助阅读的一种方法。  
  
 *@tran_name_variable*  
 适用范围：SQL Server 和 Azure SQL 数据库  
 
用户定义的、含有有效事务名称的变量的名称。 必须使用 char、varchar、nchar 或 nvarchar 数据类型声明该变量。 如果传递给该变量的字符数超过 32，则只使用 32 个字符，其余的字符将被截断。  
  
 DELAYED_DURABILITY  
 适用范围：SQL Server 和 Azure SQL 数据库   

 请求将此事务与延迟持续性一起提交的选项。 如果已用 `DELAYED_DURABILITY = DISABLED` 或 `DELAYED_DURABILITY = FORCED` 更改了数据库，则忽略该请求。 有关详细信息，请参阅主题[控制事务持续性](../../relational-databases/logs/control-transaction-durability.md)。  
  
## <a name="remarks"></a>Remarks  
 仅当事务引用的所有数据在逻辑上都正确时，[!INCLUDE[tsql](../../includes/tsql-md.md)] 程序员才应发出 COMMIT TRANSACTION 命令。  
  
 如果所提交的事务是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 分布式事务，COMMIT TRANSACTION 将触发 MS DTC 使用两阶段提交协议，以便提交所有涉及该事务的服务器。 如果本地事务跨越同一[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例上的两个或多个数据库，则该实例将使用内部的两阶段提交来提交所有涉及该事务的数据库。  
  
 当在嵌套事务中使用时，内部事务的提交并不释放资源或使其修改成为永久修改。 只有在提交了外部事务时，数据修改才具有永久性，而且资源才会被释放。 当 @@TRANCOUNT 大于 1 时，每发出一个 COMMIT TRANSACTION 命令只会使 @@TRANCOUNT 按 1 递减。 当 @@TRANCOUNT 最终递减为 0 时，将提交整个外部事务。 因为 transaction_name 被 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 忽略，所以当存在显著内部事务时，发出一个引用外部事务名称的 COMMIT TRANSACTION 只会使 @@TRANCOUNT 按 1 递减。  
  
 当 @@TRANCOUNT 为 0 时发出 COMMIT TRANSACTION 将会导致出现错误；因为没有相应的 BEGIN TRANSACTION。  
  
 不能在发出一个 COMMIT TRANSACTION 语句之后回滚事务，因为数据修改已经成为数据库的一个永久部分。  
  
 仅当事务计数在语句开始处为 0 时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]才会增加语句内的事务计数。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-committing-a-transaction"></a>A. 提交事务  
适用范围：SQL Server、Azure SQL 数据库、Azure SQL 数据仓库和并行数据仓库   

以下示例删除候选作业。 它使用 AdventureWorks。 
  
```   
BEGIN TRANSACTION;   
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;   
COMMIT TRANSACTION;   
```  
  
### <a name="b-committing-a-nested-transaction"></a>B. 提交嵌套事务  
适用范围：SQL Server 和 Azure SQL 数据库    

下面的示例创建一个表，生成三个级别的嵌套事务，然后提交该嵌套事务。 虽然每个 `COMMIT TRANSACTION` 语句都具有一个 transaction_name 参数，但 `COMMIT TRANSACTION` 与 `BEGIN TRANSACTION` 语句之间没有关系。 transaction_name 参数仅是帮助阅读的方法，可帮助程序员确保提交的正确号码被编码以便将 `@@TRANCOUNT` 减少到 0，从而提交外部事务。 
  
```   
IF OBJECT_ID(N'TestTran',N'U') IS NOT NULL  
    DROP TABLE TestTran;  
GO  
CREATE TABLE TestTran (Cola int PRIMARY KEY, Colb char(3));  
GO  
-- This statement sets @@TRANCOUNT to 1.  
BEGIN TRANSACTION OuterTran;  
  
PRINT N'Transaction count after BEGIN OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
INSERT INTO TestTran VALUES (1, 'aaa');  
 
-- This statement sets @@TRANCOUNT to 2.  
BEGIN TRANSACTION Inner1;  
 
PRINT N'Transaction count after BEGIN Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (2, 'bbb');  
  
-- This statement sets @@TRANCOUNT to 3.  
BEGIN TRANSACTION Inner2;  
  
PRINT N'Transaction count after BEGIN Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
INSERT INTO TestTran VALUES (3, 'ccc');  
  
-- This statement decrements @@TRANCOUNT to 2.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner2;  
 
PRINT N'Transaction count after COMMIT Inner2 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
 
-- This statement decrements @@TRANCOUNT to 1.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner1;  
 
PRINT N'Transaction count after COMMIT Inner1 = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
  
-- This statement decrements @@TRANCOUNT to 0 and  
-- commits outer transaction OuterTran.  
COMMIT TRANSACTION OuterTran;  
  
PRINT N'Transaction count after COMMIT OuterTran = '  
    + CAST(@@TRANCOUNT AS nvarchar(10));  
```  
  
## <a name="see-also"></a>另请参阅  
 [BEGIN DISTRIBUTED TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT WORK (Transact-SQL)](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION (Transact-SQL)](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK (Transact-SQL)](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION (Transact-SQL)](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT (Transact-SQL)](../../t-sql/functions/trancount-transact-sql.md)  
  
  
