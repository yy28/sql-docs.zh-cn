---
title: "发布服务器信息，订阅监视列表（事务发布，SQL Server 2005 和更高版本） | Microsoft Docs"
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
  - "sql13.rep.monitor.publisherinfo.subscriptionssummary.tran.f1"
ms.assetid: 6bc64ddb-5c86-4681-a391-77fc1d3c4e6e
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 发布服务器信息，订阅监视列表（事务发布，SQL Server 2005 和更高版本）
  **“订阅监视列表”** 选项卡可用于运行 SQL Server 2005 及更高版本的分发服务器；用来显示所选发布服务器上所有可用发布中的订阅的有关信息。 可以筛选订阅列表，以查看有错误的订阅、出现警告的订阅以及所有性能较差的订阅。 此选项卡提供了用于管理员可以监视的发布服务器上的所有复制活动的单个位置︰ 复制都监视器显示需要注意，根据所选的复制类型和中选择的选项的所有订阅 **显示** 下拉列表框。 由于此选项卡上显示的项基于当前状态和性能，因此只有与 **“显示”** 列表框中的当前选项相匹配的订阅才会显示在此页上。  
  
## 选项  
 有关订阅的详细信息及相关任务，请右键单击相应订阅所在的行，再单击快捷菜单上的选项。 若要更改网格显示数据的方式，请右键单击网格，然后单击以下选项之一：  
  
-   **排序**：按 **“列排序”** 对话框中的一列或多列排序。  
  
-   **选择要显示的列**：选择要显示哪些列以及要在 **“选择列”** 对话框中以何种顺序显示它们。  
  
-   **筛选器**：根据 **“筛选设置”** 对话框中的列值筛选网格中的行。  
  
-   **清除筛选器**：清除网格的任何筛选设置。  
  
 筛选设置是特定于每个网格的。 列的选择和排序应用于同一类型的所有网格，如每个发布服务器的发布网格。  
  
 **显示事务订阅**  
 为所选发布服务器选择要显示的订阅类型（事务、快照或合并）。  
  
 **显示**  
 为所选订阅类型选择要显示的订阅状态。 例如，可以选择仅显示包含错误的订阅。  
  
 **状态**  
 每个订阅的状态，由分发代理或日志读取器代理的状态决定（显示优先级较高的状态；如果使用排队更新订阅，则状态还可以由队列读取器代理决定）。  
  
 默认情况下，包含订阅信息的网格按排序 **状态** 列 (然后按排序 **性能** 这些订阅具有相同状态的列)。 下面的列表显示了可能的状态值以及这些值的排序顺序（例如，错误项始终显示在该网格的顶部）：  
  
-   错误  
  
-   “严重”状态下的性能  
  
-   即将过期/已过期  
  
-   未初始化的订阅   
  
-   正在重试失败的命令  
  
-   未运行  
  
-   正在运行  
  
 如果给定的订阅处于多种状态，该排序顺序还决定将要显示哪个值。 例如，如果某个订阅包含错误并且即将过期， **“状态”** 列将显示 **“错误”**。  
  
 对 status 值 **性能关键**, ，**即将过期/已过期**, ，和 **未初始化的订阅** 都是警告。 当显示警告时，“状态”  列还可显示是否正在运行代理。 例如，状态可能为 **“正在运行，‘严重’状态下的性能”**。  
  
 对 status 值 **性能关键** 和 **即将过期/已过期** 仅当设置了阈值时，才会显示。 有关性能度量和设置阈值的信息，请参阅 [用复制监视器监视性能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) 和 [设置阈值和警告在复制监视器中的](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 **订阅**  
 每个订阅，请在窗体的名称︰ *SubscriberName: SubscriptionDatabaseName*。  
  
 **发布**  
 与订阅同步，窗体中的发布的名称︰ *PublicationDatabaseName: PublicationName*。  
  
 **性能**  
 每个订阅的性能等级都是基于复制监视器的最新度量值，并不反映历史性能。 对于为发布定义了性能阈值的订阅，均会度量其性能；如果没有为发布定义性能阈值，此列将显示 **“未启用”**。 性能等级可以为以下值之一：  
  
-   很好  
  
-   好  
  
-   一般  
  
-   较差  
  
-   严重  
  
 如果性能状态为“严重”，则 **“状态”** 列中将显示 **“‘严重’状态下的性能”** 。 有关如何定义性能等级以及如何设置性能阈值的详细信息，请参阅 [用复制监视器监视性能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。  
  
 **滞后时间**  
 事务在发布服务器上提交和相应的事务在订阅服务器上提交之间间隔的平均时间。 所显示的滞后时间基于复制监视器的最新度量值。 有关度量滞后时间的详细信息，请参阅 [测量滞后时间和验证对于事务复制的连接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)。  
  
 **上次同步**  
 分发代理上次运行的时间。 如果正在进行同步，则显示 **“正在进行”** 。  
  
## 另请参阅  
 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [查看信息并为发布服务器和 #40; 执行任务复制监视器 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [监视复制](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  