---
title: "事务 （SQL 数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4ea7244857dcd25b1e36f3420811ef035d4ee3b2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="transactions-sql-data-warehouse"></a>事务 （SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  事务是一组的一个或多个数据库语句，完全提交或全部回滚。 每个事务是原子、 一致、 隔离和持久 (ACID)。 如果事务成功，其中的所有语句不都会提交。 如果事务失败，这是至少其中一个组中的语句失败，则将回滚整个组。  
  
 开头和结尾的事务依赖于自动提交设置和 BEGIN TRANSACTION、 提交和回滚语句。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]支持以下类型的事务：  
  
-   *显式事务*开头的 BEGIN TRANSACTION 语句和 with 提交或回滚语句的结尾。  
  
-   *自动提交事务*在会话中自动启动并不会启动与 BEGIN TRANSACTION 语句。 当自动提交设置为 ON 时，每个语句在事务中运行，并是必需的任何显式提交或回滚。 当自动提交设置为 OFF 时，提交或回滚语句需要确定事务的结果。 在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，自动提交事务开始后立即提交或回滚语句中，或将自动提交 SET OFF 语句后面。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
BEGIN TRANSACTION [;]  
COMMIT [ TRAN | TRANSACTION | WORK ] [;]  
ROLLBACK [ TRAN | TRANSACTION | WORK ] [;]  
SET AUTOCOMMIT { ON | OFF } [;]  
SET IMPLICIT_TRANSACTIONS { ON | OFF } [;]  
```  
  
## <a name="arguments"></a>参数  
 BEGIN TRANSACTION  
 标记的显式事务的起始点。  
  
 提交 [工作]  
 将标记的末尾显式或自动提交事务。 此语句导致要将其永久提交到数据库的事务中所做的更改。 语句提交到提交工作、 COMMIT TRAN 和 COMMIT TRANSACTION 等同。  
  
 回滚 [工作]  
 事务回滚到事务开始。 提交到数据库不进行事务的任何更改。 语句回滚等同于回滚工作、 ROLLBACK TRAN 和 ROLLBACK TRANSACTION。  
  
 集自动提交 { **ON** |关闭}  
 确定如何启动和结束事务。  
  
 ON  
 每个语句在其自己的事务下运行，需要执行任何显式提交或回滚语句。 当自动提交为 ON 时允许显式事务。  
  
 OFF  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]事务不已正在进行时，会自动启动事务。 作为事务的一部分运行任何后续的语句和提交或回滚有必要确定事务的结果。 一旦提交或回滚在此模式下操作的事务，模式依然是 OFF，和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]启动新的事务。 自动提交为 OFF 时，不允许显式事务。  
  
 如果你更改在活动事务中的自动提交设置，设置会影响当前事务，并且事务完成之前将不会影响。  
  
 如果自动提交为 ON 时，运行另一个集自动提交 ON 语句将不起作用。 同样，如果自动提交为 OFF，运行另一个 SET 自动提交 OFF 将不起作用。  
  
 设置 IMPLICIT_TRANSACTIONS {ON |**OFF** }  
 这会切换为设置自动提交的相同模式。 如果设置为 ON，SET IMPLICIT_TRANSACTIONS 将连接设置为隐式事务模式。 当关闭，它将连接返回到自动提交模式。  有关详细信息，请参阅[SET IMPLICIT_TRANSACTIONS &#40;Transact SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## <a name="permissions"></a>权限  
 运行与事务相关的语句需要不特定的权限。 运行事务内的语句所需的权限。  
  
## <a name="error-handling"></a>错误处理  
 如果运行提交或回滚，并且没有活动事务，将引发错误。  
  
 如果事务已正在进行时运行 BEGIN TRANSACTION，则，引发错误。 如果 BEGIN TRANSACTION 发生成功的 BEGIN TRANSACTION 语句之后或在自动提交设置关闭会话时便会出现此问题。  
  
 如果运行时语句错误以外的错误禁止的显式事务成功完成[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]自动回滚事务，并释放事务所持有的所有资源。 例如，如果客户端的网络连接到的实例[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]已损坏或客户端注销应用程序、 网络通知的中断的实例时，将回滚任何未提交的事务的连接。  
  
 如果运行时语句错误发生在一个批处理，[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]行为与一致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **XACT_ABORT**设置为**ON**和回滚整个事务。 有关详细信息**XACT_ABORT**设置，请参阅[设置 XACT_ABORT (Transact SQL)](http://msdn.microsoft.com/library/ms188792.aspx)。  
  
## <a name="general-remarks"></a>一般备注  
 会话在给定的时间; 只能运行一个事务不支持保存点和嵌套的事务。  
  
 它负责[!INCLUDE[DWsql](../../includes/dwsql-md.md)]程序员的点处仅发出提交时事务所引用的所有数据是逻辑上正确。  
  
 当事务完成之前，已终止会话时，将回滚事务。  
  
 在会话级别管理事务模式。 例如，如果一个会话开始的显式事务，或将自动提交设置为 OFF，或将 IMPLICIT_TRANSACTIONS 设置为 ON，它具有不会影响任何其他会话的事务模式。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 因为数据进行了修改数据库的永久部分发出 COMMIT 语句后，你不能回滚事务。  
  
 [创建数据库 &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)和[删除数据库 &#40;Transact SQL &#41;](../../t-sql/statements/drop-database-transact-sql.md)命令不能用到显式事务。  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]没有共享机制事务。 这意味着，在任何给定时间点，只有一个会话可以处理任何事务系统中。  
  
## <a name="locking-behavior"></a>锁定行为  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]锁定，以确保事务完整性和维护的数据库的一致性，在多个用户同时访问数据时使用。 隐式和显式事务使用锁定。 每个事务请求上的资源，例如表或数据库事务依赖的不同类型的锁。 所有[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]锁是表级别或更高版本。 锁可以阻止其他事务以某种可能会导致事务请求锁出错的方式修改资源。 每个事务释放其锁定，当它不再具有依赖锁定的资源;显式事务保留锁，直到事务完成时它是已提交或回滚。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>A. 使用显式事务  
  
```  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>B. 回滚事务  
 下面的示例演示了回滚事务的效果。  在此示例中，在 ROLLBACK 语句将回滚 INSERT 语句，但仍存在创建的表。  
  
```  
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>C. 设置自动提交  
 下面的示例将自动提交设置设为`ON`。  
  
```  
SET AUTOCOMMIT ON;  
```  
  
 下面的示例将自动提交设置设为`OFF`。  
  
```  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>D. 使用隐式多语句事务  
  
```  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id int);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>另请参阅  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [将事务隔离级别设置 &#40;Transact SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT (Transact-SQL)](../../t-sql/functions/trancount-transact-sql.md)  
  
  
