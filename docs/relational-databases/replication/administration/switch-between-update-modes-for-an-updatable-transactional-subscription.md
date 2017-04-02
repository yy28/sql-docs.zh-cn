---
title: "切换可更新事务性订阅的更新模式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "事务复制, 可更新订阅"
  - "可更新订阅, 更新模式"
  - "订阅 [SQL Server 复制], 可更新"
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 切换可更新事务性订阅的更新模式
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中切换可更新事务订阅的更新模式。 可以使用新建订阅向导，为可更新的订阅指定模式。 有关使用此向导设置模式的信息，请参阅 [查看和修改请求订阅属性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
-   **切换可更新事务订阅的更新模式，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   可以随时从立即更新向排队更新进行故障转移。 但执行该操作后，只有在已连接订阅服务器和发布服务器且队列读取器代理已将队列中的所有挂起消息应用到发布服务器后，才能恢复立即更新。  
  
###  <a name="Recommendations"></a> 建议  
  
-   当对事务发布的更新订阅支持从一种更新模式故障转移到另一种更新模式时，可通过编程方式切换更新模式以应对连接发生短暂变化的情况。 可以使用复制存储过程，以编程方式并根据需要设置更新模式。 有关详细信息，请参阅 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
> [!NOTE]  
>  若要更改的更新模式，在创建订阅后 **update_mode** 属性必须设置为 **故障转移** （它允许从立即更新到的交换机排队更新） 或 **排队故障转移** （允许从排队更新到立即更新切换） 时创建订阅。 在新建订阅向导中，这些属性是自动设置的。  
  
#### 设置推送订阅的更新模式  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地订阅”** 文件夹。  
  
3.  右键单击您要为其设置更新模式，然后单击的订阅 **设置更新方法**。  
  
4.  在 **设置更新方法-\< 订阅服务器上>: \< 订阅数据库>** 对话框中，选择 **即时更新** 或 **排队更新**。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 设置请求订阅的更新模式  
  
1.  在 **订阅属性-\< 发布服务器>: \< 发布数据库>** 对话框中，选择一个值的 **立即复制更改** 或 **对更改进行排队** 为 **订阅服务器更新方法** 选项。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 有关访问 **订阅属性-\< 发布服务器>: \< 发布数据库>** 对话框中，请参阅 [查看和修改请求订阅属性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 切换更新模式  
  
1.  验证订阅支持故障转移，通过执行 [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) 对于请求订阅或 [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) 对于推送订阅。 如果结果集中 **update mode** 的值为 **3** 或 **4**，则支持故障转移。  
  
2.  在订阅服务器上的订阅数据库上，执行 [sp_setreplfailovermode](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，以及下列其中一项值为 **@failover_mode**:  
  
    -   **排入队列** -故障转移到排队更新时已暂时失去连接。  
  
    -   **立即** -故障转移到立即更新，当恢复连接。  
  
## 另请参阅  
 [事务复制的可更新订阅](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  