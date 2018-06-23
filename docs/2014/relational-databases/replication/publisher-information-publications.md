---
title: 发布服务器信息，发布 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.monitor.publisherinfo.publications.f1
ms.assetid: 0b2e3d4e-03b7-4c31-8f96-48648d750010
caps.latest.revision: 26
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ea246905aa410a8c6d69a9e757ef5ec297601c93
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027890"
---
# <a name="publisher-information-publications"></a>发布服务器信息，发布
  **“发布”** 选项卡提供在左窗格中选择的发布服务器的所有发布的摘要信息。  
  
## <a name="options"></a>“常规”  
 若要更改网格显示数据的方式，请右键单击网格，然后单击以下选项之一：  
  
-   **排序**：按 **“列排序”** 对话框中的一列或多列排序。  
  
-   **选择要显示的列**：选择要显示哪些列以及要在 **“选择列”** 对话框中以何种顺序显示它们。  
  
-   **筛选器**：根据 **“筛选设置”** 对话框中的列值筛选网格中的行。  
  
-   **清除筛选器**：清除网格的任何筛选设置。  
  
 筛选设置是特定于每个网格的。 列的选择和排序应用于同一类型的所有网格，如每个发布服务器的发布网格。  
  
 **“状态”**  
 每个发布的状态，由其订阅的最高优先级状态决定。 默认情况下，包含发布信息的网格按 **“状态”** 列排序。 下面的列表显示了可能的状态值以及这些值的排序顺序（例如，错误项始终显示在该网格的顶部）：  
  
-   错误  
  
-   “严重”状态下的性能  
  
-   正在重试失败的命令  
  
-   “确定”  
  
 状态值 **“‘严重’状态下的性能”** 与事务订阅和合并订阅相关；只有设置阈值后，才可以显示该值。 有关性能度量和设置阈值的信息，请参阅[使用复制监视器监视性能](monitor/monitor-performance-with-replication-monitor.md)和[在复制监视器中设置阈值和警告](monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
 **发布**  
 每个发布的名称，格式为 *PublicationDatabaseName: PublicationName*。  
  
 **订阅**  
 每个发布的订阅数量。  
  
 **同步**  
 当前正在同步的每个发布的订阅数量：  
  
-   对于事务复制，“同步”意味着分发代理正在运行，但是无需复制数据。  
  
-   对于合并复制，“同步”意味着合并代理正在运行，并且正在复制数据。  
  
-   对于快照复制，“同步”意味着分发代理正在运行，并且正在复制数据。  
  
 **“当前平均性能”** 和 **“当前最差的性能”**  
 仅限[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本。 发布的所有订阅各自的平均性能率和最差性能率。 这些比率是基于复制监视器最近取得的度量值，并不反映某段时间内的订阅性能。  
  
 对于事务复制，复制监视器仅为定义了性能阈值的发布显示值。 如果没有为发布定义性能阈值，则此列将显示 **“未启用”**。 对于合并复制，在通过同一类型的连接（拨号或 LAN）进行了五次同步、并且每次同步所做的更改为 50 处或更多处之后，复制监视器将会显示值。 如果所做更改为 50 处或更多处的同步次数少于五次，或最近一次同步所做的更改少于 50 处，则此列为空白。  
  
 性能等级可以为以下值之一：  
  
-   很好  
  
-   好  
  
-   一般  
  
-   较差  
  
-   严重  
  
 有关如何定义性能等级以及如何设置性能阈值的详细信息，请参阅[使用复制监视器监视性能](monitor/monitor-performance-with-replication-monitor.md)。  
  
## <a name="see-also"></a>请参阅  
 [启动复制监视器](monitor/start-the-replication-monitor.md)   
 [查看发布服务器的信息和执行其任务（复制监视器）](monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [监视复制](monitoring-replication.md)  
  
  