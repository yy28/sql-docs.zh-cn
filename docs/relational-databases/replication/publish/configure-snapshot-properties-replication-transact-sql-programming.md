---
title: "配置快照属性（复制 Transact-SQL 编程） | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "快照 [SQL Server 复制], 属性"
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 配置快照属性（复制 Transact-SQL 编程）
  可以使用复制存储过程以编程方式定义和修改快照属性，使用的存储过程取决于发布的类型。  
  
### 在创建快照发布或事务发布时配置快照属性  
  
1.  在发布服务器上，执行 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。 指定的发布名称 **@publication**, ，其中任何一个值 **快照** 或 **连续** 为 **@repl_freq**, ，和一个或多个下列与快照相关的参数︰  
  
    -   **@alt_snapshot_folder** -如果从该位置，而不是发送或同时快照默认文件夹访问此发布的快照，则指定的路径。  
  
    -   **@compress_snapshot** -将值指定为 **true** 如果以压缩备用快照文件夹中的快照文件 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] CAB 文件格式。  
  
    -   **@pre_snapshot_script** -指定文件名和完整路径 **.sql** 将执行在订阅服务器在初始化期间应用初始快照之前的文件。  
  
    -   **@post_snapshot_script** -指定文件名和完整路径 **.sql** 之后将执行在订阅服务器在初始化期间应用初始快照的文件。  
  
    -   **@snapshot_in_defaultfolder** -将值指定为 **false** 如果快照仅在非默认位置可用。  
  
     有关创建发布的详细信息，请参阅 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
### 创建合并发布时配置快照属性  
  
1.  在发布服务器上，执行 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 指定的发布名称 **@publication**, ，其中任何一个值 **快照** 或 **连续** 为 **@repl_freq**, ，和一个或多个下列与快照相关的参数︰  
  
    -   **@alt_snapshot_folder** -如果从该位置，而不是发送或同时快照默认文件夹访问此发布的快照，则指定的路径。  
  
    -   **@compress_snapshot** -将值指定为 **true** 如果备用快照文件夹中的快照文件压缩在 CAB 文件格式。  
  
    -   **@pre_snapshot_script** -指定文件名和完整路径 **.sql** 将执行在订阅服务器在初始化期间应用初始快照之前的文件。  
  
    -   **@post_snapshot_script** -指定文件名和完整路径 **.sql** 之后将执行在订阅服务器在初始化期间应用初始快照的文件。  
  
    -   **@snapshot_in_defaultfolder** -将值指定为 **false** 如果快照仅在非默认位置可用。  
  
2.  有关创建发布的详细信息，请参阅 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
### 修改现有快照发布或事务发布的快照属性  
  
1.  在发布服务器上对发布数据库中，执行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。 将值指定为 **1** 为 **@force_invalidate_snapshot** 以及下列其中一项值为 **@property**:  
  
    -   **alt_snapshot_folder** -还指定的备用快照文件夹的新路径 **@value**。  
  
    -   **compress_snapshot** -还指定其中任何值 **true** 或 **false** 为 **@value** 以指示备用快照文件夹中的快照文件压缩在 CAB 文件格式。  
  
    -   **pre_snapshot_script** -也为 **@value** 指定文件名和完整路径 **.sql** 将执行在订阅服务器在初始化期间应用初始快照之前的文件。  
  
    -   **post_snapshot_script** -也为 **@value** 指定文件名和完整路径 **.sql** 之后将执行在订阅服务器在初始化期间应用初始快照的文件。  
  
    -   **snapshot_in_defaultfolder** -还指定其中任何值 **true** 或 **false** 以指示快照仅在非默认位置中是否可用。  
  
2.  （可选）在发布服务器上对发布数据库中，执行 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)。 指定 **@publication** 以及将要更改的一个或多个计划或安全凭据参数。  
  
    > [!IMPORTANT]  
    >  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
3.  在命令提示符处运行 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) 或启动快照代理作业以生成新的快照。 有关详细信息，请参阅 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
### 修改现有合并发布的快照属性  
  
1.  在发布服务器上对发布数据库中，执行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 将值指定为 **1** 为 **@force_invalidate_snapshot** 以及下列其中一项值为 **@property**:  
  
    -   **alt_snapshot_folder** -还指定的备用快照文件夹的新路径 **@value**。  
  
    -   **compress_snapshot** -还指定其中任何值 **true** 或 **false** 为 **@value** 以指示备用快照文件夹中的快照文件压缩在 CAB 文件格式。  
  
    -   **pre_snapshot_script** -也为 **@value** 指定文件名和完整路径 **.sql** 将执行在订阅服务器在初始化期间应用初始快照之前的文件。  
  
    -   **post_snapshot_script** -也为 **@value** 指定文件名和完整路径 **.sql** 之后将执行在订阅服务器在初始化期间应用初始快照的文件。  
  
    -   **snapshot_in_defaultfolder** -还指定其中任何值 **true** 或 **false** 以指示快照仅在非默认位置中是否可用。  
  
2.  在命令提示符处运行 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) 或启动快照代理作业以生成新的快照。 有关详细信息，请参阅 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
## 示例  
 此示例创建一个使用备用快照文件夹和压缩快照的发布。  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## 另请参阅  
 [备用快照文件夹位置](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [压缩的快照](../../../relational-databases/replication/compressed-snapshots.md)   
 [在应用快照之前和之后执行脚本](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [通过 FTP 传输快照](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  