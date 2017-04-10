---
title: "定义和修改列筛选器 | Microsoft Docs"
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
  - "筛选器 [SQL Server 复制], 列"
  - "修改筛选器, 列"
  - "修改筛选器"
  - "列筛选器 [SQL Server 复制]"
ms.assetid: d7c3186a-9a8c-45d8-ab34-05beec4c26dd
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# 定义和修改列筛选器
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定义和修改列筛选器。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
-   **定义和修改列筛选器，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   某些列不能进行筛选;有关详细信息，请参阅 [筛选已发布数据](../../../relational-databases/replication/publish/filter-published-data.md)。 如果在初始化订阅之后修改了列筛选器，则必须在更改后生成新的快照并重新初始化所有订阅。 有关属性更改要求的详细信息，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 可以在新建发布向导的 **“项目”** 页上定义列筛选器。 有关使用新建发布向导的详细信息，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
 定义和修改列筛选器在 **文章** 页 **发布属性-\< 发布>** 对话框。 有关发布和项目属性的详细信息，请参阅 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 定义列筛选器  
  
1.  在新建发布向导的 **“项目”** 页上，在 **“要发布的对象”** 窗格中展开要筛选的表。  
  
2.  清除要筛选的每个列旁边的复选框。  
  
#### 修改列筛选  
  
1.  在 **文章** 页 **发布属性-\< 发布>** 对话框框中，展开要在筛选的表 **要发布的对象** 窗格。  
  
2.  清除要筛选的每个列旁边的复选框，并确保选中每个应包含在项目中的列的复选框。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 在创建表项目时，您可以定义要在项目中包含的列以及在定义项目后更改列。 您可以使用复制存储过程以编程的方式创建和修改已筛选的列。  
  
> [!NOTE]  
>  下列过程假定基础表未发生更改。 将数据定义语言 (DDL) 更改复制到已发布表的信息，请参阅 [发布数据库上进行架构更改](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
#### 为快照发布或事务发布中发布的项目定义列筛选器  
  
1.  定义要筛选的项目。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)。 这将定义要包括在项目中或要从项目中删除的列。  
  
    -   如果发布只有少数的列从表拥有许多列，请执行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 正在添加的每个列的一次。 为 **@column** 指定列名称并将 **@operation** 的值指定为 **add**。  
  
    -   如果发布拥有许多列的表中的大部分列，则执行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), ，将值指定为 **null** 为 **@column** ，值为 **添加** 为 **@operation** 添加所有列。 然后执行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), ，一旦为每个要排除的列，将值指定为 **删除** 为 **@operation** 和排除的列名称 **@column**。  
  
3.  在发布服务器上对发布数据库中，执行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 为 **@publication** 指定发布名称并为 **@article**指定已筛选项目的名称。 这将为筛选的项目创建同步对象。  
  
#### 为快照发布或事务发布中发布的项目更改列筛选器以包括其他列  
  
1.  在发布服务器上对发布数据库中，执行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 正在添加的每个列的一次。 为 **@column** 指定列名称并将 **@operation** 的值指定为 **add**。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 为 **@publication** 指定发布名称并为 **@article**指定已筛选项目的名称。 如果发布拥有现有订阅，将值指定为 **1** 为 **@change_active**。 这将为已筛选的项目重新创建同步对象。  
  
3.  对发布重新运行快照代理作业以生成更新的快照。  
  
4.  重新初始化订阅。 有关详细信息，请参阅 [重新初始化订阅](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### 为快照发布或事务发布中发布的项目更改列筛选器以删除列  
  
1.  在发布服务器上对发布数据库中，执行 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) 一次每个列被删除。 为 **@column** 指定列名称并将 **@operation** 的值指定为 **drop**。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 为 **@publication** 指定发布名称并为 **@article**指定已筛选项目的名称。 如果发布拥有现有订阅，将值指定为 **1** 为 **@change_active**。 这将为已筛选的项目重新创建同步对象。  
  
3.  对发布重新运行快照代理作业以生成更新的快照。  
  
4.  重新初始化订阅。 有关详细信息，请参阅 [重新初始化订阅](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### 为合并复制中发布的项目定义列筛选器  
  
1.  定义要筛选的项目。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md)。 这将定义要包括在项目中或要从项目中删除的列。  
  
    -   如果发布只有少数的列从表拥有许多列，请执行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 正在添加的每个列的一次。 为 **@column** 指定列名称并将 **@operation** 的值指定为 **add**。  
  
    -   如果发布拥有许多列的表中的大部分列，则执行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), ，将值指定为 **null** 为 **@column** ，值为 **添加** 为 **@operation** 添加所有列。 然后执行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md), ，一旦为每个要排除的列，将值指定为 **删除** 为 **@operation** 和排除的列名称 **@column**。  
  
#### 为合并发布中发布的项目更改列筛选器以包括其他列  
  
1.  在发布服务器上对发布数据库中，执行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 正在添加的每个列的一次。 指定的列名称 **@column**, ，值为 **添加** 为 **@operation** ，值为 **1** 两个 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**。  
  
2.  对发布重新运行快照代理作业以生成更新的快照。  
  
3.  重新初始化订阅。 有关详细信息，请参阅 [重新初始化订阅](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### 为合并发布中发布的项目更改列筛选器以删除列  
  
1.  在发布服务器上对发布数据库中，执行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 一次每个列被删除。 指定的列名称 **@column**, ，值为 **删除** 为 **@operation** ，值为 **1** 两个 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**。  
  
2.  对发布重新运行快照代理作业以生成更新的快照。  
  
3.  重新初始化订阅。 有关详细信息，请参阅 [重新初始化订阅](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 在此事务复制示例中， `DaysToManufacture` 列将从基于 `Product` 表的项目中删除。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_1.sql)]  
  
 在此合并复制示例中， `CreditCardApprovalCode` 列将从基于 `SalesOrderHeader` 表的项目中删除。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-colu_2.sql)]  
  
## 另请参阅  
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [筛选已发布数据](../../../relational-databases/replication/publish/filter-published-data.md)   
 [为合并复制筛选已发布数据](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  