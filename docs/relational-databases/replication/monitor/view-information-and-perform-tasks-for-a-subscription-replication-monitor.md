---
title: "查看订阅信息和执行其任务（复制监视器） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "订阅 [SQL Server 复制], 查看信息"
  - "订阅 [SQL Server 复制], 复制监视器任务"
  - "查看订阅信息"
ms.assetid: 54aac83b-6f29-40d7-8901-cf059749867f
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 查看订阅信息和执行其任务（复制监视器）
  复制监视器提供下列包含订阅相关信息的选项卡：  
  
-   **所有订阅**  
  
     此选项卡显示有关所选发布的所有订阅的信息。  
  
-   **订阅监视列表**  
  
     此选项卡用于显示所选发布服务器上所有可用发布的订阅的信息：有错误、出现警告或性能最差。 对于运行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]以前版本的分发服务器，不显示此选项卡。  
  
 有关每个选项卡上各选项的详细信息，请在右窗格中单击相应选项卡，然后在菜单栏上单击 **“帮助”** 。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### 在“所有订阅”选项卡中查看订阅信息和执行订阅任务  
  
1.  在左窗格中展开发布服务器组，再展开其中的一个发布服务器，然后单击其中的一个发布。  
  
2.  若要查看有关订阅的信息，请单击 **“所有订阅”** 选项卡。 若要查看仅这些订阅中某一给定的状态，例如同步时，选择从一个选项 **显示** 下拉列表。  
  
3.  要查看和修改订阅属性，右键单击该订阅，然后单击 **属性**。 您还可以通过该选项卡访问更详细的信息和执行任务。 有关详细信息，请参阅 [查看信息并执行任务的代理与订阅相关 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
### 在“订阅监视列表”选项卡中查看订阅信息和执行订阅任务  
  
1.  在左窗格中，展开发布服务器组，然后单击一个发布服务器。  
  
2.  若要查看有关订阅的信息，请单击 **“订阅监视列表”** 选项卡。  
  
3.  选择要显示的订阅类型 **显示 \< SubscriptionType> 订阅** 下拉列表。 若要查看仅这些订阅中某一给定的状态，例如同步时，选择从一个选项 **显示** 下拉列表。  
  
4.  要查看和修改订阅属性，右键单击该订阅，然后单击 **属性**。 您还可以通过该选项卡访问更详细的信息和执行任务。 有关详细信息，请参阅 [查看信息并执行任务的代理与订阅相关 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
## 另请参阅  
 [查看和修改推送订阅属性](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [查看和修改请求订阅属性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [监视复制](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  