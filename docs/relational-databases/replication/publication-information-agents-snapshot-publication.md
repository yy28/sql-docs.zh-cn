---
title: 发布信息，代理（快照发布）| Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.downlevelagents.snapshot.f1
ms.assetid: 599ff80b-392c-43aa-9db2-dc4ed33d4f6e
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4adefcb8a8548beb0551f5dad2a5753c1764c121
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32962022"
---
# <a name="publication-information-agents-snapshot-publication"></a>发布信息，代理（快照发布）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **“代理”** 选项卡显示所选发布的快照代理的摘要信息。  
  
## <a name="options"></a>“常规”  
 有关快照代理的详细信息及相关任务，请右键单击该代理的行，再单击快捷菜单上的选项。 若要更改网格显示数据的方式，请右键单击网格，然后单击以下选项之一：  
  
-   **排序**：按 **“列排序”** 对话框中的一列或多列排序。  
  
-   **选择要显示的列**：选择要显示哪些列以及要在 **“选择列”** 对话框中以何种顺序显示它们。  
  
-   **筛选器**：根据 **“筛选设置”** 对话框中的列值筛选网格中的行。  
  
-   **清除筛选器**：清除网格的任何筛选设置。  
  
 筛选设置是特定于每个网格的。 列的选择和排序应用于同一类型的所有网格，如每个发布服务器的发布网格。  
  
 **“状态”**  
 快照代理的状态。 下面列出了可能的状态值：  
  
-   错误  
  
-   正在重试失败的命令  
  
-   未运行  
  
-   已完成  
  
 **代理**  
 快照代理。 这是与快照发布关联的唯一代理。 分发代理与此发布的订阅关联。 有关详细信息，请参阅[为与订阅关联的代理查看信息和执行任务（复制监视器）](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
 **上次启动时间**  
 代理上次启动的时间。  
  
 **Duration**  
 代理已运行的时间。 如果代理当前正在运行，该时间表示已用时间；如果代理已在之前运行完毕，则该时间表示总时间。  
  
 **上一操作**  
 在此代理最近一次运行的过程中最后执行的操作。  
  
## <a name="see-also"></a>另请参阅  
 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [查看发布的信息和执行其任务（复制监视器）](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [查看与发布关联的代理的信息和执行其任务（复制监视器）](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [监视复制](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
