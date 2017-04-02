---
title: "复制管理员常见问题 | Microsoft Docs"
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
  - "管理复制, 常见问题解答"
  - "复制 [SQL Server], 管理"
ms.assetid: 5a9e4ddf-3cb1-4baf-94d6-b80acca24f64
caps.latest.revision: 59
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 59
---
# 复制管理员常见问题
  下列问题和解答就复制数据库管理员所面临的多种任务提供指导。  
  
## 配置复制  
  
### 活动在发布时是否需要在数据库上停止？  
 否。 创建发布时，活动仍可在数据库上继续进行。 注意，生成快照可能占用大量资源，因此最好在数据库活动较少的期间生成快照（默认情况下完成新建发布向导后就生成快照）。  
  
### 快照生成期间是否锁定表？  
 锁定的时间长度取决于所用复制的类型：  
  
-   对于合并发布，快照代理不使用任何锁。  
  
-   对于事务发布，默认情况下快照代理只在快照生成的初始阶段进行锁定。  
  
-   对于快照发布，快照代理在快照生成的整个过程中都进行锁定。  
  
 由于锁会阻止其他用户更新表，所以应把快照代理安排在数据库活动较少的期间执行，对快照发布尤其如此。  
  
### 订阅何时可用？何时可以使用订阅数据库？  
 将快照应用于订阅数据库之后，即可使用订阅。 即使订阅数据库在此之前就可以访问，但在应用快照之前，不应使用数据库。 使用复制监视器检查快照生成和应用的状态：  
  
-   快照由快照代理生成。 请在复制监视器中某个发布的 **“代理”** 选项卡中查看快照生成的状态。 有关详细信息，请参阅 [查看信息并执行任务的代理相关联的发布 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)。  
  
-   快照由分发代理或合并代理应用。 请在复制监视器的 **“分发代理”** 页或 **“合并代理”** 页中查看快照应用的状态。 有关详细信息，请参阅 [查看信息并执行任务的代理与订阅相关 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
### 如果分发代理或合并代理启动时快照代理尚未完成，会出现什么情况？  
 如果分发代理或合并代理和快照代理同时运行，不会引发错误。 但是，必须注意下列事项：  
  
-   如果将分发代理或合并代理配置为连续运行，则该代理将在快照代理完成之后自动应用快照。  
  
-   如果将分发代理或合并代理配置为按计划运行或按需运行，而且在代理运行时不存在可用的快照，则代理将关闭，并显示一条快照尚不可用的消息。 快照代理完成后，必须再次运行代理以应用快照。 有关运行代理的详细信息，请参阅 [同步推送订阅](../../../relational-databases/replication/synchronize-a-push-subscription.md), ，[同步请求订阅](../../../relational-databases/replication/synchronize-a-pull-subscription.md), ，和 [复制代理可执行文件概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
### 是否应为复制配置编写脚本？  
 是。 为复制配置编写脚本是任何复制拓扑的灾难恢复计划的关键。 有关编写脚本的详细信息，请参阅 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)。  
  
### 复制数据库需要什么样的恢复模式？  
 复制使用以下任何恢复模式都可正常运行：简单恢复模式、大容量日志恢复模式或完整恢复模式。 合并复制以在元数据表中存储信息的方式跟踪更改。 事务复制通过标记事务日志来跟踪更改，但此标记过程不受恢复模式影响。  
  
### 复制为什么要向已复制的表添加一列；如果表并未发布，是否会删除该列？  
 若要跟踪更改，带有排队更新订阅的合并复制和事务复制必须能够唯一地标识每个已发布表中的每一行。 为实现这一点：  
  
-   合并复制将列添加 **rowguid** 向每个表，除非表中已有的数据类型列 **uniqueidentifier** 与 **ROWGUIDCOL** 属性设置 （在这种情况下使用此列）。 如果从发布中删除表，则删除 **rowguid** 列；如果将现有列用于跟踪，则不删除该列。  
  
-   如果事务发布支持排队更新订阅，复制将列添加 **msrepl_tran_version** 向每个表。 如果从发布中，在删除表 **msrepl_tran_version** 不删除该列。  
  
-   筛选器不能包含复制所用的 **rowguidcol** 来标识行。 默认情况下，这是您设置合并复制时添加的列，命名为 **rowguid**。  
  
### 如何管理已发布表的约束？  
 关于已发布表的约束，有几个问题需要考虑：  
  
-   事务复制要求每个已发布表都有主键约束。 合并复制不需要主键，但如果存在一个主键，则必须复制该主键。 快照复制不需要主键。  
  
-   默认情况下，主键约束、索引和检查约束都会复制到订阅服务器。  
  
-   默认情况下为外键约束和检查约束指定 NOT FOR REPLICATION 选项；约束对用户操作强制使用，但不对代理操作强制使用。  
  
 有关设置控制是否复制约束的架构选项的信息，请参阅 [Specify Schema Options](../../../relational-databases/replication/publish/specify-schema-options.md)。  
  
### 如何管理标识列？  
 复制在订阅服务器中为包含更新的复制拓扑提供自动标识范围管理。 有关详细信息，请参阅 [复制标识列](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
### 是否可以在不同的发布中发布相同的对象？  
 是，但有一些限制。 有关详细信息，请参阅主题中的"发布表中多个发布"一节 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
### 多个发布是否可以使用同一个分发数据库？  
 是。 对于可以使用同一分发数据库的发布的数量或类型没有任何限制。 来自给定发布服务器的所有发布都必须使用同一分发服务器和分发数据库。  
  
 如果有多个发布，则可以在分发服务器上配置多个分发数据库，以确保通过每个分发数据库的数据流都来自单个发布。 使用 **分发服务器属性** 对话框或 [sp_adddistributiondb & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) 若要添加分发数据库。 有关访问此对话框的详细信息，请参阅 [查看和修改分发服务器和发布服务器属性](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
### 如何在分发服务器和发布服务器中查找信息，如已经发布了数据库中的哪些对象？  
 此信息可通过 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]和许多复制存储过程获得。 有关详细信息，请参阅 [Distributor and Publisher Information Script](../../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)。  
  
### 复制是否加密数据？  
 否。 复制不对数据库中存储的数据或网络上传输的数据加密。 有关详细信息，请参阅主题的"加密"部分 [安全概述 & #40;复制和 #41;](../../../relational-databases/replication/security/security-overview-replication.md)。  
  
### 如何在 Internet 上复制数据？  
 使用以下方式在 Internet 上复制数据：  
  
-   虚拟专用网络 (VPN)。 有关详细信息，请参阅 [发布数据通过 Internet 使用 VPN](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md)。  
  
-   对于合并复制，使用 Web 同步选项。 有关详细信息，请参阅 [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)。  
  
 所有类型的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 复制都可以通过 VPN 来复制数据。但如果使用的是合并复制，应考虑使用 Web 同步。  
  
### 如果删除连接，复制是否可以继续？  
 是。 如果删除连接，复制处理可从停止处继续。 如果在不可靠的网络上使用合并复制，则请考虑使用逻辑记录，这可确保把相关更改作为一个单元来处理。 有关详细信息，请参阅 [通过逻辑记录对相关行组更改](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
### 复制是否可以在低带宽连接上工作？ 它是否使用压缩？  
 是，复制的确可以在低带宽连接上工作。 对于通过 TCP/IP 的连接，复制使用该协议提供的压缩，但不提供其他压缩。 对于通过 HTTPS 的 Web 同步连接，复制使用协议提供的压缩，也使用复制更改所用的 XML 文件的其他压缩。  
  
## 登录名和对象所有权  
  
### 是否复制登录名和密码？  
 否。 可以创建 DTS 包，把登录名和密码从发布服务器传输到一个或多个订阅服务器。  
  
### 什么是架构，如何复制架构？  
 从 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)],  有两种含义：  
  
-   对象的定义，如 CREATE TABLE 语句。 默认情况下，复制把所有已复制对象的定义都复制到订阅服务器。  
  
-   在其中创建对象的命名空间︰ \< 数据库>。 \< 架构>。 \< 对象>。 架构使用 CREATE SCHEMA 语句定义。  
  
-   在新建发布向导中，复制在架构和对象所有权方面具有以下默认行为：  
  
-   对于兼容性级别为 90 或更高的合并发布、快照发布和事务发布中的项目：默认情况下，订阅服务器中的对象所有者与发布服务器中相应对象的所有者相同。 如果订阅服务器中不存在拥有对象的架构，将自动创建这些架构。  
  
-   对于合并发布中兼容级别低于 90 的项目：默认情况下，所有者保留为空，并且在订阅服务器上创建对象的过程中指定为 **dbo** 。  
  
-   对于 Oracle 发布中的项目：默认情况下，所有者指定为 **dbo**。  
  
-   对于使用字符模式快照（用于非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器以及 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 订阅服务器）的发布中的项目：默认情况下，所有者保留为空。 所有者默认为与分发代理或合并代理连接到订阅服务器所使用的帐户关联的所有者。  
  
 可以通过更改对象所有者 **项目属性-\<***文章***>** 对话框和以下存储过程︰ **sp_addarticle**, ，**sp_addmergearticle**, ，**sp_changearticle**, ，和 **sp_changemergearticle**。 有关详细信息，请参阅 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), ，[定义项目](../../../relational-databases/replication/publish/define-an-article.md), ，和 [查看和修改项目属性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)。  
  
### 如何配置订阅数据库上的授权，以使其与发布数据库上的授权相匹配？  
 默认情况下，复制不在订阅数据库上执行 GRANT 语句。 如果希望订阅数据库上的权限与发布数据库上的权限相匹配，请使用下列方法之一：  
  
-   直接在订阅数据库上执行 GRANT 语句。  
  
-   使用快照后脚本来执行这些语句。 有关详细信息，请参阅 [执行脚本之前和之后应用快照](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。  
  
-   使用存储的过程 [sp_addscriptexec](../../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md) 以执行语句。  
  
### 如果重新初始化订阅，订阅数据库中授予的权限会怎样？  
 默认情况下，重新初始化订阅时会删除并重新创建订阅服务器中的对象，这将导致删除已授予这些对象的所有权限。 有两种方法可以处理此种情况：  
  
-   重新初始化后，使用前一部分介绍的技术重新应用授权。  
  
-   指定重新初始化订阅时不应删除对象。 重新初始化之前，进行以下两项操作之一：  
  
    -   执行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 或 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 将值指定为 'pre_creation_cmd' (**sp_changearticle**) 或 pre_creation_command (**sp_changemergearticle**) 参数 **@property** 和的值为 'none'、 'delete' 或 'truncate' 参数 **@value**。  
  
    -   在 **项目属性-\< 项目>** 对话框中的 **目标对象** 部分中，选择的值为 **保留现有对象保持不变**, ，**删除数据。如果项目有行筛选器中，删除与筛选器匹配的数据。** 或 **截断现有对象中的所有数据** 选项 **名称正在使用中时的操作**。 有关访问此对话框的详细信息，请参阅 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
## 数据库维护  
  
### 为什么无法对已发布的表运行 TRUNCATE TABLE？  
 TRUNCATE TABLE 是不会激发触发器的日志未记录的操作。 之所以不允许对已发布的表运行 TRUNCATE TABLE，是因为复制无法跟踪此操作导致的更改：事务复制通过事务日志来跟踪更改；合并复制通过已发布表的触发器来跟踪更改。  
  
### 在复制的数据库上运行大容量插入命令，会产生什么效果？  
 对于事务复制，大容量插入命令跟踪和复制的方式和其他插入命令相同。 对于合并复制，则必须确保正确更新跟踪元数据的更改。  
  
### 对于备份和还原，是否存在复制注意事项？  
 是。 对于复制所涉及数据库有许多特别注意事项。 有关详细信息，请参阅 [备份和还原复制数据库](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)。  
  
### 复制是否影响事务日志的大小？  
 合并复制和快照复制不影响事务日志的大小，但事务复制会影响。 如果数据库包括一个或多个事务发布，则只有将与这些发布有关的所有事务传递到分发数据库之后才会截断日志。 如果事务日志增长得过大，而且日志读取器代理按计划运行，请考虑缩短运行间隔。 或者，将日志读取器代理设置为以连续模式运行。 如果将其设置为以连续模式运行（默认值），请确保它正在运行。 检查日志读取器代理状态的详细信息，请参阅 [查看信息并执行任务的代理相关联的发布 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)。  
  
 此外，如果在发布数据库或分发数据库中设置了选项“sync with backup”，则直到备份了所有事务后，才会截断事务日志。 如果事务日志增长过大，而且已设置了此选项，请考虑缩短事务日志备份间的间隔。 有关备份和还原事务复制中涉及的数据库的详细信息，请参阅 [用于备份和还原快照与事务复制的策略](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
### 如何在复制的数据库中重新生成索引或表？  
 有许多用于重新生成索引的机制。 这些机制都可以使用，且对于复制并没有特别的注意事项，但下述情况例外：事务发布中的表必须具有主键，因此无法删除并重新创建这些表的主键。  
  
### 如何在发布数据库和订阅数据库上添加或更改索引？  
 可以在发布服务器或订阅服务器中添加索引，并且没有针对复制的特别注意事项（注意，索引可以影响性能）。 不会复制 CREATE INDEX 和 ALTER INDEX，因此如果要添加或更改比如发布服务器中的索引，则必须也在订阅服务器中进行相同的添加或更改（如果想要其反映在订阅服务器中）。  
  
### 如何对复制所涉及的数据库的文件进行移动和重命名？  
 在早于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本中，移动或重命名数据库文件需要分离并重新附加数据库。 因为无法分离复制的数据库，所以必须首先从这些数据库中删除复制。 从 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 开始，无需分离并重新附加数据库便可移动或重命名文件，且不会影响复制。 有关移动和重命名文件的详细信息，请参阅 [ALTER DATABASE & #40;Transact SQL & #41;](../../../t-sql/statements/alter-database-transact-sql.md)。  
  
### 如何删除正在复制的表？  
 先从发布使用删除文章 [sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md), ，[sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md), ，或 **发布属性-\< 发布>** 对话框框中，并将它放在数据库使用 `DROP <Object>`。 在添加订阅后，就不能从快照发布或事务发布中删除项目，而必须先删除订阅。 有关详细信息，请参阅 [添加项目和删除现有发布的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
### 如何在已发布的表中添加或删除列？  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持对已发布对象进行各种架构更改，包括添加和删除列。 例如，执行 ALTER TABLE... 在发布服务器上执行 DROP COLUMN，该语句将复制到订阅服务器，然后执行以删除列。 运行的版本的订阅服务器 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 支持添加和删除列通过存储过程 [sp_repladdcolumn](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) 和 [sp_repldropcolumn](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md)。 有关详细信息，请参阅 [发布数据库上进行架构更改](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
## 复制维护  
  
### 如何确定订阅服务器的数据是否与发布服务器的数据同步？  
 使用验证。 验证报告给定订阅服务器是否与发布服务器同步。 有关详细信息，请参阅 [验证已复制数据](../../../relational-databases/replication/validate-replicated-data.md)。 验证不会提供与某些行是否未正确同步有关的信息，而 [tablediff 实用工具](../../../tools/tablediff-utility.md) 可以提供此信息。  
  
### 如何向现有发布添加表？  
 不必为了添加表（或另一个对象）而停止发布数据库或订阅数据库上的活动。 将表添加到通过发布 **发布属性-\< 发布>** 对话框或存储的过程 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 和 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 有关详细信息，请参阅 [添加项目和删除现有发布的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
### 如何从发布中删除表？  
 从发布使用中移除表 [sp_droparticle](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md), ，[sp_dropmergearticle](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md), ，或 **发布属性-\< 发布>** 对话框。 在添加订阅后，就不能从快照发布或事务发布中删除项目，而必须先删除订阅。 有关详细信息，请参阅 [添加项目和删除现有发布的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
### 哪些操作需要重新初始化订阅？  
 许多项目和发布更改都需要重新初始化订阅。 有关详细信息，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
### 什么操作会导致快照失效？  
 许多项目和发布更改都可使快照无效，并需要生成新快照。 有关详细信息，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
### 如何删除复制？  
 从数据库删除复制所需的操作取决于数据库是作为发布数据库、订阅数据库使用，还是同时作为这两种数据库使用。  
  
### 如何确定是否存在要复制的事务或行？  
 对于事务复制，请使用存储过程或复制监视器中的 **“未分发的命令”** 选项卡。 有关详细信息，请参阅 [视图复制命令和在分发数据库 & #40; 中的其他信息复制 TRANSACT-SQL 编程 & #41;](../../../relational-databases/replication/monitor/view replicated commands and information in distribution database.md) 和 [查看信息并执行与订阅 & #40; 关联的代理任务复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
 对于合并复制，使用存储的过程 **sp_showpendingchanges**。 有关详细信息，请参阅 [sp_showpendingchanges & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)。  
  
### 分发代理滞后多少？ 是否应重新初始化？  
 使用 **sp_replmonitorsubscriptionpendingcmds** 存储过程或 **未分发的命令** 在复制监视器中的选项卡。 存储过程和选项卡显示：  
  
-   在分发数据库中尚未传递到所选订阅服务器的命令数。 一个命令由一个 Transact-SQL 数据操作语言 (DML) 语句或一个数据定义语言 (DDL) 语句组成。  
  
-   将命令传递到订阅服务器所需的估计时间。 如果此值大于生成快照并将其应用于订阅服务器所需的时间，请考虑重新初始化订阅服务器。 有关详细信息，请参阅 [重新初始化订阅](../../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
 有关详细信息，请参阅 [sp_replmonitorsubscriptionpendingcmds & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md) 和 [查看信息并执行与订阅 & #40; 关联的代理任务复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
## 复制和其他数据库功能  
  
### 复制是否可与日志传送和数据库镜像一起进行？  
 是。 有关详细信息，请参阅 [日志传送以及复制和 #40;SQL Server 和 #41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md) 和 [数据库镜像和复制 & #40;SQL Server 和 #41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)。  
  
### 复制是否可与聚类分析一起进行？  
 是。 没有需要特别注意的事项，因为所有数据都存储在群集上的一组磁盘中。  
  
## 另请参阅  
 [管理和 #40;复制和 #41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [复制管理最佳实践](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  