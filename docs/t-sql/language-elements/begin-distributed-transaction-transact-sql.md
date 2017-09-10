---
title: "开始分布式事务 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/29/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DISTRIBUTED
- BEGIN_DISTRIBUTED_TRANSACTION_TSQL
- DISTRIBUTED_TSQL
- BEGIN DISTRIBUTED TRANSACTION
dev_langs:
- TSQL
helpviewer_keywords:
- BEGIN DISTRIBUTED TRANSACTION statement
- distributed transactions [SQL Server], starting
- MS DTC, transaction management
- distributed transactions [SQL Server], BEGIN DISTRIBUTED TRANSACTION statement
- servers [SQL Server], distributed transactions
- starting distributed transactions
- remote servers [SQL Server], distributed transactions
- starting transactions
ms.assetid: c3bc2716-39d3-4061-8c6a-8734899231ac
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 93287230933c8ad33bc72185b2b26402ef8048fa
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="begin-distributed-transaction-transact-sql"></a>BEGIN DISTRIBUTED TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定一个由 [!INCLUDE[tsql](../../includes/tsql-md.md)] 分布式事务处理协调器 (MS DTC) 管理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务的起点。  
    
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
BEGIN DISTRIBUTED { TRAN | TRANSACTION }   
     [ transaction_name | @tran_name_variable ]   
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *transaction_name*  
 用户定义的事务名，用于跟踪 MS DTC 实用工具中的分布式事务。 *transaction_name*必须符合标识符的规则，并且必须是\<= 32 个字符。  
  
 @*tran_name_variable*  
 用户定义的一个变量名，它含有一个事务名，该事务名用于跟踪 MS DTC 实用工具中的分布式事务。 必须使用声明变量**char**， **varchar**， **nchar**，或**nvarchar**数据类型。  
  
## <a name="remarks"></a>注释  
 执行 BEGIN DISTRIBUTED TRANSACTION 语句的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例是事务创建者，并控制事务的完成。 当为会话发出后续 COMMIT TRANSACTION 或 ROLLBACK TRANSACTION 语句时，控制实例请求 MS DTC 在所涉及的所有实例间管理分布式事务的完成。  
  
 事务级别的快照隔离不支持分布式事务。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的远程实例登记到分布式事务中的主要方法是当已在分布式事务中登记的会话执行引用链接服务器的分布式查询时。  
  
 例如，如果在服务器 A 上发出 BEGIN DISTRIBUTED TRANSACTION，则该会话将调用服务器 B 上的一个存储过程和服务器 C 上的另一个存储过程。 服务器 C 上的存储过程执行针对服务器 D 的分布式查询，这样该分布式事务将涉及所有四台计算机。 服务器 A 上的[!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例是该事务的初始控制实例。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 分布式事务涉及的会话并不获取可以传递给另一个会话的事务对象，从而也不能将其显式登记在分布式事务中。 远程服务器登记到事务中的唯一方法是成为分布式查询或远程存储过程调用的目标。  
  
 当在本地事务中执行分布式的查询时，事务如果目标 OLE DB 数据源支持 ITransactionLocal 自动提升为分布式事务。 如果目标 OLE DB 数据源不支持 ITransactionLocal，仅只读操作允许分布式查询中。  
  
 已在分布式事务中登记的会话执行一个引用远程服务器的远程存储过程调用。  
  
 **Sp_configure 远程 proc trans**选项控制是否对在本地事务中的远程存储过程的调用会自动导致本地事务提升为分布式事务由 MS DTC 管理。 连接级 SET 选项 REMOTE_PROC_TRANSACTIONS 可以用于覆盖由建立实例默认**sp_configure 远程 proc trans**。启用本选项后，远程存储过程调用会使一个本地事务被提升为分布式事务。 创建 MS DTC 事务的连接成为该事务的创建者。 COMMIT TRANSACTION 初始化一个 MS DTC 协调的提交。 如果**sp_configure 远程 proc trans**选项为 ON，在本地事务中的远程存储的过程调用已自动受到保护作为分布式事务的一部分而无需重写到专门问题的应用程序开始分布式事务而不是 BEGIN TRANSACTION。  
  
 有关分布式事务环境和处理的详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器文档。  
  
## <a name="permissions"></a>Permissions  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
 该示例从[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]的本地实例和远程服务器的实例上的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 数据库中同时删除候选项。 本地和远程数据库都将提交或回滚本事务。  
  
> [!NOTE]  
>  除非正在运行[!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例的计算机中当前安装了 MS DTC，否则本示例会产生错误消息。 有关安装 MS DTC 的详细信息，请参见 Microsoft 分布式事务处理协调器文档。  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN DISTRIBUTED TRANSACTION;  
-- Delete candidate from local instance.  
DELETE AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
-- Delete candidate from remote instance.  
DELETE RemoteServer.AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [BEGIN TRANSACTION (Transact-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION (Transact-SQL)](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [提交工作 &#40;Transact SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION (Transact-SQL)](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [回滚工作 &#40;Transact SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION (Transact-SQL)](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  

