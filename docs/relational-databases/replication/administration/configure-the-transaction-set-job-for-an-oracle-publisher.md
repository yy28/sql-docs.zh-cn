---
title: 配置事务集作业（Oracle 发布服务器）
description: 了解如何为发布到 SQL Server 订阅服务器的 Oracle 发布服务器配置事务集作业。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 8f25f3d9c9a69d3a8f87e8a4eb1886f31092940f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "75322046"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher"></a>为 Oracle 发布服务器配置事务集作业
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Xactset** 作业是在发布服务器上运行的复制创建的 Oracle 数据库作业，用于在日志读取器代理未与发布服务器连接时创建事务集。 您可以使用复制存储过程以编程方式从分发服务器启用和配置此作业。 有关详细信息，请参阅 [Performance Tuning for Oracle Publishers](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)（Oracle 发布服务器的性能优化）。  
  
### <a name="to-enable-the-transaction-set-job"></a>启用事务集作业  
  
1.  在 Oracle 分发服务器上，将 **job_queue_processes** 初始化参数设置为一个足够大的值以允许 Xactset 作业运行。 有关此参数的详细信息，请参阅 Oracle 发布服务器的数据库文档。  
  
2.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 为 **publisher 指定 Oracle 发布服务器的名称，将 \@propertyname 的值指定为 xactsetbatching，并将** propertyvalue 的值指定为“enabled”  **\@**  **\@** 。  
  
3.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 为 **publisher 指定 Oracle 发布服务器的名称，将 \@propertyname 的值指定为 xactsetjobinterval，并为** propertyvalue 指定作业时间间隔（分钟）  **\@** **\@** 。  
  
4.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 为 **publisher 指定 Oracle 发布服务器的名称，将 \@propertyname 的值指定为 xactsetjob，并将** propertyvalue 的值指定为 enabled  **\@**  **\@** 。  
  
### <a name="to-configure-the-transaction-set-job"></a>配置事务集作业  
  
1.  （可选）在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 为 **publisher 指定 Oracle 发布服务器的名称\@** 。 这将返回发布服务器上的 **Xactset** 作业的属性。  
  
2.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 为 **publisher 指定 Oracle 发布服务器的名称，为 \@propertyname 指定要设置的 Xactset 作业属性的名称，并为** propertyvalue 指定新设置 **\@** **\@** 。  
  
3.  （可选）对于每个要设置的 Xactset 作业属性重复步骤 2。 更改 **xactsetjobinterval** 属性后，必须重新启动 Oracle 发布服务器上的作业以使得新间隔生效。  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>查看事务集作业的属性  
  
1.  在分发服务器上，执行 [sp_helpxactsetjob](../../../relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql.md)。 为 **publisher 指定 Oracle 发布服务器的名称\@** 。  
  
### <a name="to-disable-the-transaction-set-job"></a>禁用事务集作业  
  
1.  在分发服务器上，执行 [sp_publisherproperty (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 为 **publisher 指定 Oracle 发布服务器的名称，将 \@propertyname 的值指定为 xactsetjob，并将** propertyvalue 的值指定为 disabled  **\@**  **\@** 。  
  
## <a name="example"></a>示例  
 以下示例将启用 `Xactset` 作业并将运行间隔设置为三分钟。  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../relational-databases/replication/codesnippet/tsql/configure-the-transactio_1.sql)]  
  
## <a name="see-also"></a>另请参阅  
 [Oracle 发布服务器的性能优化](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
