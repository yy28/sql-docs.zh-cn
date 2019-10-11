---
title: 查看和解决合并发布的数据冲突 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9e3de9c6652de3ddd8d80bbc2d09b003acfe5220
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710679"
---
# <a name="conflict-resolution-for-merge-replication"></a>合并复制的冲突解决
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可以根据为每个项目指定的冲突解决程序来解决合并发布中的冲突。 默认情况下，解决冲突无需用户干预。 但是，可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 复制冲突查看器中查看冲突，并更改解决的结果。  
  
 在冲突保持期的指定时间（默认值为 14 天）内，可以在复制冲突查看器中查看冲突数据。 若要设置冲突保持期，请执行以下任一操作：  
  
-   为 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 的 `@conflict_retention` 参数指定保留期值。  
  
-   为 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 的 `@property` 参数指定 conflict_retention  值，并为 `@value` 参数指定保留期值。  
  
 默认情况下，冲突信息存储在下列位置：    
-   如果发布兼容级别为 90RTM 或更高，则存储在发布服务器和订阅服务器上。   
-   如果发布兼容级别低于 80RTM，则存储在发布服务器上。   
-   如果订阅服务器运行的是 [!INCLUDE[ssEW](../../includes/ssew-md.md)]，则存储在发布服务器上。 冲突数据不能存储在 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 订阅服务器上。  
  
 冲突信息的存储受 **conflict_logging** 发布属性的控制。 有关详细信息，请参阅 [sp_addmergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 和 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。  
  
 也可以在同步过程中使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 交互式冲突解决程序以交互方式解决冲突。 交互式冲突解决程序可以通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 同步管理器获取。 有关详细信息，请参阅[使用 Windows 同步管理器同步订阅（Windows 同步管理器）](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)。  
  
## <a name="resolve-conflicts"></a>解决冲突  
  
1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到发布服务器（或订阅服务器，若适合的话），然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击要查看其冲突的发布，然后单击 **“查看冲突”** 。  
  
    > [!NOTE]  
    >  如果为 **conflict_logging** 属性指定了值 **“subscriber”** ， **“查看冲突”** 菜单选项将不可用。 若要查看冲突，请在命令提示符下启动 ConflictViewer.exe。 默认情况下，ConflictViewer.exe 位于以下目录中：Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE。 要获取有效引导参数的列表，请运行 ConflictViewer.exe -?。  
  
4.  在 **“选择冲突表”** 对话框中，选择要查看冲突的数据库、发布和表。  
  
5.  在复制冲突查看器中可以：  
  
    -   使用上部网格右侧的按钮来筛选行。  
  
    -   在上部网格中选择行，以在下部网格中显示该行的信息。  
  
    -   在上部网格中选择一行或多行，然后单击 **“删除”** ，这与单击 **“提交入选方”** 按钮的效果相同（不对数据进行任何更改）。  
  
    -   单击属性按钮 (...) 查看有关冲突所涉及的列的详细信息  。  
  
    -   编辑 **“冲突解决入选方”** 或 **“冲突解决落选方”** 列中的数据，然后再提交数据（如果列为灰色，则数据为只读）。  
  
    -   单击 **“提交入选方”** 接受指定为冲突入选方的行。  
  
    -   单击 **“提交落选方”** 覆盖解决结果，并将指定为冲突落选方的值传播到拓扑中的所有节点。  
  
    -   选择 **“记录此冲突的详细信息”** 将冲突数据记录到一个文件中。 若要指定文件的位置，请指向 **“查看”** 菜单，然后单击 **“选项”** 。 输入一个值，或单击浏览按钮 ( **...** )，然后导航到相应文件。 单击 **“确定”** 可退出 **“选项”** 对话框。  
  
6.  关闭复制冲突查看器。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="view-conflict-information"></a>查看冲突信息
在合并复制中解决冲突后，落选行中的数据将写入冲突表中。 这些冲突数据可以使用复制存储过程以编程方式进行查看。 有关详细信息，请参阅 [高级合并复制冲突的检测和解决](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
1.  在发布服务器上，对发布数据库执行 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。 请注意结果集中以下列的值：  
  
    -   **centralized_conflicts** - 1 指示冲突行存储在发布服务器上，0 指示冲突行未存储在发布服务器上。  
  
    -   **decentralized_conflicts** - 1 指示冲突行存储在订阅服务器上，0 指示冲突行未存储在订阅服务器上。  
  
        > [!NOTE]  
        >  合并发布的冲突日志记录行为是通过使用 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 的 `@conflict_logging` 参数设置的。 已不推荐使用 `@centralized_conflicts` 参数。  
  
     下表基于为 `@conflict_logging` 指定的值描述了这些列的值。  
  
    |@conflict_logging 值|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**发布服务器**|1|0|  
    |**订阅服务器**|0|1|  
    |**两者**|1|1|  
  
2.  在发布服务器上对发布数据库，或在订阅服务器上对订阅数据库执行 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)。 为 `@publication` 指定值，以便只返回属于特定发布的项目的冲突信息。 这将返回具有冲突的项目的冲突表信息。 请注意任何相关项目的 **conflict_table** 值。 如果项目的 **conflict_table** 值为 NULL，则在该项目中只发生了删除冲突。  
  
3.  （可选）查看相关项目的冲突行。 根据步骤 1 中 **centralized_conflicts** 和 **decentralized_conflicts** 的值，请执行下列操作之一：  
  
    -   在发布服务器上，对发布数据库执行 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)。 请为步骤 1 中的项目的 `@conflict_table` 指定冲突表。 （可选）指定 `@publication` 的值，以便将返回的冲突信息限制为特定发布。 这将会返回落选行的行数据和其他信息。  
  
    -   在订阅服务器上，对订阅数据库执行 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)。 请为步骤 1 中的项目的 `@conflict_table` 指定冲突表。 这将会返回落选行的行数据和其他信息。  
  
## <a name="conflict-where-delete-failed"></a>无法删除的冲突   
  
1.  在发布服务器上，对发布数据库执行 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。 请注意结果集中以下列的值：  
  
    -   **centralized_conflicts** - 1 指示冲突行存储在发布服务器上，0 指示冲突行未存储在发布服务器上。  
  
    -   **decentralized_conflicts** - 1 指示冲突行存储在订阅服务器上，0 指示冲突行未存储在订阅服务器上。  
  
        > [!NOTE]  
        >  合并发布的冲突日志记录行为是通过使用 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 的 `@conflict_logging` 参数设置的。 已不推荐使用 `@centralized_conflicts` 参数。  
  
2.  在发布服务器上对发布数据库，或在订阅服务器上对订阅数据库执行 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)。 为 `@publication` 指定值，以便只返回属于特定发布的项目的冲突表信息。 这将返回具有冲突的项目的冲突表信息。 请注意任何相关项目的 **source_object** 值。 如果项目的 **conflict_table** 值为 NULL，则在该项目中只发生了删除冲突。  
  
3.  （可选）查看删除冲突的冲突信息。 根据步骤 1 中 **centralized_conflicts** 和 **decentralized_conflicts** 的值，请执行下列操作之一：  
  
    -   在发布服务器上，对发布数据库执行 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)。 为 `@source_object` 指定步骤 1 中发生冲突的源表的名称。 （可选）指定 `@publication` 的值，以便将返回的冲突信息限制为特定发布。 这将返回发布服务器上存储的删除冲突信息。  
  
    -   在订阅服务器上，对订阅数据库执行 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)。 为 `@source_object` 指定步骤 1 中发生冲突的源表的名称。 （可选）指定 `@publication` 的值，以便将返回的冲突信息限制为特定发布。 这将返回订阅服务器上存储的删除冲突信息。  
  
## <a name="see-also"></a>另请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [指定合并项目冲突解决程序](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  
