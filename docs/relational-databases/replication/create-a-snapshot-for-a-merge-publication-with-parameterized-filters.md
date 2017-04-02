---
title: "为包含参数化筛选器的合并发布创建快照 | Microsoft Docs"
ms.custom: ""
ms.date: "05/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "参数化筛选器 [SQL Server 复制], 快照"
  - "快照 [SQL Server 复制], 参数化筛选器和"
  - "筛选器 [SQL Server 复制], 参数化"
ms.assetid: 00dfb229-f1de-4d33-90b0-d7c99ab52dcb
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# 为包含参数化筛选器的合并发布创建快照
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中通过参数化筛选器为合并发布创建快照。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
-   **通过参数化筛选器为合并发布创建快照，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
  
-   在使用参数化筛选器为合并发布生成快照时，必须先生成一个包含所有已发布数据和订阅的订阅服务器元数据的标准（架构）快照。 有关详细信息，请参阅 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。 创建完架构快照后，便可生成包含特定于订阅服务器的已发布数据分区的快照。  
  
-   如果发布中对一个或多个项目的筛选生成了对每个订阅具有唯一性的非重叠分区，则每当运行合并代理时都会清除元数据。 这意味着分区快照会过期得更快。 使用此选项时，应考虑允许订阅服务器启动快照的生成和传递。 有关筛选选项的详细信息，请参阅的"设置 '分区选项'"部分 [带有参数化筛选器的合并发布的快照](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 启用生成分区的快照 **数据分区** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。 可以允许订阅服务器启动快照生成及传送和/或生成快照。  
  
 生成一个或多个分区的快照之前，必须：  
  
1.  使用新建发布向导创建合并发布，并在该向导的 **“添加筛选器”** 页上指定一个或多个参数化行筛选器。 有关详细信息，请参阅 [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
2.  生成发布的架构快照。 默认情况下，架构快照在完成新建发布向导时生成；您也可以从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中生成架构快照。  
  
#### 生成架构快照  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“发布”** 文件夹。  
  
3.  右键单击您要为其创建快照，然后单击的发布 **查看快照代理状态**。  
  
4.  在 **查看快照代理状态-\< 发布>** 对话框中，单击 **启动**。  
  
     快照代理生成快照后，将显示一条消息，例如“[100%] 已生成 17 个项目的快照”。  
  
#### 允许订阅服务器启动快照的生成和传递  
  
1.  在 **数据分区** 页 **发布属性-\< 发布>** 对话框中，选择 **自动定义分区并生成快照，如果需要新的订阅服务器尝试同步时**。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### 生成和刷新快照  
  
1.  在 **数据分区** 页 **发布属性-\< 发布>** 对话框中，单击 **添加**。  
  
2.  输入一个值 **host_name （)** 和/或 **suser_sname （)** 与想要创建快照的分区相关联的值。  
  
3.  还可以指定快照刷新计划：  
  
    1.  选择 **安排此分区在以下时间运行快照代理程序**  
  
    2.  接受默认的快照刷新计划，或者单击 **“更改”** 以指定其他计划。  
  
4.  单击 **确定**, ，从而返回到 **发布属性-\< 发布>** 对话框。  
  
5.  在属性网格中选择分区，然后单击 **“立即生成所选快照”**。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 使用存储过程和快照代理，您可以执行以下操作：  
  
-   允许订阅服务器在第一次同步时请求快照生成和应用。  
  
-   为每个分区预生成快照。  
  
-   手动为每个订阅服务器生成快照。  
  
    > [!IMPORTANT]  
    >  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
#### 创建允许订阅服务器启动快照生成和传递的发布  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergepublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 指定下列参数：  
  
    -   将 **@publication**指定为发布的名称。  
  
    -   值为 **true** 为 **@allow_subscriber_initiated_snapshot**, ，这可使订阅服务器启动快照进程。  
  
    -   （可选）可并发运行的动态快照进程数 **@max_concurrent_dynamic_snapshots**。 如果正在运行的进程数达到了最大值，并且订阅服务器尝试生成快照，则该进程将被置于队列中。 默认情况下，并发进程的数量不受限制。  
  
2.  在发布服务器上，执行 [sp_addpublication_snapshot & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定在步骤 1 中使用的发布名称 **@publication** 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 在其下的 Windows 凭据 [复制快照代理](../../relational-databases/replication/agents/replication-snapshot-agent.md) 运行所使用的 **@job_login** 和 **@password**。 如果代理将使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证连接到发布服务器时，您还必须指定的值为 **0** 为 **@publisher_security_mode** 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录信息 **@publisher_login** 和 **@publisher_password**。 此操作将为发布创建一个快照代理作业。 有关生成初始快照和为快照代理定义自定义计划的详细信息，请参阅 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，为所有参数提供的值配置发布服务器时包括 *job_login* 和 *job_password*, ，发送到分发服务器上以纯文本格式。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
3.  执行 [sp_addmergearticle & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 若要添加到发布的项目。 必须对发布中的每个项目执行一次此存储过程。 当使用参数化筛选器，必须指定一个或多个项目使用的参数化的行筛选器 **@subset_filterclause** 参数。 有关详细信息，请参阅 [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
4.  如果将基于参数化的行筛选器进行筛选的其他文章，执行 [sp_addmergefilter & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 若要定义的联接或项目之间的逻辑记录关系。 必须对要定义的每个关系执行一次此存储过程。 有关详细信息，请参阅 [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
5.  当合并代理请求快照初始化订阅服务器时，将自动生成请求订阅的分区的快照。  
  
#### 创建发布并预生成或自动刷新快照  
  
1.  执行 [sp_addmergepublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 若要创建发布。 有关详细信息，请参阅 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  在发布服务器上，执行 [sp_addpublication_snapshot & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定在步骤 1 中使用的发布名称 **@publication** 和在其下的快照代理运行的 Windows 凭据 **@job_login** 和 **@password**。 如果代理将使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证连接到发布服务器时，您还必须指定的值为 **0** 为 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录信息 **@publisher_login** 和 **@publisher_password**。 此操作将为发布创建一个快照代理作业。 有关生成初始快照和为快照代理定义自定义计划的详细信息，请参阅 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，为所有参数提供的值配置发布服务器时包括 *job_login* 和 *job_password*, ，发送到分发服务器上以纯文本格式。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
3.  执行 [sp_addmergearticle & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 若要添加到发布的项目。 必须对发布中的每个项目执行一次此存储过程。 当使用参数化筛选器，必须指定一个项目使用的参数化的行筛选器 **@subset_filterclause** 参数。 有关详细信息，请参阅 [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
4.  如果将基于参数化的行筛选器进行筛选的其他文章，执行 [sp_addmergefilter & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 若要定义的联接或项目之间的逻辑记录关系。 必须对要定义的每个关系执行一次此存储过程。 有关详细信息，请参阅 [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
5.  在发布服务器上对发布数据库中，执行 [sp_helpmergepublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), ，指定的值的 **@publication** 步骤 1 中。 记下的值 **snapshot_jobid** 结果集中。  
  
6.  值转换 **snapshot_jobid** 在步骤 5 中获得 **uniqueidentifier**。  
  
7.  在发布服务器 **msdb** 数据库，执行 [sp_start_job & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md), ，指定转换后的值的第 6 步中获得 **@job_id**。  
  
8.  在发布服务器上对发布数据库中，执行 [sp_addmergepartition & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)。 指定步骤 1 中发布的名称 **@publication** 和值用来定义分区的 **@suser_sname** 如果 [SUSER_SNAME & #40;Transact SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md) 用于筛选子句中或用于 **@host_name** 如果 [HOST_NAME & #40;Transact SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) 筛选器子句中使用。  
  
9. 在发布服务器上对发布数据库中，执行 [sp_adddynamicsnapshot_job & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)。 指定步骤 1 中发布的名称 **@publication**, ，值 **@suser_sname** 或 **@host_name** 从步骤 8 和作业的计划。 此操作将创建为指定分区生成参数化快照的作业。 有关详细信息，请参阅 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)。  
  
    > [!NOTE]  
    >  使用在步骤 2 中定义的初始快照作业的 Windows 帐户运行此作业。 若要删除参数化的快照作业及其相关的数据分区，请执行 [sp_dropdynamicsnapshot_job & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)。  
  
10. 在发布服务器上对发布数据库中，执行 [sp_helpmergepartition & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md), ，指定的值的 **@publication** 从步骤 1 和的值 **@suser_sname** 或 **@host_name** 来自步骤 8。 记下的值 **dynamic_snapshot_jobid** 结果集中。  
  
11. 在分发服务器 **msdb** 数据库，执行 [sp_start_job & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md), ，指定在步骤 9 中获得的值 **@job_id**。 此操作将启动分区的参数化快照作业。  
  
12. 重复步骤 8-11，分别为每个订阅生成一个分区快照。  
  
#### 创建发布并为每个分区手动创建快照  
  
1.  执行 [sp_addmergepublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 若要创建发布。 有关详细信息，请参阅 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  在发布服务器上，执行 [sp_addpublication_snapshot & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定在步骤 1 中使用的发布名称 **@publication** 和在其下的快照代理运行的 Windows 凭据 **@job_login** 和 **@password**。 如果代理将使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证连接到发布服务器时，您还必须指定的值为 **0** 为 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录信息 **@publisher_login** 和 **@publisher_password**。 此操作将为发布创建一个快照代理作业。 有关生成初始快照和为快照代理定义自定义计划的详细信息，请参阅 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，为所有参数提供的值配置发布服务器时包括 *job_login* 和 *job_password*, ，发送到分发服务器上以纯文本格式。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
3.  执行 [sp_addmergearticle & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 若要添加到发布的项目。 必须对发布中的每个项目执行一次此存储过程。 当使用参数化筛选器，必须指定至少一个项目使用的参数化的行筛选器 **@subset_filterclause** 参数。 有关详细信息，请参阅 [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
4.  如果将基于参数化的行筛选器进行筛选的其他文章，执行 [sp_addmergefilter & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 若要定义的联接或项目之间的逻辑记录关系。 必须对要定义的每个关系执行一次此存储过程。 有关详细信息，请参阅 [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
5.  启动快照作业或从命令提示符下运行复制快照代理，以生成标准快照架构及其他文件。 有关详细信息，请参阅 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
6.  从命令提示符，以生成大容量复制 (.bcp) 文件，指定的分区快照的位置重新运行复制快照代理 **-DynamicSnapshotLocation** 和一个或两个用于定义分区的以下属性︰  
  
    -   **-DynamicFilterHostName** -值如果 [HOST_NAME & #40;Transact SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) 可使用。  
  
    -   **-DynamicFilterLogin** -值如果 [SUSER_SNAME & #40;Transact SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md) 可使用。  
  
7.  重复步骤 6，分别为每个订阅生成一个分区快照。  
  
8.  对每个订阅运行合并代理以在订阅服务器上应用初始分区快照，并指定以下属性：  
  
    -   **-Hostname** -用于定义分区，如果要覆盖 HOST_NAME 的实际值的值。  
  
    -   **-DynamicSnapshotLocation** -此分区的动态快照的位置。  
  
> [!NOTE]  
>  有关复制代理编程的详细信息，请参阅 [复制代理可执行文件概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此示例使用参数化筛选器创建合并发布，其中由订阅服务器启动快照生成过程。 值为 **@job_login** 和 **@job_password** 传递中使用脚本变量。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_1.sql)]  
  
 此示例创建一个发布使用参数化筛选器，其中每个订阅服务器具有其分区通过执行已定义 [sp_addmergepartition](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md) 和筛选的快照作业通过执行创建 [sp_adddynamicsnapshot_job](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md) 传入的分区信息。 值为 **@job_login** 和 **@job_password** 传递中使用脚本变量。  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_2.sql)]  
  
 此示例使用参数化筛选器创建发布，其中每个订阅服务器都必须通过提供分区信息来创建它自己的数据分区和已筛选的快照作业。 手动运行复制代理时，订阅服务器使用命令行参数提供分区信息。 此示例假设还对发布创建了订阅。  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPartitionManual](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_3.sql)]  
  
```  
  
REM Line breaks are added to improve readability.   
REM In a batch file, commands must be made in a single line.  
REM Run the Snapshot agent from the command line to generate the standard snapshot   
REM schema and other files.   
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub% -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  
  
PAUSE  
  
```  
  
```  
  
REM Run the Snapshot agent from the command line, this time to generate   
REM the bulk copy (.bcp) data for each Subscriber partition.    
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
MD %SnapshotDir%  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub%  -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  -DynamicFilterHostName "adventure-works\Fernando"    
-DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
```  
  
REM Run the Merge Agent for each subscription to apply the partitioned   
REM snapshot for each Subscriber.    
SET Publisher = %computername%  
SET Subscriber = %computername%  
SET PubDB = AdventureWorks2012   
SET SubDB = AdventureWorks2012Replica   
SET PubName = AdvWorksSalesPersonMerge   
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE" -Publisher  %Publisher%    
-Subscriber  %Subscriber%  -Distributor %Publisher%  -PublisherDB %PubDB%    
-SubscriberDB %SubDB% -Publication %PubName%  -PublisherSecurityMode 1  -OutputVerboseLevel 3    
-Output -SubscriberSecurityMode 1  -SubscriptionType 3 -DistributorSecurityMode 1    
-Hostname "adventure-works\Fernando"  -DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以使用复制管理对象 (RMO) 通过以下方法以编程的方式生成分区快照：  
  
-   允许订阅服务器在第一次同步时请求快照生成和应用。  
  
-   为每个分区预生成快照。  
  
-   通过运行快照代理为每台订阅服务器手动生成一个快照。  
  
> [!NOTE]  
>  在筛选时的一篇文章生成对都是唯一的每个订阅 （通过指定的 P:Microsoft.SqlServer.Replication.MergeArticle.PartitionOption F:Microsoft.SqlServer.Replication.PartitionOptions.NonOverlappingSingleSubscription 的值，在创建合并项目时） 的非重叠分区，将清除元数据只要运行合并代理。 这意味着分区快照会过期得更快。 使用此选项时，应考虑允许订阅服务器请求快照生成。 有关详细信息，请参阅主题 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md)中的“使用适当的筛选选项”部分。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须存储凭据，请使用 [Windows .NET Framework 提供的](http://go.microsoft.com/fwlink/?LinkId=34733) Cryptographic Services [!INCLUDE[msCoName](../../includes/msconame-md.md)] （加密服务）。  
  
#### 创建允许订阅服务器启动快照生成和传递的发布  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 类为发布数据库中，设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为实例 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 从步骤 1，并调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 返回 **false**, ，确认数据库是否存在。  
  
3.  如果 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 属性是 **false**, ，将其设置为 **true** 并调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>。  
  
4.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 类，并将设置此对象的下列属性︰  
  
    -    <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   已发布的数据库的名称 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>。  
  
    -   有关发布的名称 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>。  
  
    -   要为运行的动态快照作业的最大数 <xref:Microsoft.SqlServer.Replication.MergePublication.MaxConcurrentDynamicSnapshots%2A>。 因为订阅服务器启动的快照请求随时都可以发生，所以在多个订阅服务器同时请求其分区快照时，此属性会限制可以同时运行的快照代理作业的数目。 运行的作业达到最大数目时，其他分区快照请求会进行排队，直到其前面的一个作业运行完才开始运行。  
  
    -   使用按位逻辑 OR (**|** 在 Visual C# 和 **或者** 在 Visual Basic 中) 来添加的值的运算符 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowSubscriberInitiatedSnapshot> 到 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>。  
  
    -    <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 字段 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 提供的凭据 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户下运行快照代理作业。  
  
        > [!NOTE]  
        >  设置 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 的成员创建发布时，建议使用 **sysadmin** 固定的服务器角色。 有关详细信息，请参阅 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法以创建发布。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，提供的所有属性的值配置发布服务器时包括 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, ，发送到分发服务器上以纯文本格式。 您还应该加密在发布服务器和它之前调用的远程分发服务器之间的连接 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
6.  使用 <xref:Microsoft.SqlServer.Replication.MergeArticle> 属性将项目添加到发布。 指定 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 至少一个项目定义参数化筛选器属性。 （可选）创建 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 定义的对象联接项目之间的筛选器。 有关详细信息，请参阅 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
7.  如果值 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 是 **false**, ，调用 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 若要创建此发布的初始快照代理作业。  
  
8.  调用 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 方法 <xref:Microsoft.SqlServer.Replication.MergePublication> 步骤 4 中创建的对象。 这将启动生成初始快照的代理作业。 有关生成初始快照和为快照代理定义自定义计划的详细信息，请参阅 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
9. （可选）检查值是否为 **true** 为 <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 属性以确定初始快照何时可供使用。  
  
10. 如果订阅服务器的合并代理是第一次连接，则会自动生成一个分区快照。  
  
#### 创建发布并预生成快照或自动刷新快照  
  
1.  使用的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 类来定义合并发布。 有关详细信息，请参阅 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  使用 <xref:Microsoft.SqlServer.Replication.MergeArticle> 属性将项目添加到发布。 指定 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 属性对于至少一个项目定义参数化筛选器，然后创建任何 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 定义的对象联接项目之间的筛选器。 有关详细信息，请参阅 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
3.  如果值 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 是 **false**, ，调用 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 若要创建此发布的快照代理作业。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 方法 <xref:Microsoft.SqlServer.Replication.MergePublication> 步骤 1 中创建的对象。 此方法启动生成初始快照的代理作业。 有关生成初始快照和为快照代理定义自定义计划的详细信息，请参阅 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
5.  检查值是否为 **true** 为 <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 属性以确定初始快照何时可供使用。  
  
6.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePartition> 类，并将参数化筛选条件设置为订阅服务器，使用一种或两个以下属性︰  
  
    -   如果订阅服务器的分区定义的结果 [SUSER_SNAME & #40;Transact SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md), ，使用 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A>。  
  
    -   如果订阅服务器的分区定义的结果 [HOST_NAME & #40;Transact SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) 或函数，请使用此重载 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A>。  
  
7.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 类，并设置相同的属性，如下所示的第 6 步。  
  
8.  使用 <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> 类可定义用于生成订阅服务器分区的筛选的快照的计划。  
  
9. 使用的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 从步骤 1 中，调用 <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergePartition%2A>。 传递 <xref:Microsoft.SqlServer.Replication.MergePartition> 步骤 6 中的对象。  
  
10. 使用的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 从步骤 1 中，调用 <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergeDynamicSnapshotJob%2A> 方法。 传递 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 步骤 7 中的对象和 <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> 步骤 8 中的对象。  
  
11. 调用 <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergeDynamicSnapshotJobs%2A>, ，并找到 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 返回数组中的新添加的分区的快照作业的对象。  
  
12. 获取 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob.Name%2A> 作业的属性。  
  
13. 通过使用创建连接到分发服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
14. 创建实例的 SQL Server 管理对象 (SMO) <xref:Microsoft.SqlServer.Management.Smo.Server> 类，并传入 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 13 中的对象。  
  
15. 创建的实例 <xref:Microsoft.SqlServer.Management.Smo.Agent.Job> 类，并传入 <xref:Microsoft.SqlServer.Management.Smo.Server.JobServer%2A> 属性 <xref:Microsoft.SqlServer.Management.Smo.Server> 从第 14 步和第 12 步中的作业名称的对象。  
  
16. 调用 <xref:Microsoft.SqlServer.Management.Smo.Agent.Job.Start%2A> 方法以启动分区的快照作业。  
  
17. 为每个订阅服务器重复步骤 6-16。  
  
#### 创建发布并为每个分区手动创建快照  
  
1.  使用的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 类来定义合并发布。 有关详细信息，请参阅 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  使用 <xref:Microsoft.SqlServer.Replication.MergeArticle> 属性将项目添加到发布指定 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 属性对于至少一个项目定义参数化筛选器，然后创建任何 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 定义的对象联接项目之间的筛选器。 有关详细信息，请参阅 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
3.  生成初始快照。 有关详细信息，请参阅 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
4.  创建 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 类的实例，并设置下列所需属性：  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> -发布服务器的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> -发布数据库的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> -发布的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> -分发服务器的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> -值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 到使用的 Windows 集成身份验证或值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 使用 SQL Server 身份验证。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> -值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 到使用的 Windows 集成身份验证或值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 使用 SQL Server 身份验证。  
  
5.  将值设为 <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> 为 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>。  
  
6.  设置一个或多个下列属性以定义分区参数：  
  
    -   如果订阅服务器的分区定义的结果 [SUSER_SNAME & #40;Transact SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md), ，使用 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterLogin%2A>。  
  
    -   如果订阅服务器的分区定义的结果 [HOST_NAME & #40;Transact SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) 或函数，请使用此重载 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterHostName%2A>。  
  
7.  调用 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 方法。  
  
8.  为每个订阅服务器重复步骤 4-7。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 此示例创建一个允许订阅服务器请求快照生成的合并发布。  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
 此示例为带有参数化行筛选器的合并发布手动创建订阅服务器分区和筛选快照。  
  
 [!code-csharp[HowTo#rmo_CreateMergePartition](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepartition)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePartition](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepartition)]  
  
 此示例手动启动快照代理，为带有参数化行筛选器的合并发布的订阅服务器生成筛选数据快照。  
  
 [!code-csharp[HowTo#rmo_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatefilteredsnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatefilteredsnapshot)]  
  
## 另请参阅  
 [参数化行筛选器](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [复制系统存储过程概念](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [带有参数化筛选器的合并发布的快照](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)   
 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  