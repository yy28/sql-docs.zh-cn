---
title: "定义和修改合并项目间的联接筛选器 | Microsoft Docs"
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
  - "筛选器 [SQL Server 复制], 联接"
  - "合并复制联接筛选器 [SQL Server 复制]"
  - "修改筛选器, 联接"
  - "联接筛选器"
ms.assetid: f7f23415-43ff-40f5-b3e0-0be1d148ee5b
caps.latest.revision: 46
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# 定义和修改合并项目间的联接筛选器
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定义和修改合并项目间的联接筛选器。 合并复制支持联接筛选器，这类筛选器通常与参数化筛选器配合使用，以将表分区扩展到其他相关的表项目。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
-   **定义和修改合并项目间的联接筛选器，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   若要创建联接筛选器，发布必须至少包含两个相关表。 联接筛选器可扩展行筛选器；因此必须先对一个表定义行筛选器，才能使用联接将该筛选器扩展到另一个表。 定义一个联接筛选器后，如果发布包含更多相关表，则可使用其他联接筛选器来扩展此联接筛选器。  
  
-   如果在初始化对发布的订阅后添加、修改或删除联接筛选器，必须在更改后生成新的快照并重新初始化所有订阅。 有关属性更改要求的详细信息，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
###  <a name="Recommendations"></a> 建议  
  
-   可以为一组表手动创建联接筛选器，或者复制可以基于表上定义的外键和主键之间的关系自动生成筛选器。 自动生成一组联接筛选器的详细信息，请参阅 [自动生成设置联接筛选器之间合并项目的 & #40;SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 定义、 修改和删除联接筛选器在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>** 对话框。 有关使用向导和访问对话框中的详细信息，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md) 和 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 定义联接筛选器  
  
1.  在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>**, 中，选择现有的行筛选器或联接筛选器 **筛选的表** 窗格。  
  
2.  单击 **“添加”**，再单击 **“添加联接以扩展所选筛选器”**。  
  
3.  创建联接语句：选择 **“使用生成器创建语句”** 或 **“手动编写联接语句”**。  
  
    -   如果您选择使用生成器，则使用网格中的列 (**一起**, ，**筛选的表列**, ，**运算符**, ，和 **联接的表列**) 来生成联接语句。  
  
         在网格中的每列都包含下拉组合框中，从而允许您选择两个列和一个运算符 (**=**, ，**<>**, ，**<=**, ，**\<**, ，**>=**, ，**>**, ，和 **如**)。 结果显示在 **“预览”** 文本区域中。 如果联接中涉及的列的多个对，选择一个连接词 (或或) 从 **结合使用** 列中，然后输入两个多个列和一个运算符。  
  
    -   如果选择手动编写语句，那么请在 **“联接语句”** 文本区域编写联接语句。 使用 **“筛选的表列”** 列表框和 **“联接的表列”** 列表框将列拖放到 **“联接语句”** 文本区域。  
  
    -   完整的联接语句如下所示：  
  
        ```  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] INNER JOIN [Sales].[SalesOrderDetail] ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID]  
        ```  
  
         JOIN 子句应使用由两个部分组成的名称来命名；它不支持由三个部分和四个部分组成的名称命名。  
  
4.  指定联接选项：  
  
    -   如果要筛选的表 （父表） 中联接的列是唯一的请选择 **唯一键**。  
  
        > [!CAUTION]  
        >  选择此选项表示联接筛选器中子表和父表是一对一还是一对多的关系。 仅当子表的联接列上具有保证唯一性的约束时才选择此选项。 如果未能正确设置此选项，可能无法收敛数据。  
  
    -   默认情况下，合并复制在同步过程中会逐行处理更改。 若要有相关的已筛选的表和联接的表作为一个单元处理的行中的更改，请选择 **逻辑记录** ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本)。 只有满足使用逻辑记录的项目和发布要求，此选项才可用。 详细信息请参阅"使用逻辑记录的注意事项"部分中 [通过逻辑记录对相关行组更改](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  如果您在 **发布属性-\< 发布>** 对话框中，单击 **确定** 以保存并关闭对话框。  
  
#### 修改联接筛选器  
  
1.  在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>**, ，选择一个筛选器中的 **筛选的表** 窗格中，然后再单击 **编辑**。  
  
2.  在 **“编辑联接”** 对话框中，修改筛选器。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 删除联接筛选器  
  
1.  在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>**, ，选择一个筛选器中的 **筛选的表** 窗格中，然后再单击 **删除**。 如果删除的联接筛选器自身是由其他联接扩展而成的，则也将删除那些联接。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 这些过程显示了父项目上的参数化筛选器以及该项目和相关子项目间的联接筛选器。 可以使用复制存储过程，以编程方式定义和修改联接筛选器。  
  
#### 定义联接筛选器以将项目筛选器扩展到合并发布中的相关项目  
  
1.  为要联接到的项目（又称为父项目）定义筛选。  
  
    -   对于使用参数化行筛选器筛选的项目，请参阅 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
    -   对于使用静态行筛选器筛选的项目，请参阅 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 若要定义一个或多个相关实参也称为子项目，为发布的文章。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
3.  在发布服务器上对发布数据库中，执行 [sp_addmergefilter & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)。 指定 **@publication**, ，此筛选器的唯一名称 **@filtername**, ，步骤 2 中创建的子项目的名称 **@article**, ，为要联接到父项目的名称 **@join_articlename**, ，以及下列其中一项值为 **@join_unique_key**:  
  
    -   **0** -表示父和子项目之间多对一或多对多联接。  
  
    -   **1** -表示父和子项目间的一对一或一对多联接。  
  
     此步骤定义了两个项目间的联接筛选器。  
  
    > [!CAUTION]  
    >  只能设置 **@join_unique_key** 到 **1** 如果保证唯一性的父项目的基础表中具有的联接列上的约束。 如果 **@join_unique_key** 设置为 **1** 不正确，可能会出现数据无法收敛。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此示例定义了合并发布的项目，并针对 `SalesOrderDetail` 表来筛选 `SalesOrderHeader` 表项目，而该表本身使用静态行筛选器进行筛选。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_1.sql)]  
  
 此示例在合并发布，其中包含一系列联接筛选器基于筛选的项目中定义的一组项目 `Employee` ，它是表本身的值中使用参数化的行筛选器 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) 中 **LoginID** 列。 有关详细信息，请参阅 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-join_2.sql)]  
  
## 另请参阅  
 [联接筛选器](../../../relational-databases/replication/merge/join-filters.md)   
 [参数化行筛选器](../../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [为合并复制筛选已发布数据](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [如何定义和修改合并项目间的联接筛选器 (SQL Server Management Studio)](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [定义合并表项目间的逻辑记录关系](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [定义和修改合并项目的参数化行筛选器](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
  