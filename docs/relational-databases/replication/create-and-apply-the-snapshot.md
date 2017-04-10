---
title: "创建并应用快照 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "快照 [SQL Server 复制], 应用"
  - "快照 [SQL Server 复制], 创建"
ms.assetid: 631f48bf-50c9-4015-b9d8-8f1ad92d1ee2
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 创建并应用快照
  快照由快照代理在创建发布后生成。 按以下方式生成：  
  
-   立即。 默认情况下，在新建发布向导中创建合并发布后会立即生成此发布的快照。  
  
-   在计划时间。 在指定的计划 **快照代理程序** 页新建发布向导或使用存储过程或复制管理对象 (RMO)。  
  
-   手动。 从命令提示或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]运行快照代理。 有关运行代理的详细信息，请参阅 [复制代理可执行文件概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) 和 [启动和停止复制代理 & #40;SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
 对于合并复制，每当运行快照代理时都会生成快照。 对于事务复制，在生成快照取决于发布属性设置 **immediate_sync**。 如果该属性设置为 TRUE（使用新建发布向导时的默认设置），则每当运行快照代理时都会生成快照，而且可以随时将其应用到订阅服务器。 如果该属性设置为 FALSE (默认值时使用 **sp_addpublication**)，仅当自上次快照代理运行; 以来已添加新的订阅生成快照订阅服务器必须等待快照代理程序完成才能实现同步。  
  
 默认情况下，快照生成后，它们将保存在位于分发服务器上的默认快照文件夹中。 还可以将快照文件保存在可移动介质（例如可移动磁盘、CD-ROM）上，或者保存在默认快照文件夹以外的位置。 另外，可以压缩文件，以便它们更容易存储和传输以及在订阅服务器上应用快照前后执行脚本。 有关这些选项的详细信息，请参阅 [Snapshot Options](../../relational-databases/replication/snapshot-options.md)。  
  
 如果快照用于使用参数化筛选器的合并发布，则创建快照的过程包括两部分。 首先创建包含复制脚本和已发布对象的架构（但不包含数据）的架构快照。 然后，使用包括脚本、从架构快照复制的架构以及属于订阅分区的数据的快照初始化每个订阅。 有关详细信息，请参阅 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
 在发布服务器上创建快照并将其存储在默认位置或其他快照位置后，可以将快照传输到订阅服务器并应用。 分发代理（用于快照复制或事务复制）或合并代理（用于合并复制）在初始同步期间将快照传输到订阅服务器上的订阅数据库中并将架构和数据文件应用到此数据库。 默认情况下，如果使用新建订阅向导，在创建订阅后会立即发生初始同步。 此行为由该向导的 **“初始化订阅”** 页面上的 **“初始化时间”** 选项控制。 当初始化订阅后生成快照时，除非订阅标记为重新初始化，否则快照不会应用到订阅服务器。 有关详细信息，请参阅 [重新初始化订阅](../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
 在分发代理或合并代理应用初始快照后，该代理将传播后续更新和其他数据修改。 在向订阅服务器分发并应用快照时，只有那些正在等待初始快照或新建快照的订阅服务器会受到影响。 该发布的其他订阅服务器（即那些已经收到对已发布数据的插入、更新、删除或其他修改内容的订阅服务器）不受影响。  
  
 若要创建并应用初始快照，请参阅 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
 若要查看或修改默认快照文件夹位置，请参阅  
  
-   [!包括 [ssManStudioFull] (.../ Token/ssManStudioFull_md.md)]: [Specify the Default Snapshot Location &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)  
  
-   复制编程和 RMO 编程： [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
## 另请参阅  
 [使用快照初始化订阅](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [保护快照文件夹的安全](../../relational-databases/replication/security/secure-the-snapshot-folder.md)   
 [sp_addpublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)  
  
  