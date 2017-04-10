---
title: "发布服务器信息，订阅监视列表（快照发布，SQL Server 2005 和更高版本） | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publisherinfo.subscriptionssummary.snapshot.f1"
ms.assetid: 2ebeee62-7f54-4c77-9d37-15708bc5cc23
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 发布服务器信息，订阅监视列表（快照发布，SQL Server 2005 和更高版本）
  在运行 **及更高版本的分发服务器上，可以使用** “订阅监视列表” [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 选项卡；此选项卡用于显示所选发布服务器上的所有可用发布中的订阅的相关信息。 可以筛选订阅列表，以查看有错误的订阅、出现警告的订阅以及所有性能较差的订阅。 此选项卡提供了用于管理员可以监视的发布服务器上的所有复制活动的单个位置︰ 复制都监视器显示需要注意，根据所选的复制类型和中选择的选项的所有订阅 **显示** 下拉列表框。 由于此选项卡上显示的项基于当前状态和性能，因此只有与 **“显示”** 列表框中的当前选项相匹配的订阅才会显示在此页上。  
  
## 选项  
 有关订阅的详细信息及相关任务，请右键单击相应订阅所在的行，再单击快捷菜单上的选项。 若要更改网格显示数据的方式，请右键单击网格，然后单击以下选项之一：  
  
-   **排序**：按 **“列排序”** 对话框中的一列或多列排序。  
  
-   **选择要显示的列**：选择要显示哪些列以及要在 **“选择列”** 对话框中以何种顺序显示它们。  
  
-   **筛选器**：根据 **“筛选设置”** 对话框中的列值筛选网格中的行。  
  
-   **清除筛选器**：清除网格的任何筛选设置。  
  
 筛选设置是特定于每个网格的。 列的选择和排序应用于同一类型的所有网格，如每个发布服务器的发布网格。  
  
 **显示快照订阅**  
 为所选发布服务器选择要显示的订阅类型（事务、快照或合并）。  
  
 **显示**  
 为所选订阅类型选择要显示的订阅状态。 例如，可以选择仅显示包含错误的订阅。  
  
 **状态**  
 每一个订阅的状态，该状态由快照代理或分发代理的状态决定（显示优先级较高的状态）。  
  
 默认情况下，包含订阅信息的网格按 **“状态”** 列排序。 下面的列表显示了可能的状态值以及这些值的排序顺序（例如，错误项始终显示在该网格的顶部）：  
  
-   错误  
  
-   即将过期/已过期  
  
-   未初始化的订阅   
  
-   正在重试失败的命令  
  
-   同步  
  
-   未同步  
  
 如果给定的订阅处于多种状态，该排序顺序还决定将要显示哪个值。 例如，如果某个订阅包含错误并且即将过期， **“状态”** 列将显示 **“错误”**。  
  
 对 status 值 **即将过期/已过期** 和 **未初始化的订阅** 都是警告。 当显示警告时，“状态”  列还可显示是否正在运行代理。 例如，状态可以为 **正在运行，即将过期/已过期**。  
  
 状态值 **即将过期/已过期** 设置阈值的情况下，才会显示。 设置阈值的信息，请参阅 [设置阈值和警告在复制监视器中的](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 **订阅**  
 每个订阅，请在窗体的名称︰ *SubscriberName: SubscriptionDatabaseName*。  
  
 **发布**  
 与订阅同步，窗体中的发布的名称︰ *PublicationDatabaseName: PublicationName*。  
  
 **上次同步**  
 分发代理上次运行的时间。 如果正在进行同步，则显示 **“正在进行”** 。  
  
## 另请参阅  
 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [查看信息并为发布服务器和 #40; 执行任务复制监视器 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [监视复制](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  