---
title: "优化参数化行筛选器 | Microsoft Docs"
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
  - "预计算分区 [SQL Server 复制]"
  - "筛选器 [SQL Server 复制], 参数化"
  - "合并复制预计算分区 [SQL Server 复制], SQL Server Management Studio"
  - "参数化筛选器 [SQL Server 复制], 优化"
ms.assetid: 49349605-ebd0-4757-95be-c0447f30ba13
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 优化参数化行筛选器
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中优化参数化行筛选器。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
-   **优化参数化行筛选器，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
  
-   当使用参数化筛选器时，可通过在创建发布时指定 **use partition groups** 或 **keep partition changes** 选项来控制合并复制处理筛选器的方式。 通过将其他元数据存储在发布数据库中，上述选项可提高具有已筛选项目的发布的同步性能。 通过在创建项目时设置 **partition options** ，您可以控制在订阅服务器之间共享数据的方式。 有关这些要求的详细信息，请参阅 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
     使用 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] SQL Server Compact 订阅服务器时，keep_partition_changes 必须设置为 true 以确保正确传播删除操作。 设置为 false 时，订阅服务器可能有比预期更多的行。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 以下设置可用于优化参数化行筛选器：  
  
 **分区选项**  
 此选项设置为 on **属性** 页 **项目属性-\< 项目>** 对话框中，或在 **添加筛选器** 对话框。 这两个对话框可用于新建发布向导和 **发布属性-\< 发布>** 对话框。  **项目属性-\< 项目>** 对话框允许您指定此选项中均不提供的其他值 **添加筛选器** 对话框。  
  
 **预计算分区**  
 此选项设置为 **True** 默认情况下，如果在出版物中的项目符合一组的要求。 有关这些要求的详细信息，请参阅 [使用预计算分区优化参数化筛选器性能](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)。 修改此选项在 **订阅选项** 页 **发布属性-\< 发布>** 对话框。  
  
 **优化同步**  
 此选项应设置为 **True** 才 **预计算分区** 设置为 **False**。 此选项设置为 on **订阅选项** 页 **发布属性-\< 发布>** 对话框。  
  
 有关使用新建发布向导和访问的详细信息 **发布属性-\< 发布>** 对话框中，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md) 和 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 在“添加筛选器”或“编辑筛选器”对话框中设置分区选项。  
  
1.  在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>** 对话框中，单击 **添加**, ，然后单击 **添加筛选器**。  
  
2.  创建参数化筛选器。 有关详细信息，请参阅 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
3.  选择指示订阅服务器之间如何共享数据的选项：  
  
    -   **此表中的行将转到多个订阅**  
  
    -   **此表中的行将仅转到一个订阅**  
  
     如果选择 **“此表中的行将仅转到一个订阅”**，则合并复制可以通过存储和处理较少的元数据来优化性能。 但是，必须确保在对数据分区时不能将行复制到多个订阅服务器。 有关详细信息，请参阅主题 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)中的“设置‘分区选项’”部分。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您在 **发布属性-\< 发布>** 对话框中，单击 **确定** 以保存并关闭对话框。  
  
#### 若要设置分区选项，在项目属性-\< 项目> 对话框  
  
1.  在 **文章** 新建发布向导的页面或 **发布属性-\< 发布>** 对话框中，选择一个表，然后单击 **项目属性**。  
  
2.  单击 **“设置突出显示的表项目的属性”** 或 **“设置所有表项目的属性”**。  
  
3.  在 **目标对象** 部分 **属性** 的选项卡上 **项目属性-\< 项目>** 对话框框中，指定以下值之一 **分区选项**:  
  
    -   **重叠**  
  
    -   **重叠，不允许分区外的数据更改**  
  
    -   **不重叠，一个订阅**  
  
    -   **不重叠，由所有订阅共享**  
  
     有关这些选项以及它们与 **“添加筛选器”** 和 **“编辑筛选器”** 对话框中选项的关系的详细信息，请参阅 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)的“设置‘分区选项’”部分。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您在 **发布属性-\< 发布>** 对话框中，单击 **确定** 以保存并关闭对话框。  
  
#### 设置预计算分区  
  
1.  在 **订阅选项** 页 **发布属性-\< 发布>** 对话框中，选择一个值作为 **预计算分区** 选项。 在以下情况下，则此属性为只读：  
  
    -   发布不满足对预计算分区的要求。  
  
    -   尚未为发布生成快照。 这种情况下，该选项会显示 **“创建快照时自动设置”**值。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 设置优化同步  
  
1.  在 **订阅选项** 页 **发布属性-\< 发布>** 对话框中，选择一个值的 **True** 为 **优化同步** 选项。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 有关定义的筛选选项 **@keep_partition_changes** 和 **@use_partition_groups**, ，请参阅 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。  
  
#### 创建新发布时指定合并筛选器的优化  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 指定 **@publication** ，并将值 **true** 指定给以下参数之一：  
  
    -   **@use_partition_groups**:-高级别的性能优化，提供项目符合预计算分区的要求。 有关详细信息，请参阅 [使用预计算分区优化参数化筛选器性能](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)。  
  
    -   **@keep_partition_changes** -如果使用预计算分区不能将使用此优化。  
  
2.  为发布添加一个快照作业。 有关详细信息请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
3.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), ，指定以下参数︰  
  
    -   **@publication** -步骤 1 中发布的名称。  
  
    -   **@article** -项目的名称，  
  
    -   **@source_object** -要发布的数据库对象。  
  
    -   **@subset_filterclause** -用于水平筛选项目的可选参数化筛选器子句。  
  
    -   **@partition_options** -筛选项目的分区选项。  
  
4.  对发布中的每个项目重复步骤 3。  
  
5.  （可选）在发布服务器上对发布数据库中，执行 [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 来定义两个项目之间的联接筛选器。 有关详细信息，请参阅 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
#### 查看和修改现有发布的合并筛选器行为  
  
1.  （可选）在发布服务器上对发布数据库中，执行 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), ，并指定 **@publication**。 记下的值 **keep_partition_changes** 和 **use_partition_groups** 结果集中。  
  
2.  （可选）在发布服务器上对发布数据库中，执行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 将值指定为 **use_partition_groups** 为 **@property** 和任一 **true** 或 **false** 为 **@value**。  
  
3.  （可选）在发布服务器上对发布数据库中，执行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 将值指定为 **keep_partition_changes** 为 **@property** 和任一 **true** 或 **false** 为 **@value**。  
  
    > [!NOTE]  
    >  启用时 **keep_partition_changes**, ，则必须首先禁用 **use_partition_groups** 并将值指定为 **1** 为 **@force_reinit_subscription**。  
  
4.  （可选）在发布服务器上对发布数据库中，执行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 将值指定为 **partition_options** 为 **@property** 和适当的值 **@value**。 请参阅 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 有关的这些定义筛选选项。  
  
5.  （可选）启动快照代理以重新生成快照（如果需要）。 有关哪些更改需要生成新快照的信息，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
## 另请参阅  
 [自动生成一组合并项目 & #40; 之间的联接筛选器SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md)   
 [定义和修改合并项目的参数化行筛选器](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [参数化行筛选器](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  