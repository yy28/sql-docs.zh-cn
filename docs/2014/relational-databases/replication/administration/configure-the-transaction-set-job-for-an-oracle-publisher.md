---
title: 为 Oracle 发布服务器配置事务集作业（复制 Transact-sql 编程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_publisherproperty
- Oracle publishing [SQL Server replication], configuring
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48282f08df588f54b6f03a0b99c58a2f0cf039ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67793527"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>为 Oracle 发布服务器配置事务集作业（复制 Transact-SQL 编程）
  **Xactset** 作业是在发布服务器上运行的复制创建的 Oracle 数据库作业，用于在日志读取器代理未与发布服务器连接时创建事务集。 您可以使用复制存储过程以编程方式从分发服务器启用和配置此作业。 有关详细信息，请参阅 [Performance Tuning for Oracle Publishers](../non-sql/performance-tuning-for-oracle-publishers.md)（Oracle 发布服务器的性能优化）。  
  
### <a name="to-enable-the-transaction-set-job"></a>启用事务集作业  
  
1.  在 Oracle 分发服务器上，将 **job_queue_processes** 初始化参数设置为一个足够大的值以允许 Xactset 作业运行。 有关此参数的详细信息，请参阅 Oracle 发布服务器的数据库文档。  
  
2.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 为** \@发布服务器**指定 Oracle 发布服务器的名称，将的值`xactsetbatching`指定为** \@propertyname**，并将值`enabled`指定** \@为。**  
  
3.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 ** \@为 "** ** \@发布服务器**" 指定 Oracle 发布服务器的名称，将`xactsetjobinterval` "值" 指定为** \@propertyname**，并为 "值" 指定值 "时间间隔"。  
  
4.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 为** \@发布服务器**指定 Oracle 发布服务器的名称，将的值`xactsetjob`指定为** \@propertyname**，并将值`enabled`指定** \@为。**  
  
### <a name="to-configure-the-transaction-set-job"></a>配置事务集作业  
  
1.  （可选）在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 为 **publisher 指定 Oracle 发布服务器的名称\@** 。 这将返回发布服务器上的 **Xactset** 作业的属性。  
  
2.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 为 **publisher 指定 Oracle 发布服务器的名称，为 \@propertyname 指定要设置的 Xactset 作业属性的名称，并为** propertyvalue 指定新设置 **\@** **\@** 。  
  
3.  （可选）对于每个要设置的 Xactset 作业属性重复步骤 2。 更改`xactsetjobinterval`属性时，必须在 Oracle 发布服务器上重新启动作业，以使新的时间间隔生效。  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>查看事务集作业的属性  
  
1.  在分发服务器上，执行 [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql)。 为 **publisher 指定 Oracle 发布服务器的名称\@** 。  
  
### <a name="to-disable-the-transaction-set-job"></a>禁用事务集作业  
  
1.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 为** \@发布服务器**指定 Oracle 发布服务器的名称，将的值`xactsetjob`指定为** \@propertyname**，并将值`disabled`指定** \@为。**  
  
## <a name="example"></a>示例  
 以下示例将启用 `Xactset` 作业并将运行间隔设置为三分钟。  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>另请参阅  
 [Oracle 发布服务器的性能优化](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
