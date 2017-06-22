---
title: "查看事务发布的数据冲突 (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
- viewing conflict information
ms.assetid: 9977dd75-b0de-4376-9c13-86d80567d8aa
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 966493051334ca3ead4b6412545ab77e97edafc0
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="view-data-conflicts-for-transactional-publications-sql-server-management-studio"></a>查看事务发布的数据冲突 (SQL Server Management Studio)
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 复制冲突查看器中，您可以查看对等事务复制和具有排队更新订阅的事务复制的冲突。 有关如何检测和解决冲突的信息，请参阅[对等复制中的冲突检测](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)和[设置排队更新冲突解决选项 (SQL Server Management Studio)](../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)。  
  
 冲突数据的可用性取决于复制的类型和冲突保持期：  
  
-   对于对等复制，默认情况下，分发代理在检测到冲突时将会失败。 冲突错误会记录到错误日志中，但是冲突数据不会记录到冲突表中；因此没有可供查看的冲突数据。 如果允许分发代理继续运行，将在检测到冲突的每个节点本地记录冲突。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)中的“处理冲突”。  
  
-   对于排队更新订阅，每个冲突的数据都可用。 在冲突保持期的指定时间（默认值为 14 天）内，可以在复制冲突查看器中查看冲突数据。 若要设置冲突保持期，请执行以下操作之一：  
  
    -   为 @conflict_retention sp_addpublication [的](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)参数指定保持值。  
  
    -   将 **@property** 参数的值指定为 @property ，并为 @value sp_addpublication [的](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。  
  
### <a name="to-view-conflicts"></a>查看冲突  
  
1.  连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的相应服务器，然后展开该服务器节点：  
  
    -   对于对等复制，此为发生冲突的节点。  
  
    -   对于排队更新订阅，此为发布服务器。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击要查看其冲突的发布，然后单击 **“查看冲突”**。  
  
4.  在 **“选择冲突表”** 对话框中，选择要查看冲突的数据库、发布和表。  
  
5.  在复制冲突查看器中可以：  
  
    -   使用上部网格右侧的按钮来筛选行。  
  
    -   在上部网格中选择行，以在下部网格中显示该行的信息。  
  
    -   在上部网格中选择一行或多行，再单击 **“删除”**，即从冲突元数据表中删除相应行。  
  
    -   单击属性按钮 (**...**) 查看有关冲突所涉及的列的详细信息。  
  
    -   选择 **“记录此冲突的详细信息”** 将冲突数据记录到一个文件中。 若要指定文件的位置，请指向 **“查看”** 菜单，然后单击 **“选项”**。 输入一个值，或单击浏览按钮 (**...**)，然后导航到相应文件。 单击 **“确定”** 关闭 **“选项”** 对话框。  
  
6.  关闭复制冲突查看器。  
  
## <a name="see-also"></a>另请参阅  
 [对等事务复制](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
