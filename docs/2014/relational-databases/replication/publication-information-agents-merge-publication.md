---
title: 发布信息，代理（合并发布）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.downlevelagents.merge.f1
ms.assetid: 73ff590a-20da-4f10-b592-c60b7226d22b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a3f6a4f3e96e3dc73ffca93393359a3cd40654a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095227"
---
# <a name="publication-information-agents-merge-publication"></a>发布信息，代理（合并发布）
  **“代理”** 选项卡显示所选发布的快照代理的摘要信息。  
  
## <a name="options"></a>选项  
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
 快照代理。 这是与合并发布关联的唯一代理。 合并代理与此发布的订阅关联。 有关详细信息，请参阅[查看与订阅关联的代理的信息和执行其任务（复制监视器）](monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
 **上次启动时间**  
 代理上次启动的时间。  
  
 **Duration**  
 代理已运行的时间。 如果代理当前正在运行，该时间表示已用时间；如果代理已在之前运行完毕，则该时间表示总时间。  
  
 **上一操作**  
 在此代理最近一次运行的过程中最后执行的操作。  
  
## <a name="see-also"></a>请参阅  
 [启动复制监视器](monitor/start-the-replication-monitor.md)   
 [查看发布的信息和执行其任务（复制监视器）](monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [查看与发布关联的代理的信息和执行其任务（复制监视器）](monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [监视复制](monitoring-replication.md)  
  
  
