---
title: "查看发布服务器的信息和执行其任务（复制监视器） | Microsoft Docs"
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
  - "发布服务器 [SQL Server 复制], 复制监视器任务"
  - "查看发布服务器的信息"
  - "发布服务器 [SQL Server 复制], 查看信息"
ms.assetid: 1e777e95-377a-4de3-b965-867464aadaaf
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 查看发布服务器的信息和执行其任务（复制监视器）
  复制监视器提供了下列选项卡，以显示有关选定发布服务器的信息：  
  
-   **发布**  
  
     此选项卡显示选定发布服务器上所有发布的相关信息。  
  
-   **订阅监视列表**  
  
     此选项卡用于显示所选发布服务器上所有可用发布的订阅的信息：有错误、出现警告或性能最差。 对于运行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]以前版本的分发服务器，不显示此选项卡。  
  
-   **“代理”** 选项卡  
  
     此选项卡显示所有类型的复制所使用的代理和作业的详细信息。 使用该选项卡，还可以启动和停止每个代理和作业。  
  
 若要查看每个选项卡上各个选项的详细信息，请在右窗格中单击该选项卡，再单击菜单栏上的 **“帮助”** 。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### 查看发布服务器的信息和执行其任务  
  
1.  在左窗格中，展开发布服务器组，然后单击一个发布服务器。  
  
2.  若要查看所有发布的信息，请单击 **“发布”** 选项卡。  
  
3.  若要查看有关订阅的信息，请单击 **“订阅监视列表”** 选项卡。 还可以从此访问更详细的信息以及执行任务：  
  
    -   要查看有关与订阅关联的代理的详细的信息，请右键单击该订阅，然后单击 **查看详细信息**。  
  
    -   要查看订阅的属性，右键单击该订阅，然后单击 **属性**。  
  
    -   要同步推送订阅，请右键单击该订阅，然后单击 **开始同步**。  
  
    -   要重新初始化订阅，请右键单击该订阅，然后单击 **重新初始化订阅**。  
  
4.  若要查看有关代理的信息，请单击 **“代理”** 选项卡。 您还可以通过此选项卡访问更详细的信息并执行任务：  
  
    -   若要查看详细的信息 （如信息性消息和任何错误消息） 代理，右键单击代理，，然后单击 **查看详细信息**。  
  
    -   要查看有关运行 （如计划、 作业步骤的详细信息等） 的代理的作业的详细的信息，请右键单击代理，，然后单击 **属性**。  
  
    -   要管理的代理配置文件，用鼠标右键单击该代理，然后单击 **代理配置文件**。 有关详细信息，请参阅 [使用复制代理配置文件](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)。  
  
    -   要启动未运行的代理，请右键单击代理，，然后单击 **启动代理**。  
  
    -   要停止正在运行的代理，请右键单击代理，，然后单击 **停止代理**。  
  
## 另请参阅  
 [查看和修改分发服务器和发布服务器属性](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [监视复制](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  