---
title: "管理标识列 | Microsoft Docs"
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
  - "标识值 [SQL Server 复制]"
  - "合并复制 [SQL Server 复制], 标识范围管理"
  - "发布 [SQL Server 复制], 标识列"
  - "事务复制, 标识范围管理"
  - "标识列 [SQL Server], 复制"
ms.assetid: 98892836-cf63-494a-bd5d-6577d9810ddf
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# 管理标识列
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中管理标识列。 在将订阅服务器插入操作复制回发布服务器时，必须对标识列进行管理，以免在订阅服务器和发布服务器上分配相同的标识值。 复制可自动管理标识范围，或者您可以选择手动处理标识范围管理。  有关由复制提供的标识范围管理选项的信息，请参阅 [复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
-   **管理标识列，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
  
-   在多个发布中发布表时，必须为这些发布指定相同的标识范围管理选项。 详细信息，请参阅"发布表中多个发布"中 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
-   若要创建自动递增的数字，可以在多个表中使用，或者，可以从应用程序调用，而不引用任何表，请参阅 [序列号](../../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在上指定标识列管理选项 **属性** 的选项卡上 **项目属性-\< 项目>** 新建发布向导的对话框。 有关使用此向导的详细信息，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md)。 在新建发布向导中：  
  
-   如果您选择 **合并发布** 或 **带有更新订阅的事务性发布** 上 **发布类型** 页上，选择自动或手动标识范围管理 （自动进行的默认情况下，建议使用）。 在发布表后不能修改该属性，但可以修改其他相关属性。  
  
-   如果选择其他的发布类型，则应将标识范围管理设置为手动。  
  
 上修改标识范围和阈值 **属性** 的选项卡上 **项目属性-\< 项目>**, ，即位于 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 指定标识列管理选项  
  
1.  如果发布服务器运行的是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本，请在新建发布向导的 **“发布类型”** 页上，选择 **“合并发布”** 或 **“带有更新订阅的事务发布”**。  
  
2.  在 **“项目”** 页上，选择一个包含标识列的表。  
  
3.  单击 **“项目属性”**，再单击 **“设置突出显示的表项目的属性”**。  
  
4.  上 **属性** 的选项卡上 **项目属性-\< 文章>** 对话框中，在 **标识范围管理** 部分中，设置 **自动管理标识范围** 属性设置为 **自动** 或 **手动** (对于发布服务器运行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本)，或 **True** 或 **False** (的发布服务器运行的版本 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)])。  
  
5.  如果在步骤 4 中选择了 **“自动”** 或 **True** ，请输入下表中列出的选项值。 有关如何使用这些设置的详细信息，请参阅的"分配标识范围"部分 [复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
    |选项|值|说明|  
    |------------|-----------|-----------------|  
    |**发布服务器范围大小**|表示范围大小的整数值（例如 20000）。|请参阅的"分配标识范围"部分 [复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
    |**订阅服务器范围大小**|表示范围大小的整数值（例如 10000）。|请参阅的"分配标识范围"部分 [复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
    |**范围阈值百分比**|表示百分比阈值的整数值（例如，90 相当于 90%）。|指定新标识范围之前在节点上使用的总标识值的百分比。<br /><br /> <br /><br /> 注意：必须指定此值，但此值只用于：使用排队更新订阅的订阅服务器以及运行 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 或以前版本的其他 SQL Server 版本的合并发布的订阅服务器。 有关详细信息，请参阅的"分配标识范围"部分 [复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
    |**下一个范围的起始值**|整数值。 只读。|下一个范围的起始值。 例如，如果当前范围是 5001-6000，此起始值就是 6001。|  
    |**最大标识值**|整数值。 只读。|标识列的最大值。 由列的基本数据类型决定。|  
    |**增量**|整数值。 只读。|对于每个插入操作，标识列中的数字应增加或减少的量：通常设置为 1。|  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 发布表后修改标识范围和阈值  
  
1.  在 **文章** 页 **发布属性-\< 发布>** 对话框中，选择一个包含标识列的表。  
  
2.  单击 **“项目属性”**，再单击 **“设置突出显示的表项目的属性”**。  
  
3.  在 **属性** 的选项卡上 **项目属性-\< 项目>** 对话框中，在 **标识范围管理** 部分中，输入一个或多个以下属性的值︰ **发布服务器范围大小**, ，**订阅服务器范围大小**, ，和 **范围阈值百分比**。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  单击 **确定** 上 **发布属性-\< 发布>** 对话框。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 创建项目时，可使用复制存储过程来指定标识范围管理选项。  
  
#### 定义事务发布的项目时启用自动标识范围管理  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 要发布的源表具有标识列，如果指定的值 **自动** 为 **@identityrangemanagementoption**, ，分配到的发布服务器的标识值范围 **@pub_identity_range**, ，分配到的每个订阅服务器的标识值范围 **@identity_range**, ，并使用新的标识范围分配为之前的总标识值的百分比 **@threshold**。 有关如何定义项目的详细信息，请参阅 [定义项目](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  确保标识列的数据类型足够大，从而能够支持分配到所有订阅服务器的标识总范围。  
  
#### 定义事务发布的项目时禁用自动标识范围管理  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 将 **@identityrangemanagementoption** 的值指定为 **manual**。 有关如何定义项目的详细信息，请参阅 [定义项目](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  将范围分配到订阅服务器上的标识项目列，以避免在更新订阅服务器时产生冲突。 详细信息，请参阅部分上为主题中的手动标识范围管理分配范围 [复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
#### 定义合并发布的项目时启用自动标识范围管理  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 要发布的源表具有标识列，如果指定的值 **自动** 为 **@identityrangemanagementoption**, ，分配给服务器订阅有关的标识值范围 **@pub_identity_range**, ，分配给发布服务器和每个客户端订阅的标识值的范围 **@identity_range**, ，为分配新标识范围之前使用的总标识值的百分比 **@threshold**。 有关何时分配新标识范围的详细信息，请参阅分配标识范围主题 [复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)。 有关如何定义项目的详细信息，请参阅 [定义项目](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  确保标识列的数据类型足够大，从而能够支持分配到所有订阅服务器（尤其是具有服务器订阅的订阅服务器）的标识总范围。  
  
#### 定义合并发布的项目时禁用自动标识范围管理  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 为 **@identityrangemanagementoption**指定下列值之一：  
  
    -   **手动** -对更新订阅服务器，必须手动分配标识范围。  
  
    -   **无** -发布服务器上的标识列将不会被定义为订阅服务器上的标识列。  
  
     有关如何定义项目的详细信息，请参阅 [定义项目](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  将范围分配到订阅服务器上的标识项目列，以避免在更新订阅服务器时产生冲突。  
  
#### 为快照发布或事务发布中现有的项目更改自动标识范围管理设置  
  
1.  在发布服务器上对发布数据库中，执行 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md) 并记下的值 **identityrangemanagementoption** 结果集中。 如果该值为 **0**，则未启用自动标识范围管理。  
  
2.  如果结果集中 **identityrangemanagementoption** 的值为 **1**，则按下面的方法更改设置：  
  
    -   若要更改已分配的标识范围，执行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 发布服务器上对发布数据库。 将值指定为 **identity_range** 或 **pub_identity_range** 为 **@property** 和的新范围值 **@value**。  
  
    -   若要更改分配新范围的阈值，执行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 发布服务器上对发布数据库。 将 **@property** 的值指定为 **threshold** ，并为 **@value**指定新阈值。  
  
#### 为合并发布中的现有项目更改自动标识范围管理设置  
  
1.  在发布服务器上对发布数据库中，执行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) 并记下的值 **identity_support** 结果集中。 如果该值为 **0**，则未启用自动标识范围管理。  
  
2.  如果值 **identity_support** 在结果集是 **1**, ，更改设置，如下所示︰  
  
    -   若要更改已分配的标识范围，执行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 发布服务器上对发布数据库。 将值指定为 **identity_range** 或 **pub_identity_range** 为 **@property** 和的新范围值 **@value**。  
  
    -   若要更改分配新范围的阈值，执行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 发布服务器上对发布数据库。 将 **@property** 的值指定为 **threshold** ，并为 **@value**指定新阈值。 有关何时分配新标识范围的详细信息，请参阅分配标识范围主题 [复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
    -   若要禁用自动标识范围管理，请执行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 发布服务器上对发布数据库。 将 **@property** 的值指定为 **identityrangemanagementoption** ，并将 **@value** 的值指定为 **manual** 或 **none**。  
  
## 另请参阅  
 [对等事务复制](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  