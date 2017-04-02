---
title: "从备份初始化事务订阅（复制 Transact-SQL 编程） | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
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
  - "手动初始化订阅 [SQL Server 复制]"
  - "订阅 [SQL Server 复制], 初始化"
  - "初始化订阅 [SQL Server 复制], 无快照"
  - "事务复制, 备份和还原"
  - "备份 [SQL Server 复制], 事务复制"
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 从备份初始化事务订阅（复制 Transact-SQL 编程）
  虽然通常使用快照来初始化对事务发布的订阅，但也可以使用复制存储过程通过备份初始化订阅。 有关详细信息，请参阅 [初始化事务订阅不使用快照](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
### 从备份初始化事务订阅服务器  
  
1.  对于现有发布中，请确保该发布支持的功能通过执行从备份初始化 [sp_helppublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) 在发布数据库上的发布服务器。 记下的值 **allow_initialize_from_backup** 结果集中。  
  
    -   如果值为 **1**，则该发布支持此功能。  
  
    -   如果值为 **0**, ，执行 [sp_changepublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) 在发布数据库上的发布服务器。 将值指定为 **allow_initialize_from_backup** 为 **@property** ，值为 **true** 为 **@value**。  
  
2.  对于新发布，执行 [sp_addpublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 在发布数据库上的发布服务器。 将值指定为 **true** 为 **allow_initialize_from_backup**。 有关详细信息，请参阅 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
    > [!WARNING]  
    >  若要避免丢失订阅服务器数据时使用 **sp_addpublication** 与 `@allow_initialize_from_backup = N'true'`, ，始终使用 `@immediate_sync = N'true'`。  
  
3.  创建的发布数据库使用备份 [备份和 #40;Transact SQL & #41;](../../t-sql/statements/backup-transact-sql.md) 语句。  
  
4.  还原订阅服务器上使用备份 [还原 & #40;Transact SQL & #41;](../Topic/RESTORE%20\(Transact-SQL\).md) 语句。  
  
5.  在发布服务器上对发布数据库中，执行存储的过程 [sp_addsubscription & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定下列参数：  
  
    -   **@sync_type** -值为 **用备份初始化**。  
  
    -   **@backupdevicetype** -备份设备的类型︰ **逻辑** （默认值）， **磁盘**, ，或 **磁带**。  
  
    -   **@backupdevicename** -要用于还原的逻辑或物理备份设备。  
  
         对于逻辑设备，指定备份设备时，指定的名称 **sp_addumpdevice** 用于创建该设备。  
  
         对于物理设备，指定完整的路径和文件名，比如 `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\BACKUP\Mybackup.dat'` 或 `TAPE = '\\.\TAPE0'`。  
  
    -   （可选） **@password** -创建备份集时提供的密码。  
  
    -   （可选） **@mediapassword** -格式化介质集时提供的密码。  
  
    -   （可选） **@fileidhint** -要还原的备份集的标识符。 例如，指定为 **1** 表示备份介质中的第一个备份集，而指定为 **2** 则表示第二个备份集。  
  
    -   （对于磁带设备是可选的） **@unload** -将值指定为 **1** （默认值） 如果还原操作已完成后，应从驱动器卸载磁带和 **0** 如果不应卸载。  
  
6.  （可选）对于请求订阅，执行 [sp_addpullsubscription & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md) 和 [sp_addpullsubscription_agent & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) 在订阅服务器上的订阅数据库上。 有关详细信息，请参阅 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
7.  （可选）启动分发代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 或 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
## 另请参阅  
 [通过备份和还原来复制数据库](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [SQL Server 数据库的备份和还原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  