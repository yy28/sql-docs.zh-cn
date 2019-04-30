---
title: 发布服务器信息，订阅监视列表 （快照发布，SQL Server 2005 和更高版本） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publisherinfo.subscriptionssummary.snapshot.f1
ms.assetid: 2ebeee62-7f54-4c77-9d37-15708bc5cc23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0b84f87aff9684cc08fc0d91fc5de364f816125a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262149"
---
# <a name="publisher-information-subscription-watch-list-snapshot-publication-sql-server-2005-and-later"></a>发布服务器信息，订阅监视列表（快照发布，SQL Server 2005 和更高版本）
  在运行 **及更高版本的分发服务器上，可以使用** “订阅监视列表” [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 选项卡；此选项卡用于显示所选发布服务器上的所有可用发布中的订阅的相关信息。 可以筛选订阅列表，以查看有错误的订阅、出现警告的订阅以及所有性能较差的订阅。 此选项卡为管理员提供了监视发布服务器上所有复制活动的单一位置：复制监视器根据所选复制类型以及“显示”下拉列表框中选择的选项，显示需要注意的所有订阅。 由于此选项卡上显示的项基于当前状态和性能，因此只有与 **“显示”** 列表框中的当前选项相匹配的订阅才会显示在此页上。  
  
## <a name="options"></a>选项  
 有关订阅的详细信息及相关任务，请右键单击相应订阅所在的行，再单击快捷菜单上的选项。 若要更改网格显示数据的方式，请右键单击网格，然后单击以下选项之一：  
  
-   **排序**：在“列排序”对话框中对一列或多个列进行排序。  
  
-   **选择要显示的列**：在“选择列”对话框中选择要显示的列以及它们的显示顺序。  
  
-   **筛选器**：根据“筛选设置”对话框中的列值筛选网格中的行。  
  
-   **清除筛选器**：清除网格的任何筛选设置。  
  
 筛选设置是特定于每个网格的。 列的选择和排序应用于同一类型的所有网格，如每个发布服务器的发布网格。  
  
 **显示快照订阅**  
 为所选发布服务器选择要显示的订阅类型（事务、快照或合并）。  
  
 **“显示”**  
 为所选订阅类型选择要显示的订阅状态。 例如，可以选择仅显示包含错误的订阅。  
  
 **“状态”**  
 每一个订阅的状态，该状态由快照代理或分发代理的状态决定（显示优先级较高的状态）。  
  
 默认情况下，包含订阅信息的网格按 **“状态”** 列排序。 下面的列表显示了可能的状态值以及这些值的排序顺序（例如，错误项始终显示在该网格的顶部）：  
  
-   错误  
  
-   即将过期/已过期  
  
-   未初始化的订阅  
  
-   正在重试失败的命令  
  
-   正在同步  
  
-   未同步  
  
 如果给定的订阅处于多种状态，该排序顺序还决定将要显示哪个值。 例如，如果某个订阅包含错误并且即将过期， **“状态”** 列将显示 **“错误”**。  
  
 状态值 **“即将过期/已过期”** 和 **“未初始化的订阅”** 属于警告。 当显示警告时，“状态”  列还可显示是否正在运行代理。 例如，状态可以为 **“正在运行，即将过期/已过期”**。  
  
 只有在设置了阈值时，才会显示状态值 **“即将过期/已过期”** 。 有关设置阈值的信息，请参阅[在复制监视器中设置阈值和警告](monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 **订阅**  
 每个订阅的名称，格式为：SubscriberName:SubscriptionDatabaseName。  
  
 **发布**  
 与订阅同步的发布的名称，格式为：PublicationDatabaseName:PublicationName。  
  
 **上次同步**  
 分发代理上次运行的时间。 如果正在进行同步，则显示 **“正在进行”** 。  
  
## <a name="see-also"></a>请参阅  
 [启动复制监视器](monitor/start-the-replication-monitor.md)   
 [使用复制监视器查看信息和执行任务](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [监视复制](monitoring-replication.md)  
  
  
