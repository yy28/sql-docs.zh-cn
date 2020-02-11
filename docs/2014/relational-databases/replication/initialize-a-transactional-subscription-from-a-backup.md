---
title: 从备份初始化事务订阅（复制 Transact-sql 编程） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
- transactional replication, backup and restore
- backups [SQL Server replication], transactional replication
ms.assetid: d0637fc4-27cc-4046-98ea-dc86b7a3bd75
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7e7fb32de254729c4173fab260e5797db5f2cc2f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67793303"
---
# <a name="initialize-a-transactional-subscription-from-a-backup-replication-transact-sql-programming"></a>从备份初始化事务订阅（复制 Transact-SQL 编程）
  虽然通常使用快照来初始化对事务发布的订阅，但也可以使用复制存储过程通过备份初始化订阅。 有关详细信息，请参阅 [初始化事务订阅（不使用快照）](initialize-a-transactional-subscription-without-a-snapshot.md)中手动初始化订阅。  
  
### <a name="to-initialize-a-transactional-subscriber-from-a-backup"></a>从备份初始化事务订阅服务器  
  
1.  对于现有的发布，请通过在发布服务器上对发布数据库执行 [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) 来确保该发布支持从备份进行初始化操作。 请注意结果集中 **allow_initialize_from_backup** 的值。  
  
    -   如果值为 **1**，则该发布支持此功能。  
  
    -   如果值为 **0**，则在发布服务器上对发布数据库执行 [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)。 ** \@为** `true` ** \@属性**指定**allow_initialize_from_backup**的值，并将值指定为。  
  
2.  对于新发布，在发布服务器上对发布数据库执行 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)。 将的值指定`true`为**allow_initialize_from_backup**。 有关详细信息，请参阅[创建发布](publish/create-a-publication.md)。  
  
    > [!WARNING]  
    >  为了避免丢失订阅服务器数据，在将 **sp_addpublication** 与 `@allow_initialize_from_backup = N'true'`一起使用时，始终使用 `@immediate_sync = N'true'`。  
  
3.  使用 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql) 语句创建发布数据库的备份。  
  
4.  使用 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql) 语句在订阅服务器上还原备份。  
  
5.  在发布服务器上对发布数据库执行存储过程 [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)。 指定下列参数：  
  
    -   sync_type-值为**initialize with backup**。 ** \@**  
  
    -   backupdevicetype-备份设备的类型： **logical** （默认）、**磁盘**或**磁带**。 ** \@**  
  
    -   backupdevicename-用于还原的逻辑或物理备份设备。 ** \@**  
  
         对于逻辑设备，指定使用 **sp_addumpdevice** 创建该设备时指定的备份设备的名称。  
  
         对于物理设备，指定完整的路径和文件名，比如 `DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\BACKUP\Mybackup.dat'` 或 `TAPE = '\\.\TAPE0'`。  
  
    -   可有可无password-创建备份集时提供的密码。 ** \@**  
  
    -   可有可无mediapassword-格式化介质集时提供的密码。 ** \@**  
  
    -   可有可无fileidhint-要还原的备份集的标识符。 ** \@** 例如，指定为 **1** 表示备份介质中的第一个备份集，而指定为 **2** 则表示第二个备份集。  
  
    -   （对于磁带设备是可选的）unload-如果还原完成后应从驱动器卸载磁带，则将值指定为**1** （默认值）; 如果不应卸载磁带，则指定为**0** 。 ** \@**  
  
6.  （可选）对于请求订阅，在订阅服务器上对订阅数据库执行 [sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql) 和 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)。 有关详细信息，请参阅 [创建请求订阅](create-a-pull-subscription.md)。  
  
7.  （可选）启动分发代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 或 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)。  
  
## <a name="see-also"></a>另请参阅  
 [通过备份和还原复制数据库](../databases/copy-databases-with-backup-and-restore.md)   
 [SQL Server 数据库的备份和还原](../backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
