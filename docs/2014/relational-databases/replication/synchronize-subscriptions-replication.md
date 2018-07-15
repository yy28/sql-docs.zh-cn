---
title: 同步订阅（复制）| Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], subscriptions
- subscriptions [SQL Server replication], synchronizing
- replication [SQL Server], synchronization
ms.assetid: cbe13120-8dd9-4309-88dd-07a801c68f5f
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1c24eee2e720e9a2a7098875f6255e08817cdabc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319877"
---
# <a name="synchronize-subscriptions-replication"></a>同步订阅（复制）
  订阅是由复制代理进行同步的。 分发代理同步针对的是事务发布和快照发布的订阅，而合并代理同步针对的是合并发布的订阅。 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、复制存储过程和复制管理对象 (RMO) 来同步订阅，并控制同步行为。 下面的主题介绍如何同步订阅并指定同步选项。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [创建并应用初始快照](create-and-apply-the-initial-snapshot.md)  
  
-   [为包含参数化筛选器的合并发布创建快照](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [使用备份来初始化事务发布 &#40;SQL Server Management Studio&#41;](enable-initialization-with-backup-for-transactional-publications.md)  
  
-   [从备份初始化事务订阅（复制 Transact-SQL 编程）](initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [手动初始化订阅](initialize-a-subscription-manually.md)  
  
-   [同步请求订阅](synchronize-a-pull-subscription.md)  
  
-   [同步推送订阅](synchronize-a-push-subscription.md)  
  
-   [重新初始化订阅](reinitialize-a-subscription.md)  
  
-   [在应用快照之前和之后执行脚本 &#40;SQL Server Management Studio&#41;](execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [在同步期间执行脚本（复制 Transact-SQL 编程）](execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [查看和解决合并发布的数据冲突 &#40;SQL Server Management Studio&#41;](view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   [查看事务发布的数据冲突 &#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
-   [使用 Windows 同步管理器同步订阅（Windows 同步管理器）](synchronize-a-subscription-using-windows-synchronization-manager.md)  
  
-   [为合并项目实现业务逻辑处理程序](implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [调试业务逻辑处理程序（复制编程）](debug-a-business-logic-handler-replication-programming.md)  
  
-   [控制同步期间触发器和约束的行为（复制 Transact-SQL 编程）](control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [为合并项目实现自定义冲突解决程序](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="see-also"></a>请参阅  
 [同步数据](synchronize-data.md)  
  
  
