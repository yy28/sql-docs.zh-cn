---
title: 配置事务集作业为 Oracle 发布服务器 （复制 TRANSACT-SQL 编程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_publisherproperty
- Oracle publishing [SQL Server replication], configuring
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8da949228afdfa4b0e6407205f1a995ee80fb343
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248377"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>为 Oracle 发布服务器配置事务集作业（复制 Transact-SQL 编程）
  **Xactset** 作业是在发布服务器上运行的复制创建的 Oracle 数据库作业，用于在日志读取器代理未与发布服务器连接时创建事务集。 您可以使用复制存储过程以编程方式从分发服务器启用和配置此作业。 有关详细信息，请参阅 [Performance Tuning for Oracle Publishers](../non-sql/performance-tuning-for-oracle-publishers.md)（Oracle 发布服务器的性能优化）。  
  
### <a name="to-enable-the-transaction-set-job"></a>启用事务集作业  
  
1.  在 Oracle 分发服务器上，将 **job_queue_processes** 初始化参数设置为一个足够大的值以允许 Xactset 作业运行。 有关此参数的详细信息，请参阅 Oracle 发布服务器的数据库文档。  
  
2.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 指定 Oracle 发布服务器的名称**@publisher**，值为`xactsetbatching`有关**@propertyname**，并将值`enabled`为**@propertyvalue**.  
  
3.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 指定 Oracle 发布服务器的名称**@publisher**，值为`xactsetjobinterval`有关**@propertyname**，和作业时间间隔，以分钟为单位的**@propertyvalue**.  
  
4.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 指定 Oracle 发布服务器的名称**@publisher**，值为`xactsetjob`有关**@propertyname**，并将值`enabled`为**@propertyvalue**.  
  
### <a name="to-configure-the-transaction-set-job"></a>配置事务集作业  
  
1.  （可选）在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 为 **@publisher**。 这将返回发布服务器上的 **Xactset** 作业的属性。  
  
2.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 为 **@publisher**指定 Oracle 发布服务器的名称，为 **@propertyname**指定要设置的 Xactset 作业属性的名称，并为 **@propertyvalue**。  
  
3.  （可选）对于每个要设置的 Xactset 作业属性重复步骤 2。 更改时`xactsetjobinterval`属性，您必须重启该作业在 Oracle 发布服务器上新间隔生效。  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>查看事务集作业的属性  
  
1.  在分发服务器上，执行 [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql)。 为 **@publisher**。  
  
### <a name="to-disable-the-transaction-set-job"></a>禁用事务集作业  
  
1.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 指定 Oracle 发布服务器的名称**@publisher**，值为`xactsetjob`有关**@propertyname**，并将值`disabled`为**@propertyvalue**.  
  
## <a name="example"></a>示例  
 以下示例将启用 `Xactset` 作业并将运行间隔设置为三分钟。  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>请参阅  
 [Oracle 发布服务器的性能优化](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
