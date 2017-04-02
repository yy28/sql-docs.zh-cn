---
title: "同步订阅（复制） | Microsoft Docs"
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
  - "同步 [SQL Server 复制], 订阅"
  - "订阅 [SQL Server 复制], 同步"
  - "复制 [SQL Server 复制], 同步"
ms.assetid: cbe13120-8dd9-4309-88dd-07a801c68f5f
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 同步订阅（复制）
  订阅是由复制代理进行同步的。 分发代理同步针对的是事务发布和快照发布的订阅，而合并代理同步针对的是合并发布的订阅。 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、复制存储过程和复制管理对象 (RMO) 来同步订阅，并控制同步行为。 下面的主题介绍如何同步订阅并指定同步选项。  
  
## 本节内容  
  
-   [创建并应用初始快照](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [为包含参数化筛选器的合并发布创建快照](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [启用使用备份初始化事务发布和 #40;SQL Server Management Studio & #41;](../../relational-databases/replication/enable initialization with backup for transactional publications.md)  
  
-   [初始化事务订阅从备份和 #40;复制 TRANSACT-SQL 编程 & #41;](../../relational-databases/replication/initialize a transactional subscription from a backup.md)  
  
-   [手动初始化订阅](../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [同步请求订阅](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [同步推送订阅](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [重新初始化订阅](../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [应用快照之前和之后执行脚本 （& a) #40;SQL Server Management Studio & #41;](../../relational-databases/replication/execute scripts before and after a snapshot is applied.md)  
  
-   [在同步 & #40; 期间执行脚本复制 TRANSACT-SQL 编程 & #41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [查看和解决数据冲突的合并发布 & #40;SQL Server Management Studio & #41;](../../relational-databases/replication/view and resolve data conflicts for merge publications.md)  
  
-   [对于事务发布和 #40; 查看数据冲突SQL Server Management Studio & #41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
-   [使用 Windows 同步管理器和 #40; 同步订阅Windows 同步管理器和 #41;](../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md)  
  
-   [实现合并项目的业务逻辑处理程序](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [调试业务逻辑处理程序 & #40;复制编程 & #41;](../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [在同步 & #40; 控制行为的触发器和约束复制 TRANSACT-SQL 编程 & #41;](../../relational-databases/replication/control behavior of triggers and constraints in synchronization.md)  
  
-   [为合并项目实现自定义冲突解决程序](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## 另请参阅  
 [同步数据](../../relational-databases/replication/synchronize-data.md)  
  
  