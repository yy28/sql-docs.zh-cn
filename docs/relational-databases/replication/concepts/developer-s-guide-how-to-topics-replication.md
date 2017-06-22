---
title: "开发人员指南：操作指南主题（复制）| Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c6c15ae6-da52-4638-93d3-61c7242e8a0b
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 288ed137e701d6cfb416d12b6ff2176c59ec0278
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="developer39s-guide-how-to-topics-replication"></a>开发人员指南：操作指南主题（复制）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本主题提供了一些链接，这些链接包含有关如何以编程方式执行与复制相关的任务的信息。  
  
## <a name="securing-a-replication-topology"></a>保护复制拓扑  
  
-   [查看和修改复制安全设置](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
-   [管理发布访问列表中的登录名](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="configuring-modifying-and-disabling-publishing-and-distribution-replication"></a>配置、修改和禁用发布和分发（复制）  
  
-   [配置发布和分发](../../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
-   [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [禁用发布和分发](../../../relational-databases/replication/disable-publishing-and-distribution.md)  
  
## <a name="creating-modifying-and-deleting-publications-and-articles"></a>创建、修改及删除发布和项目  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [定义项目](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [查看和修改项目属性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [删除发布](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [删除项目](../../../relational-databases/replication/publish/delete-an-article.md)  
  
-   [从 Oracle 数据库创建发布](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)  
  
-   [设置订阅的过期期限](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)  
  
-   [指定架构选项](../../../relational-databases/replication/publish/specify-schema-options.md)  
  
-   [复制架构更改](../../../relational-databases/replication/publish/replicate-schema-changes.md)  
  
-   [管理标识列](../../../relational-databases/replication/publish/manage-identity-columns.md)  
  
-   [设置合并发布的兼容级别](../../../relational-databases/replication/publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>快照选项  
  
-   [配置快照属性（复制 Transact-SQL 编程）](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [通过 FTP 传递快照](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)  
  
### <a name="filtering-data"></a>筛选数据  
  
-   [定义和修改列筛选器](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)  
  
-   [定义和修改静态行筛选器](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)  
  
-   [定义和修改合并项目的参数化行筛选器](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [优化参数化行筛选器](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)  
  
-   [定义和修改合并项目间的联接筛选器](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>事务复制选项  
  
-   [为事务项目的数据更改设置传播方法](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [对事务发布启用更新订阅](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>合并复制选项  
  
-   [定义合并表项目间的逻辑记录关系](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [指定合并表项目的处理顺序（复制 Transact-SQL 编程）](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [指定合并表项目仅用于下载](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [为合并项目指定不应跟踪删除（复制 Transact-SQL 编程）](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [指定合并项目的冲突跟踪和解决方法级别](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [指定合并项目冲突解决程序](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
-   [指定合并项目的交互式冲突解决](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="creating-modifying-and-deleting-subscriptions"></a>创建、修改和删除订阅  
  
-   [创建请求订阅](../../../relational-databases/replication/create-a-pull-subscription.md)  
  
-   [查看和修改请求订阅属性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
  
-   [删除请求订阅](../../../relational-databases/replication/delete-a-pull-subscription.md)  
  
-   [创建推送订阅](../../../relational-databases/replication/create-a-push-subscription.md)  
  
-   [查看和修改推送订阅属性](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)  
  
-   [删除推送订阅](../../../relational-databases/replication/delete-a-push-subscription.md)  
  
-   [指定同步计划](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
-   [创建事务发布的可更新订阅](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md)
  
-   [为非 SQL Server 订阅服务器创建订阅](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronizing-subscriptions"></a>同步订阅  
  
-   [创建并应用初始快照](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [为包含参数化筛选器的合并发布创建快照](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [从备份初始化事务订阅（复制 Transact-SQL 编程）](../../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md)  
  
-   [手动初始化订阅](../../../relational-databases/replication/initialize-a-subscription-manually.md)  
  
-   [同步请求订阅](../../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [同步推送订阅](../../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
-   [重新初始化订阅](../../../relational-databases/replication/reinitialize-a-subscription.md)  
  
-   [在同步期间执行脚本（复制 Transact-SQL 编程）](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)  
  
-   [为合并项目实现业务逻辑处理程序](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
-   [调试业务逻辑处理程序（复制编程）](../../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)  
  
-   [控制同步期间触发器和约束的行为（复制 Transact-SQL 编程）](../../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)  
  
-   [为合并项目实现自定义冲突解决程序](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administering-a-replication-topology"></a>管理复制拓扑  
  
-   [处理复制代理配置文件](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [在订阅服务器上验证数据](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
-   [通过参数化筛选器为合并发布管理分区](../../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)  
  
-   [将数据批量加载到合并发布中的表（复制 Transact-SQL 编程）](../../../relational-databases/replication/bulk-load-data-into-tables-in-a-merge-publication.md)  
  
-   [清除合并元数据（复制 Transact-SQL 编程）](../../../relational-databases/replication/administration/clean-up-merge-metadata-replication-transact-sql-programming.md)  
  
-   [执行合并项目的虚更新（复制 Transact-SQL 编程）](../../../relational-databases/replication/administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)  
  
-   [查看分发数据库中复制的命令和其他信息（复制 Transact-SQL 编程）](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [为事务复制启用协调备份（复制 Transact-SQL 编程）](../../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)  
  
-   [管理对等拓扑（复制 Transact-SQL 编程）](../../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)  
  
-   [停止复制拓扑（复制 Transact-SQL 编程）](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)  
  
-   [为 Oracle 发布服务器配置事务集作业（复制 Transact-SQL 编程）](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)  
  
-   [升级复制脚本（复制 Transact-SQL 编程）](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitoring-a-replication-topology"></a>监视复制拓扑  
  
-   [允许非管理员使用复制监视器](../../../relational-databases/replication/monitor/allow-non-administrators-to-use-replication-monitor.md)  
  
-   [以编程方式监视复制](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
-   [查看分发数据库中复制的命令和其他信息（复制 Transact-SQL 编程）](../../../relational-databases/replication/monitor/view-replicated-commands-and-information-in-distribution-database.md)  
  
-   [查看合并发布的冲突信息（复制 Transact-SQL 编程）](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
-   [为事务复制测量滞后时间和验证连接](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
