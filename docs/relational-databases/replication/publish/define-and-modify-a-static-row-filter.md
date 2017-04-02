---
title: "定义和修改静态行筛选器 | Microsoft Docs"
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
  - "修改筛选器, 静态行"
  - "静态行筛选器"
  - "筛选器 [SQL Server 复制], 静态行"
ms.assetid: a6ebb026-026f-4c39-b6a9-b9998c3babab
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 定义和修改静态行筛选器
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定义和修改静态行筛选器。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
-   **定义和修改静态行筛选器，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   如果在初始化对发布的订阅后添加、修改或删除静态行筛选器，则必须在更改后生成新的快照并重新初始化所有订阅。 有关属性更改要求的详细信息，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
-   如果为对等事务复制启用了发布，则不能筛选表。  
  
###  <a name="Recommendations"></a> 建议  
  
-   由于这些筛选器是静态的，因此所有订阅服务器都将接收到相同的数据子集。 如果您需要在属于合并发布的表项目中动态筛选行，以使每一订阅服务器都能接收到不同的数据分区，请参阅 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。 您还可使用合并复制基于现有的行筛选器筛选相关的行。 有关详细信息，请参阅 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 定义、 修改和删除静态行筛选器在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>** 对话框。 有关使用向导和访问对话框中的详细信息，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md) 和 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 定义静态行筛选器  
  
1.  在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>** 对话框中，要采取的操作取决于发布的类型︰  
  
    -   对于快照发布或事务发布，请单击 **“添加”**。  
  
    -   对于合并发布，请单击 **“添加”**，再单击 **“添加筛选器”**。  
  
2.  在 **添加筛选器** 对话框中，选择要从下拉列表框中筛选的表。  
  
3.  在 **“筛选语句”** 文本区域创建筛选语句。 您可以在文本区域中直接键入，也可以从 **“列”** 列表框中拖放列。  
  
    > [!NOTE]  
    >  WHERE 子句应使用由两部分构成的命名方式，不支持由三部分和四部分构成的命名方式。 如果发布来自 Oracle 发布服务器，则 WHERE 子句必须符合 Oracle 语法。  
  
    -   **“筛选语句”** 文本区域包括默认的文本，其格式为：  
  
        ```tsql  
        SELECT <published_columns> FROM [schema].[tablename] WHERE  
        ```  
  
    -   默认文本无法更改；请使用标准的 SQL 语法在 WHERE 关键字后键入筛选子句。 完整筛选子句如下所示：  
  
        ```tsql  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE [LoginID] = 'adventure-works\ranjit0'  
        ```  
  
    -   静态行筛选器可以包含用户定义函数。 包含用户定义函数的静态行筛选器的完整筛选子句如下所示：  
  
        ```tsql  
        SELECT <published_columns> FROM [Sales].[SalesOrderHeader] WHERE MyFunction([Freight]) > 100  
        ```  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您在 **发布属性-\< 发布>** 对话框中，单击 **确定** 以保存并关闭对话框。  
  
#### 修改静态行筛选器  
  
1.  在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>** 对话框中选择筛选器 **筛选的表** 窗格中，然后再单击 **编辑**。  
  
2.  在 **“编辑筛选器”** 对话框中，修改筛选器。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 删除静态行筛选器  
  
1.  在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>** 对话框中选择筛选器 **筛选的表** 窗格中，然后再单击 **删除**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 在创建表项目时，可以定义 WHERE 子句以筛选项目中的行。 定义行筛选器后，还可以对其进行更改。 可使用复制存储过程以编程的方式创建和修改静态行筛选器。  
  
#### 为快照发布或事务发布定义静态行筛选器  
  
1.  定义要筛选的项目。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_articlefilter & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)。 指定项目的名称 **@article**, ，为发布的名称 **@publication**, ，为筛选器的名称 **@filter_name**, ，和为筛选子句 **@filter_clause** (不包括 `WHERE`)。  
  
3.  如果还必须定义列筛选器，请参阅 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。 否则，执行 [sp_articleview & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 指定为发布名称 **@publication**, ，筛选项目的名称 **@article**, ，并指定步骤 2 中的筛选器子句 **@filter_clause**。 这将为筛选的项目创建同步对象。  
  
#### 为快照发布或事务发布修改静态行筛选器  
  
1.  在发布服务器上对发布数据库中，执行 [sp_articlefilter & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)。 指定项目的名称 **@article**, ，为发布的名称 **@publication**, ，为新的筛选器的名称 **@filter_name**, ，并为新的筛选子句 **@filter_clause** (不包括 `WHERE`)。 由于此更改将使现有订阅中的数据失效，将值指定为 **1** 为 **@force_reinit_subscription**。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_articleview & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。 指定为发布名称 **@publication**, ，筛选项目的名称 **@article**, ，并在步骤 1 中指定的筛选器子句 **@filter_clause**。 这将重新创建定义筛选项目的视图。  
  
3.  对发布重新运行快照代理作业以生成更新的快照。 有关详细信息，请参阅 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
4.  重新初始化订阅。 有关详细信息，请参阅 [重新初始化订阅](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### 为快照发布或事务发布删除静态行筛选器  
  
1.  在发布服务器上对发布数据库中，执行 [sp_articlefilter & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)。 指定项目的名称 **@article**, ，为发布的名称 **@publication**, ，其值为 NULL 的 **@filter_name**, ，且值为 NULL 表示 **@filter_clause**。 由于此更改将使现有订阅中的数据失效，将值指定为 **1** 为 **@force_reinit_subscription**。  
  
2.  对发布重新运行快照代理作业以生成更新的快照。 有关详细信息，请参阅 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
3.  重新初始化订阅。 有关详细信息，请参阅 [重新初始化订阅](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
#### 为合并发布定义静态行筛选器  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定为筛选子句 **@subset_filterclause** (不包括 `WHERE`)。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  如果还必须定义列筛选器，请参阅 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
#### 为合并发布修改静态行筛选器  
  
1.  在发布服务器上对发布数据库中，执行 [sp_changemergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定为发布名称 **@publication**, ，筛选项目的名称 **@article**, ，值为 **subset_filterclause** 为 **@property**, ，并为新的筛选子句 **@value** (不包括 `WHERE`)。 由于此更改将使现有订阅中的数据失效，指定的值为 1 **@force_reinit_subscription**。  
  
2.  对发布重新运行快照代理作业以生成更新的快照。 有关详细信息，请参阅 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
3.  重新初始化订阅。 有关详细信息，请参阅 [重新初始化订阅](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 在此事务复制示例中，对项目进行水平筛选以删除所有停产的产品。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_1.sql)]  
  
 在此合并复制示例中，对项目进行水平筛选以仅返回属于指定销售人员的行。 其中还使用了联接筛选器。 有关详细信息，请参阅 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-stat_2.sql)]  
  
## 另请参阅  
 [定义和修改合并项目的参数化行筛选器](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [筛选已发布数据](../../../relational-databases/replication/publish/filter-published-data.md)   
 [为合并复制筛选已发布数据](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  