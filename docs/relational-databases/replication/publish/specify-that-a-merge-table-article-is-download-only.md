---
title: "指定合并表项目仅用于下载 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 14839cec-6dbf-49c2-aa27-56847b09b4db
caps.latest.revision: "40"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf7eb381ded738c7b3fe2fd020e32e1a50df014c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="specify-that-a-merge-table-article-is-download-only"></a>指定合并表项目仅用于下载
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中指定合并表项目仅用于下载。 仅用于下载的项目是为具有不在订阅服务器上更新的数据的应用程序设计的。 有关详细信息，请参阅[使用仅下载项目优化合并复制性能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
-   **指定合并表项目仅用于下载，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   如果在初始化订阅后指定项目仅用于下载，则所有收到该项目的客户端订阅必须重新初始化。 服务器订阅不必重新初始化。 有关属性更改的影响的详细信息，请参阅[更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在新建发布向导的“项目”页或“项目属性 - \<项目>”对话框的“属性”选项卡上指定项目仅用于下载。 新建发布向导和“发布属性 - \<发布>”对话框中提供了该对话框。 有关如何使用该向导和如何访问该对话框的详细信息，请参阅[创建发布](../../../relational-databases/replication/publish/create-a-publication.md)和[查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-articles-page"></a>在“项目”页上指定项目仅用于下载  
  
-   在新建发布向导的 **“项目”** 页上，选择一个表，然后选中复选框 **“已选中的表仅用于下载”**。  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-properties-tab-of-the-article-properties---article-dialog-box"></a>在“项目属性 - \<项目>”对话框的“属性”选项卡上指定项目仅用于下载  
  
1.  在新建发布向导或“发布属性 - \<发布>”对话框的“项目”页上，选择一个表，然后单击“项目属性”。  
  
2.  单击 **“设置突出显示的表项目的属性”** 或 **“设置所有表项目的属性”**。  
  
3.  在“项目属性 - \<项目>”对话框的“属性”选项卡的“目标对象”部分中，为“同步方向”指定以下值之一：  
  
    -   **下载到订阅服务器，禁止订阅服务器更改**  
  
    -   **下载到订阅服务器，允许订阅服务器更改**  
  
4.  如果处于“发布属性 - \<发布>”对话框中，请单击“确定”以保存并关闭该对话框。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-specify-that-a-new-merge-table-article-is-download-only"></a>指定新合并表项目仅用于下载  
  
1.  执行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)，为参数 **@subscriber_upload_options** 在 **1** 或 **@subscriber_upload_options**指定合并表项目仅用于下载。 这些数字分别与以下行为相对应：  
  
    -   **0** - 无限制（默认值）。 将订阅服务器上所做的更改上载到发布服务器。  
  
    -   **1** - 允许在订阅服务器上进行更改，但不会将它们上载到发布服务器。  
  
    -   **2** - 不允许在订阅服务器上进行更改。  
  
        > [!NOTE]  
        >  如果某个项目的源表已经在另一个发布中发布，则两个项目的 **@subscriber_upload_options** 值必须相同。  
  
#### <a name="to-modify-an-existing-merge-table-article-to-be-download-only"></a>修改现有合并表项目以使其仅用于下载  
  
1.  若要确定项目是否仅用于下载，请执行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 记下结果集中该项目的 **upload_options** 值。  
  
2.  如果在步骤 1 中返回的值为 **0**，则执行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)，为参数 **@property** 指定值 **@property**，为 **@subscriber_upload_options** 指定值 **@force_invalidate_snapshot** 和 **@force_reinit_subscription**并为 **@subscriber_upload_options** 在 **1** 指定值 **@value**，这里的数字分别对应于以下行为：  
  
    -   **1** - 允许在订阅服务器上进行更改，但不会将它们上载到发布服务器。  
  
    -   **2** - 不允许在订阅服务器上进行更改。  
  
        > [!NOTE]  
        >  如果某个项目的源表已经在另一个发布中发布，则两个项目的仅用于下载行为必须相同。  
  
## <a name="see-also"></a>另请参阅  
 [使用仅下载项目优化合并复制性能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [查看和修改项目属性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  
