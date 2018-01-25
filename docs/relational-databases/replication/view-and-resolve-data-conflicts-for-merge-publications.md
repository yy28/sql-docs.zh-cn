---
title: "查看和解决合并发布的数据冲突 | Microsoft Docs"
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
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
caps.latest.revision: "41"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6ba5f6cdb6c81e5a9d59efe770daa7f1b069d6fd
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="view-and-resolve-data-conflicts-for-merge-publications"></a>查看和解决合并发布的数据冲突
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]可以根据为每个项目指定的冲突解决程序来解决合并发布中的冲突。 默认情况下，解决冲突无需用户干预。 但是，可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 复制冲突查看器中查看冲突，并更改解决的结果。  
  
 在冲突保持期的指定时间（默认值为 14 天）内，可以在复制冲突查看器中查看冲突数据。 若要设置冲突保持期，请执行以下任一操作：  
  
-   为 [sp_addmergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 的 **@conflict_retention** 参数指定保持值。  
  
-   为 **@property** 参数指定 **conflict_retention** 值，并为 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 的 **@value** 参数指定保持值。  
  
 默认情况下，冲突信息存储在下列位置：  
  
-   如果发布兼容级别为 90RTM 或更高，则存储在发布服务器和订阅服务器上。  
  
-   如果发布兼容级别低于 80RTM，则存储在发布服务器上。  
  
-   如果订阅服务器运行的是 [!INCLUDE[ssEW](../../includes/ssew-md.md)]，则存储在发布服务器上。 冲突数据不能存储在 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 订阅服务器上。  
  
 冲突信息的存储受 **conflict_logging** 发布属性的控制。 有关详细信息，请参阅 [sp_addmergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 和 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。  
  
 也可以在同步过程中使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 交互式冲突解决程序以交互方式解决冲突。 交互式冲突解决程序可以通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 同步管理器获取。 有关详细信息，请参阅[使用 Windows 同步管理器同步订阅（Windows 同步管理器）](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)。  
  
### <a name="to-view-and-resolve-conflicts-for-merge-publications"></a>查看和解决合并发布的冲突  
  
1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到发布服务器（或订阅服务器，若适合的话），然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击要查看其冲突的发布，然后单击 **“查看冲突”**。  
  
    > [!NOTE]  
    >  如果为 **conflict_logging** 属性指定了值 **“subscriber”** ， **“查看冲突”** 菜单选项将不可用。 若要查看冲突，请在命令提示符下启动 ConflictViewer.exe。 默认情况下，ConflictViewer.exe 位于以下目录中：Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE。 要获取有效引导参数的列表，请运行 ConflictViewer.exe -?。  
  
4.  在 **“选择冲突表”** 对话框中，选择要查看冲突的数据库、发布和表。  
  
5.  在复制冲突查看器中可以：  
  
    -   使用上部网格右侧的按钮来筛选行。  
  
    -   在上部网格中选择行，以在下部网格中显示该行的信息。  
  
    -   在上部网格中选择一行或多行，然后单击 **“删除”**，这与单击 **“提交入选方”** 按钮的效果相同（不对数据进行任何更改）。  
  
    -   单击属性按钮 (**...**) 查看有关冲突所涉及的列的详细信息。  
  
    -   编辑 **“冲突解决入选方”** 或 **“冲突解决落选方”** 列中的数据，然后再提交数据（如果列为灰色，则数据为只读）。  
  
    -   单击 **“提交入选方”** 接受指定为冲突入选方的行。  
  
    -   单击 **“提交落选方”** 覆盖解决结果，并将指定为冲突落选方的值传播到拓扑中的所有节点。  
  
    -   选择 **“记录此冲突的详细信息”** 将冲突数据记录到一个文件中。 若要指定文件的位置，请指向 **“查看”** 菜单，然后单击 **“选项”**。 输入一个值，或单击浏览按钮 (**...**)，然后导航到相应文件。 单击 **“确定”** 可退出 **“选项”** 对话框。  
  
6.  关闭复制冲突查看器。  
  
## <a name="see-also"></a>另请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [指定合并项目冲突解决程序](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  
