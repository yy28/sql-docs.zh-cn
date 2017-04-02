---
title: "指定合并表项目仅用于下载 | Microsoft Docs"
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
  - "合并复制 [SQL Server 复制], 仅下载项目"
  - "项目 [SQL Server 复制], 仅下载"
  - "仅下载项目"
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# 指定合并表项目仅用于下载
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指定合并表项目仅用于下载。 仅用于下载的项目是为具有不在订阅服务器上更新的数据的应用程序设计的。 有关详细信息，请参阅 [对 Download-Only 项目优化合并复制性能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
-   **指定合并表项目仅用于下载，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   如果在初始化订阅后指定项目仅用于下载，则所有收到该项目的客户端订阅必须重新初始化。 服务器订阅不必重新初始化。 效果属性更改的详细信息，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 指定项目为仅下载上 **文章** 新建发布向导的页面或 **属性** 的选项卡上 **项目属性-\< 项目>** 对话框。 此对话框可在新建发布向导和 **发布属性-\< 发布>** 对话框。 有关使用向导和访问对话框中的详细信息，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md) 和 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 在“项目”页上指定项目仅用于下载  
  
-   在 **文章** 页中的新建发布向导选择一个表，然后选择复选框 **突出显示表仅用于下载**。  
  
#### 若要指定一篇文章是仅下载项目属性-属性选项卡上 \< 文章> 对话框  
  
1.  在 **文章** 新建发布向导的页面或 **发布属性-\< 发布>** 对话框中，选择一个表，然后单击 **项目属性**。  
  
2.  单击 **“设置突出显示的表项目的属性”** 或 **“设置所有表项目的属性”**。  
  
3.  在 **目标对象** 部分 **属性** 的选项卡上 **项目属性-\< 项目>** 对话框框中，指定以下值之一 **同步方向**:  
  
    -   **下载到订阅服务器，禁止订阅服务器更改**  
  
    -   **下载到订阅服务器，允许订阅服务器更改**  
  
4.  如果您在 **发布属性-\< 发布>** 对话框中，单击 **确定** 以保存并关闭对话框。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 指定新合并表项目仅用于下载  
  
1.  执行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), ，将值指定为 **1** 或 **2** 参数 **@subscriber_upload_options**。 这些数字分别与以下行为相对应：  
  
    -   **0** -无限制 （默认值）。 将订阅服务器上所做的更改上载到发布服务器。  
  
    -   **1** -允许在订阅服务器上，进行更改，但不是将其上载到发布服务器。  
  
    -   **2** -不允许在订阅服务器上进行更改。  
  
        > [!NOTE]  
        >  如果在另一个发布中，值的已发布项目的源表 **@subscriber_upload_options** 必须是两个项目相同的。  
  
#### 修改现有合并表项目以使其仅用于下载  
  
1.  若要确定项目是否仅下载，请执行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 记下的值 **upload_options** 对于结果中的项目设置。  
  
2.  如果中返回的值是第 1 步 **0**, ，执行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), ，指定的值 **subscriber_upload_options** 为 **@property**, ，值为 **1** 为 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**, ，且值为 **1** 或 **2** 为 **@value**, ，对应于以下行为︰  
  
    -   **1** -允许在订阅服务器上，进行更改，但不是将其上载到发布服务器。  
  
    -   **2** -不允许在订阅服务器上进行更改。  
  
        > [!NOTE]  
        >  如果某个项目的源表已经在另一个发布中发布，则两个项目的仅用于下载行为必须相同。  
  
## 另请参阅  
 [使用仅下载项目优化合并复制的性能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [定义项目](../../../relational-databases/replication/publish/define-an-article.md)   
 [查看和修改项目属性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  