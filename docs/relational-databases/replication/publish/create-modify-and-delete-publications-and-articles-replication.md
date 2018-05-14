---
title: 创建、修改和删除发布和项目（复制）| Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], creating
- articles [SQL Server replication], defining
ms.assetid: e66d06ec-a12b-444d-875b-77f958af2f21
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2f5d375a46a4e158311e5005dc8bf7c3b2627bc1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="create-modify-and-delete-publications-and-articles-replication"></a>创建、修改和删除发布和项目（复制）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本节包含有关与创建发布和定义项目相关的任务的过程信息。  
  
## <a name="in-this-section"></a>本节内容  
  
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
  
## <a name="snapshot-options"></a>快照选项  
  
-   [指定快照格式 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/specify-snapshot-format-sql-server-management-studio.md)  
  
-   [指定备用快照文件夹位置 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   [压缩快照文件 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/compress-snapshot-files-sql-server-management-studio.md)  
  
-   [配置快照属性（复制 Transact-SQL 编程）](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [在应用快照之前和之后执行脚本 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [通过 FTP 传递快照](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)  
  
## <a name="filtering-data"></a>筛选数据  
  
-   [定义和修改列筛选器](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)  
  
-   [定义和修改静态行筛选器](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)  
  
-   [定义和修改合并项目的参数化行筛选器](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [优化参数化行筛选器](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)  
  
-   [定义和修改合并项目间的联接筛选器](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
-   [在合并项目之间自动生成一组联接筛选器 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/automatically-generate-join-filters-between-merge-articles.md)  
  
## <a name="transactional-replication-options"></a>事务复制选项  
  
-   [为事务项目的数据更改设置传播方法](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [允许更新事务发布的订阅](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
-   [设置排队更新冲突解决选项 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)  
  
-   [在事务发布中发布存储过程的执行 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
## <a name="merge-replication-options"></a>合并复制选项  
  
-   [定义合并表项目间的逻辑记录关系](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [指定合并表项目的处理顺序（复制 Transact-SQL 编程）](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [指定合并表项目仅用于下载](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [为合并项目指定不应跟踪删除（复制 Transact-SQL 编程）](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [指定合并项目的冲突跟踪和解决方法级别](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [指定合并项目冲突解决程序](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
-   [指定合并项目的交互式冲突解决](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="see-also"></a>另请参阅  
 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
