---
title: "订阅过期和停用 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "分发服务器 [SQL Server 复制], 分发保持期"
  - "订阅 [SQL Server 复制], 过期"
  - "发布 [SQL Server 复制], 发布保持期"
  - "过期 [SQL Server 复制]"
  - "保持期 [SQL Server 复制]"
  - "发布保持期"
  - "分发保持期"
  - "订阅 [SQL Server 复制], 停用"
  - "停用订阅"
ms.assetid: 4d03f5ab-e721-4f56-aebc-60f6a56c1e07
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# 订阅过期和停用
  如果在指定的“保持期” 内未同步订阅，订阅可能会停用或过期。 发生什么操作取决于复制的类型和所超过的保持期。  
  
 若要设置保持期，请参阅 [设置订阅的过期期限](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md), ，[分发保持期设置为事务发布和 #40;SQL Server Management Studio & #41;](../../relational-databases/replication/set distribution retention period for transactional publications.md), ，和 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)。  
  
## 事务复制  
 事务复制使用的最大分发保持期 ( **@max_distretention** 参数 [sp_adddistributiondb & #40;Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md))和发布保持期 ( **@retention** 参数 [sp_addpublication & #40;Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)):  
  
-   如果在最大分发保持期 （默认值为 72 小时） 内未同步订阅，并且有尚未传递到订阅服务器上分发数据库中的更改，会将订阅标记的已停用 **分发清除** 在分发服务器运行的作业。 必须重新初始化订阅。  
  
-   如果在发布保持期 （默认值为 336 小时） 内未同步订阅，订阅将过期并被丢弃 **已过期的订阅清除** 在发布服务器运行的作业。 必须重新创建和同步订阅。  
  
     如果推送订阅过期，则会彻底删除该订阅，但是请求订阅则不同。 您必须清除订阅服务器上的请求订阅。 有关详细信息，请参阅 [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)。  
  
## 合并复制  
 合并复制使用发布保持期 ( **@retention** 和 **@retention_period_unit** 参数 [sp_addmergepublication & #40;Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md))。 订阅过期后必须将其重新初始化，因为订阅的元数据已被删除。 未重新初始化的订阅将由运行在发布服务器上的 **“过期的订阅清除”** 作业删除。 默认情况下，此作业每天运行；它删除在两倍的发布保持期内尚未同步的所有推送订阅。 例如：  
  
-   如果某发布的保持期为 14 天，则订阅如果在 14 天内尚未同步就会过期。  
  
     如果发布服务器运行的是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本，并且订阅的代理来自 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本，则仅当对该订阅分区中的数据进行更改时，该订阅才会过期。 例如，假定订阅服务器仅接收德国客户的客户数据。 如果将保持期设置为 14 天，则只有在最近 14 天内更改了德国客户的数据时，该订阅才会在第 14 天过期。  
  
-   在上次同步后的第 14 天到第 27 天，可以重新初始化该订阅。  
  
-   在上次同步后的第 28 天，该订阅由 **“过期的订阅清除”** 作业删除。 如果推送订阅过期，则会彻底删除该订阅，但是请求订阅则不同。 您必须清除订阅服务器上的请求订阅。 有关详细信息，请参阅 [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md)。  
  
### 设置合并发布的发布保持期时的注意事项  
 在设置合并发布的保持期时，请谨记下列注意事项：  
  
-   合并发布的保持期具有 24 小时的宽限期，以适应处于不同时区中的订阅服务器。 例如，如果将保持期设置为 1 天，则实际的保持期为 48 小时。  
  
-   合并复制元数据的清除取决于发布保持期：  
  
    -   在到达保持期之前，复制无法清除发布数据库和订阅数据库中的元数据。 在为保持期指定较大值时务必谨慎，因为这可能对复制性能产生负面影响。 如果能很有把握地预测出所有订阅服务器都将在该时间段内定期同步，则建议使用较低的设置。  
  
    -   可以指定订阅永不过期 (值为 0， **@retention**)，但强烈建议您不要使用此值，因为不能清除元数据。  
  
-   任何重新发布服务器的保持期都必须设置为等于或小于在原始发布服务器上设置的保持期。 对于所有发布服务器和它们的备用同步伙伴，应该使用相同的发布保持期。 使用不同的值可能会导致无法收敛。 如果需要更改发布保持期的值，请重新初始化订阅服务器，以免数据无法收敛。  
  
-   如果在清除之后增大发布保持期，而且订阅尝试与发布服务器（已删除元数据）合并，则订阅将由于增大了保持期值而不会过期。 但是，发布服务器没有足够的元数据来下载对订阅服务器所做的更改，这会导致无法收敛。  
  
## 另请参阅  
 [重新初始化订阅](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [复制代理管理](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  