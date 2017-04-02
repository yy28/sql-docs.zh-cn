---
title: "通过参数化筛选器为合并发布管理分区 | Microsoft Docs"
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
  - "分区 [SQL Server 复制]"
  - "合并复制分区 [SQL Server 复制], SQL Server Management Studio"
  - "参数化筛选器 [SQL Server 复制], 分区管理"
ms.assetid: fb5566fe-58c5-48f7-8464-814ea78e6221
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 通过参数化筛选器为合并发布管理分区
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中通过参数化筛选器为合并发布管理分区。 参数化行筛选器可用于生成不重叠的分区。 可以限制这些分区，以便只有一个订阅接收到给定分区。 在这类情况下，大量订阅服务器将导致大量的分区，从而需要同等数量的分区快照。 有关详细信息，请参阅 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
-   **通过参数化筛选器为合并发布管理分区，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
  
-   如果对复制拓扑编写脚本（建议这样做），则发布脚本包含用于创建数据分区的存储过程调用。 该脚本提供了对所创建的分区的引用和一种在必要时重建分区的途径。 有关详细信息，请参阅 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)。  
  
-   如果发布具有的参数化筛选器可生成带有非重叠分区的订阅，并且如果特定订阅丢失并需要重新创建，则您必须执行以下操作：删除曾订阅的分区，重新创建订阅，然后重新创建该分区。 有关详细信息，请参阅 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)。 生成发布创建脚本时，复制会为现有订阅服务器分区生成创建脚本。 有关详细信息，请参阅 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 管理分区上 **数据分区** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。 在此页上，可以执行下列操作：创建和删除分区、允许订阅服务器启动快照的生成和传递、生成一个或多个分区的快照和清除快照。  
  
#### 创建分区  
  
1.  在 **数据分区** 页 **发布属性-\< 发布>** 对话框中，单击 **添加**。  
  
2.  在 **添加数据分区** 对话框框中，输入一个值 **host_name （)** 和/或 **suser_sname （)** 与你想要创建的分区相关联的值。  
  
3.  还可以指定快照刷新计划：  
  
    1.  选择 **安排此分区在以下时间运行快照代理程序**  
  
    2.  接受默认的快照刷新计划，或者单击 **“更改”** 以指定其他计划。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 删除分区  
  
1.  在 **“数据分区”** 页上，在网格中选择分区。  
  
2.  单击 **“删除”**。  
  
#### 允许订阅服务器启动快照的生成和传递  
  
1.  在 **“数据分区”** 页上，选择 **“在新订阅服务器尝试同步时，根据需要自动定义分区并生成快照”**。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 生成分区快照  
  
1.  在 **“数据分区”** 页上，在网格中选择分区。  
  
2.  单击 **“立即生成所选快照”**  
  
#### 清除分区快照  
  
1.  在 **“数据分区”** 页上，在网格中选择分区。  
  
2.  单击 **“清除现有快照”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 为了更好地管理带有参数化筛选器的发布，可使用复制存储过程以编程方式枚举现有的分区。 还可以创建和删除现有的分区。 可以获取以下有关现有分区的信息：  
  
-   如何筛选分区 (使用 [SUSER_SNAME & #40;Transact SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md) 或 [HOST_NAME & #40;Transact-SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md))。  
  
-   用于生成分区快照的作业的名称。  
  
-   分区快照作业上次运行的时间。  
  
 尽管在初始化新订阅时可以按需生成由两部分构成的快照的第二部分，但通过下面的过程可以控制此快照的生成方式，并在最方便的时候预生成该快照。 有关详细信息，请参阅 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
#### 查看有关现有分区的信息  
  
1.  在发布服务器上对发布数据库中，执行 [sp_helpmergepartition & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)。 为 **@publication**指定发布的名称。 （可选）指定 **@suser_sname** 或 **@host_name** 返回只根据单个筛选条件的信息。  
  
#### 定义新分区并生成新分区快照  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergepartition & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)。 为 **@publication**指定发布的名称，并为以下某个参数指定用于定义分区的参数化值：  
  
    -   **@suser_sname** -当参数化筛选器定义返回的值由 [SUSER_SNAME & #40;Transact SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md)。  
  
    -   **@host_name** -当参数化筛选器定义返回的值由 [HOST_NAME & #40;Transact SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md)。  
  
2.  创建并初始化此新分区的参数化快照。 有关详细信息，请参阅 [Create a Snapshot for a Merge Publication with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
#### 删除分区  
  
1.  在发布服务器上对发布数据库中，执行 [sp_dropmergepartition & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)。 为 **@publication** 指定发布的名称，并为以下某个参数指定用于定义分区的参数化值：  
  
    -   **@suser_sname** -当参数化筛选器定义返回的值由 [SUSER_SNAME & #40;Transact SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md)。  
  
    -   **@host_name** -当参数化筛选器定义返回的值由 [HOST_NAME & #40;Transact SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md)。  
  
     此操作还将删除快照作业以及该分区的任何快照文件。  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 若要更好地管理具有参数化筛选器的发布，可以通过使用复制管理对象 (RMO) 以编程方式创建新的订阅服务器分区，枚举现有的订阅服务器分区以及删除订阅服务器分区。 有关如何创建订阅服务器分区的信息，请参阅 [Create a Snapshot for a Merge Publication with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。 可以获得有关现有分区的以下信息：  
  
-   分区所基于的值和筛选函数。  
  
-   为订阅服务器生成参数化快照的作业的名称。  
  
-   参数化快照作业上次运行的时间。  
  
#### 查看有关现有分区的信息  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 类。 设置 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性的发布，并设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中创建。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 2 中的发布属性定义不正确，或者此发布不存在。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> 方法，并将结果传递给数组 <xref:Microsoft.SqlServer.Replication.MergePartition> 对象。  
  
5.  每个 <xref:Microsoft.SqlServer.Replication.MergePartition> 对象数组中，请获取感兴趣的任何属性。  
  
#### 删除现有分区  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 类。 设置 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性的发布，并设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中创建。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 2 中的发布属性定义不正确，或者此发布不存在。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> 方法，并将结果传递给数组 <xref:Microsoft.SqlServer.Replication.MergePartition> 对象。  
  
5.  每个 <xref:Microsoft.SqlServer.Replication.MergePartition> 对象数组中，请确定是否应删除该分区。 此决定通常基于的值 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A> 属性或 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A> 属性。  
  
6.  调用 <xref:Microsoft.SqlServer.Replication.MergePublication.RemoveMergePartition%2A> 方法 <xref:Microsoft.SqlServer.Replication.MergePublication> 步骤 2 中的对象。 传递 <xref:Microsoft.SqlServer.Replication.MergePartition> 步骤 5 中的对象。  
  
7.  对已删除的每个分区重复步骤 6。  
  
## 另请参阅  
 [参数化行筛选器](../../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [带有参数化筛选器的合并发布的快照](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  