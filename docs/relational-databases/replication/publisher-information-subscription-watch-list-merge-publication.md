---
title: "发布服务器信息，订阅监视列表（合并发布）| Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.publisherinfo.subscriptionssummary.merge.f1
ms.assetid: 4ec956bf-5cef-4377-a1d1-8c7f0107a6cb
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f1a6afe57c26dcf92aa82a9542cd65f9f3997d44
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="publisher-information-subscription-watch-list-merge-publication"></a>发布服务器信息，订阅监视列表（合并发布）
  在运行 **及更高版本的分发服务器上，可以使用** “订阅监视列表” [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 选项卡；此选项卡用于显示所选发布服务器上的所有可用发布中的订阅的相关信息。 可以筛选订阅列表，以查看有错误的订阅、出现警告的订阅以及所有性能较差的订阅。 此选项卡为管理员提供了监视发布服务器上所有复制活动的单一位置：复制监视器根据所选复制类型和在 **“显示”** 下拉列表框中选择的选项，显示所有需要注意的订阅。 由于此选项卡上显示的项基于当前状态和性能，因此只有与 **“显示”** 列表框中的当前选项相匹配的订阅才会显示在此页上。  
  
## <a name="options"></a>选项  
 有关订阅的详细信息及相关任务，请右键单击相应订阅所在的行，再单击快捷菜单上的选项。 若要更改网格显示数据的方式，请右键单击网格，然后单击以下选项之一：  
  
-   **排序**：按 **“列排序”** 对话框中的一列或多列排序。  
  
-   **选择要显示的列**：选择要显示哪些列以及要在 **“选择列”** 对话框中以何种顺序显示它们。  
  
-   **筛选器**：根据 **“筛选设置”** 对话框中的列值筛选网格中的行。  
  
-   **清除筛选器**：清除网格的任何筛选设置。  
  
 筛选设置是特定于每个网格的。 列的选择和排序应用于同一类型的所有网格，如每个发布服务器的发布网格。  
  
 **显示合并订阅**  
 为所选发布服务器选择要显示的订阅类型（事务、快照或合并）。  
  
 **“显示”**  
 为所选订阅类型选择要显示的订阅状态。 例如，可以选择仅显示包含错误的订阅。  
  
 **状态**  
 每个订阅的状态，这取决于合并代理的状态。  
  
 默认情况下，包含订阅信息的网格按 **“状态”** 列排序（对于具有相同状态的订阅，再按 **“性能”** 列排序）。 下面的列表显示了可能的状态值以及这些值的排序顺序（例如，错误项始终显示在该网格的顶部）：  
  
-   错误  
  
-   “严重”状态下的性能  
  
-   长时间运行的合并  
  
-   即将过期/已过期  
  
-   未初始化的订阅  
  
-   正在重试失败的命令  
  
-   同步  
  
-   未同步  
  
 如果给定的订阅处于多种状态，该排序顺序还决定将要显示哪个值。 例如，如果某个订阅包含错误并且即将过期，“状态”  列将显示“错误” 。  
  
 状态值 **“‘严重’状态下的性能”**、 **“长时间运行的合并”**、 **“即将过期/已过期”**和 **“未初始化的订阅”** 都是警告。 当显示警告时， **“状态”** 列还可显示是否正在同步代理。 例如，状态可能为 **“同步，‘严重’状态下的性能”**。  
  
 只有在设置了阈值时，才会显示状态值 **“即将过期/已过期”** 和 **“长时间运行的合并”** 。 只有在使用相同的连接类型（拨号或 LAN）对订阅进行五次同步后，才会显示状态值 **“‘严重’状态下的性能”** 。 有关性能度量和设置阈值的信息，请参阅[使用复制监视器监视性能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)和[在复制监视器中设置阈值和警告](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 **订阅**  
 每个订阅的名称，格式为：*SubscriberName: SubscriptionDatabaseName*。  
  
 **友好名称**  
 每个订阅的说明。 此说明是在 **“订阅属性”** 对话框中输入的，或是用 **@description** 或 [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) 的 [@description](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 用户通常将说明用作订阅的“友好名称”或别名。  
  
 **发布**  
 与订阅同步的发布的名称，格式为： *PublicationDatabaseName: PublicationName*。  
  
 **“性能”**  
 每个订阅的性能等级，这是基于复制监视器对传送速率的最新度量值来确定的。 对于具有相同连接类型（拨号或 LAN）的发布的订阅，通过将单独的订阅性能与其平均历史性能进行比较，可以确定性能等级。 如果通过同一类型的连接进行了五次同步，且每次同步都进行了 50 处或更多的更改，则复制监视器将在此列中显示一个值。 如果所做更改为 50 处或更多处的同步次数少于五次，或最近一次同步所做的更改少于 50 处，则此列为空白。  
  
> [!NOTE]  
>  性能是根据 **“连接”** 列中显示的连接类型确定的；因此，对于较低传送速率的订阅来说，如果是通过较慢速度的连接进行同步的，那么该订阅也有可能显示出比其他订阅更高的性能等级。  
  
 性能等级可以为以下值之一：  
  
-   很好  
  
-   好  
  
-   一般  
  
-   较差  
  
 有关如何定义性能等级以及如何设置性能阈值的详细信息，请参阅[使用复制监视器监视性能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。  
  
 **传送速率**  
 合并代理每秒处理的行数。  
  
 **上次同步**  
 合并代理上次运行的时间。 在此同步过程中，更改可能已处理，也可能尚未处理。 如果正在进行同步，则会显示完成百分比值。  
  
 **Duration**  
 上次同步过程中合并代理运行所用的时间。 如果合并代理当前正在同步，该时间表示已运行的时间；如果合并代理之前已经同步，该时间则表示上次同步所用的总时间。  
  
 **“连接”**  
 订阅服务器与发布服务器之间的连接类型。 可能的值包括 **LAN**、 **“拨号”**和 **Internet**。 如果订阅使用 Web 同步，则会显示 **Internet** 值。  
  
## <a name="see-also"></a>另请参阅  
 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [查看发布服务器的信息和执行其任务（复制监视器）](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [监视复制](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
