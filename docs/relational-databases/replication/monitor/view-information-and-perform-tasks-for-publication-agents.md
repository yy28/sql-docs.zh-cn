---
title: "查看发布代理的信息和执行其任务 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- agents [SQL Server replication], viewing information
- viewing replication agent information
- agents [SQL Server replication], tasks in Replication Monitor
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3d2896e84ecfba28325f559da8e9391315c21046
ms.lasthandoff: 04/11/2017

---
# <a name="view-information-and-perform-tasks-for-publication-agents"></a>查看发布代理的信息和执行其任务
  复制监视器提供了 **“代理”** 选项卡，其中包含与所选发布关联的代理的相关信息。 分发代理和合并代理均与订阅相关联；有关详细信息，请参阅[查看与订阅关联的代理的信息和执行其任务（复制监视器）](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
 此选项卡显示有关下列代理的信息：  
  
-   快照代理，用于所有发布。  
  
-   日志读取器代理，用于所有事务发布。  
  
-   队列读取器代理，用于为排队更新订阅启用的事务发布。  
  
 若要查看有关此选项卡上的选项的详细信息，请在菜单栏上单击 **“帮助”** 。 有关启动复制监视器的信息，请参阅[启动复制监视器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-the-agents-associated-with-a-publication"></a>查看与发布相关的代理的信息并执行此代理的任务  
  
1.  在左窗格中展开发布服务器组，再展开其中的一个发布服务器，然后单击其中的一个发布。  
  
2.  单击 **“代理”** 选项卡来查看有关代理的信息。 您还可以通过此选项卡访问更详细的信息并执行任务：  
  
    -   若要查看有关代理的详细信息（如信息性消息以及任何错误消息），请右键单击代理，然后单击 **“查看详细信息”**。  
  
    -   若要查看有关运行代理的作业的详细信息（如计划、作业步骤详细信息等等），请右键单击代理，然后单击 **“属性”**。  
  
    -   若要管理代理的配置文件，请右键单击代理，然后单击 **“代理配置文件”**。 有关详细信息，请参阅[处理复制代理配置文件](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)。  
  
    -   若要启动未运行的代理，请右键单击代理，然后单击 **“启动代理”**。  
  
    -   若要停止运行中的代理，请右键单击代理，然后单击 **“停止代理”**。  
  
## <a name="see-also"></a>另请参阅  
 [在复制监视器中设置阈值和警告](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)   
 [查看发布的信息和执行其任务（复制监视器）](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [复制代理管理](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [监视复制](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
