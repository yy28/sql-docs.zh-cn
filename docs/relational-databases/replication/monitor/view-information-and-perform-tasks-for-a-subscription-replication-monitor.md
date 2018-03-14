---
title: "查看订阅的信息和执行其任务（复制监视器）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication], viewing information
- subscriptions [SQL Server replication], Replication Monitor tasks
- viewing subscription information
ms.assetid: 54aac83b-6f29-40d7-8901-cf059749867f
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e860780f284c6d7315045e9fd3bd04a7a4a83b8
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="view-information-and-perform-tasks-for-a-subscription-replication-monitor"></a>查看订阅信息和执行其任务（复制监视器）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  复制监视器提供下列包含订阅相关信息的选项卡：  
  
-   **所有订阅**  
  
     此选项卡显示有关所选发布的所有订阅的信息。  
  
-   **订阅监视列表**  
  
     此选项卡用于显示所选发布服务器上所有可用发布的订阅的信息：有错误、出现警告或性能最差。 对于运行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]以前版本的分发服务器，不显示此选项卡。  
  
 有关每个选项卡上各选项的详细信息，请在右窗格中单击相应选项卡，然后在菜单栏上单击 **“帮助”** 。 有关启动复制监视器的信息，请参阅[启动复制监视器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-all-subscriptions-tab"></a>在“所有订阅”选项卡中查看订阅信息和执行订阅任务  
  
1.  在左窗格中展开发布服务器组，再展开其中的一个发布服务器，然后单击其中的一个发布。  
  
2.  若要查看有关订阅的信息，请单击 **“所有订阅”** 选项卡。若要只查看处于给定状态（如同步）的订阅，请从 **“显示”** 下拉列表中选择一个选项。  
  
3.  若要查看和修改订阅属性，请右键单击该订阅，然后单击 **“属性”**。 您还可以通过该选项卡访问更详细的信息和执行任务。有关详细信息，请参阅[为与订阅关联的代理查看信息和执行任务（复制监视器）](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
### <a name="to-view-information-and-perform-tasks-for-subscriptions-in-the-subscription-watch-list-tab"></a>在“订阅监视列表”选项卡中查看订阅信息和执行订阅任务  
  
1.  在左窗格中，展开发布服务器组，然后单击一个发布服务器。  
  
2.  若要查看有关订阅的信息，请单击 **“订阅监视列表”** 选项卡。  
  
3.  从“显示 \<订阅类型> 订阅”下拉列表中选择要显示的订阅类型。 若要只查看处于给定状态（如同步）的订阅，请从 **“显示”** 下拉列表中选择一个选项。  
  
4.  若要查看和修改订阅属性，请右键单击该订阅，然后单击 **“属性”**。 您还可以通过该选项卡访问更详细的信息和执行任务。有关详细信息，请参阅[为与订阅关联的代理查看信息和执行任务（复制监视器）](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改推送订阅属性](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [查看和修改请求订阅属性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [监视复制](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
