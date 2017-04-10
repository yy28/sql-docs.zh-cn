---
title: "定义和修改合并项目的参数化行筛选器 | Microsoft Docs"
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
  - "参数化筛选器 [SQL Server 复制]，正在定义"
  - "参数化筛选器 [SQL Server 复制]，正在修改"
  - "合并复制 [SQL Server 复制]，动态筛选器"
  - "合并复制参数化筛选器 [SQL Server 复制]"
  - "筛选器 [SQL Server 复制], 参数化"
  - "修改筛选器，参数化行"
  - "动态筛选器 [SQL Server 复制]"
ms.assetid: de0482a2-3cc8-4030-8a4a-14364549ac9f
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 定义和修改合并项目的参数化行筛选器
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中定义和修改参数化行筛选器。  
  
 在创建表项目时，可以使用参数化行筛选器。 这些筛选器使用 [WHERE](../../../t-sql/queries/where-transact-sql.md) 子句来选择要发布的相应数据。 而不是在子句中指定文字值 （像在静态行筛选器那样），指定一个或两个以下系统函数︰ [SUSER_SNAME](../../../t-sql/functions/suser-sname-transact-sql.md) 和 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md)。 有关详细信息，请参阅 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
-   **定义和修改参数化行筛选器，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   如果在初始化对发布的订阅后添加、修改或删除参数化行筛选器，必须在更改后生成新的快照并重新初始化所有订阅。 有关属性更改要求的详细信息，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
###  <a name="Recommendations"></a> 建议  
  
-   出于性能方面的考虑，我们建议您不要将这些函数应用于参数化行筛选器子句（如 `LEFT([MyColumn]) = SUSER_SNAME()`）中的列名。 如果在筛选子句中使用 HOST_NAME 并覆盖 HOST_NAME 值，则可能需要使用 CONVERT 转换数据类型。 有关这种情况下的最佳做法的详细信息，请参阅主题中的"覆盖 host_name （） 值"一节 [参数化行筛选器](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 定义、 修改和删除参数化的行筛选器在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>** 对话框。 有关使用向导和访问对话框中的详细信息，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md) 和 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 定义参数化行筛选器  
  
1.  在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>**, ，单击 **添加**, ，然后单击 **添加筛选器**。  
  
2.  在 **添加筛选器** 对话框中，选择要从下拉列表框中筛选的表。  
  
3.  在 **“筛选语句”** 文本框中创建一个筛选语句。 您可以在文本区域中直接键入，也可以从 **“列”** 列表框中拖放列。  
  
    -   **“筛选语句”** 文本区域包括默认的文本，其格式为：  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
    -   默认文本无法更改；请使用标准的 SQL 语法在 WHERE 关键字后键入筛选子句。 参数化筛选器包括对系统函数的调用 **host_name （)** 和/或 **suser_sname （)**, ，或引用了一个或两个这些函数的用户定义函数。 以下是参数化行筛选器的一个完整筛选子句的示例：  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         WHERE 子句应使用由两部分构成的命名方式，不支持由三部分和四部分构成的命名方式。  
  
4.  选择指示订阅服务器之间如何共享数据的选项：  
  
    -   **此表中的行将转到多个订阅**  
  
    -   **此表中的行将仅转到一个订阅**  
  
     如果选择 **“此表中的行将仅转到一个订阅”**，则合并复制可以通过存储和处理较少的元数据来优化性能。 但是，必须确保在对数据分区时不能将行复制到多个订阅服务器。 有关详细信息，请参阅主题 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)中的“设置‘分区选项’”部分。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  如果您在 **发布属性-\< 发布>** 对话框中，单击 **确定** 以保存并关闭对话框。  
  
#### 修改参数化行筛选器  
  
1.  在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>**, ，选择一个筛选器中的 **筛选的表** 窗格中，然后再单击 **编辑**。  
  
2.  在 **“编辑筛选器”** 对话框中，修改筛选器。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 删除参数化行筛选器  
  
1.  在 **筛选表行** 新建发布向导的页面或 **筛选行** 页 **发布属性-\< 发布>**, ，选择一个筛选器中的 **筛选的表** 窗格中，然后再单击 **删除**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式创建和修改参数化行筛选器。  
  
#### 为合并发布中的项目定义参数化行筛选器  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定 **@publication**, ，项目的名称，为 **@article**, 、 要发布的表 **@source_object**, ，定义的参数化筛选器的 WHERE 子句 **@subset_filterclause** (不包括 `WHERE`)，以及下列其中一项值为 **@partition_options**, ，其中描述的参数化的行筛选器可能会导致分区类型︰  
  
    -   **0** -对项目可以是静态的或者不生成唯一的每个分区 （"重叠"分区） 的数据子集的筛选。  
  
    -   **1** -导致分区重叠，并在订阅服务器上所做的更新无法更改行所属的分区。  
  
    -   **2** -项目筛选将生成不重叠分区，但在多个订阅服务器可以接收相同的分区。  
  
    -   **3** -对每个订阅都是唯一的项目会生成不重叠分区的筛选。  
  
#### 更改合并发布中的项目的参数化行筛选器  
  
1.  在发布服务器上对发布数据库中，执行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定 **@publication**, ，**@article**, ，值为 **subset_filterclause** 为 **@property**, ，定义的参数化筛选器的表达式 **@value** (不包括 `WHERE`)，并将值 **1** 两个 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**。  
  
2.  如果此更改导致不同的分区行为，然后执行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 再次。 指定 **@publication**, ，**@article**, ，值为 **partition_options** 为 **@property**, ，并最适当的分区选项 **@value**, ，可以是以下项之一︰  
  
    -   **0** -对项目可以是静态的或者不生成唯一的每个分区 （"重叠"分区） 的数据子集的筛选。  
  
    -   **1** -导致分区重叠，并在订阅服务器上所做的更新无法更改行所属的分区。  
  
    -   **2** -项目筛选将生成不重叠分区，但在多个订阅服务器可以接收相同的分区。  
  
    -   **3** -对每个订阅都是唯一的项目会生成不重叠分区的筛选。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此示例在合并发布中定义一组项目，其中的项目是使用一系列联接筛选器基于 `Employee` 表筛选的，而该表则是使用参数化行筛选器基于 **LoginID** 列进行自身筛选的。 在同步期间，返回的值 [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) 中重写函数。 有关详细信息，请参阅替代主题中的 host_name （） 值 [参数化行筛选器](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../../relational-databases/replication/codesnippet/tsql/define-and-modify-a-para_1.sql)]  
  
## 另请参阅  
 [定义和修改合并项目间的联接筛选器](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [联接筛选器](../../../relational-databases/replication/merge/join-filters.md)   
 [参数化行筛选器](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  