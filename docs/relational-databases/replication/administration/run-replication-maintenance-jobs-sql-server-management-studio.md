---
title: "执行复制维护作业 (SQL Server Management Studio) | Microsoft Docs"
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
  - "作业 [SQL Server 复制]"
ms.assetid: 0dc485a0-5a50-41eb-a29d-f2b2fb920174
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 执行复制维护作业 (SQL Server Management Studio)
  复制使用下列维护作业：  
  
-   **重新初始化数据验证失败的订阅**  
  
-   **代理历史记录清除：分发**  
  
-   **分发的复制监视刷新器。**  
  
-   **复制代理检查**  
  
-   **分发清除：分发**  
  
-   **过期订阅清除**  
  
 从  的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 文件夹和复制监视器的 **“代理”** 选项卡中启动和停止这些作业。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。 查看和修改属性中每个作业 **作业属性-\< 作业>** 对话框中，也可以从相同的文件夹和选项卡。  
  
### 在 Management Studio 中启动或停止复制维护作业  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到分发服务器，然后展开服务器节点。  
  
2.  展开 **“SQL Server 代理”** 文件夹，再展开 **“作业”** 文件夹。  
  
3.  右键单击一个作业，然后单击 **作业开始** 或 **停止作业**。  
  
### 在复制监视器中启动或停止复制维护作业  
  
1.  在复制监视器中，展开发布服务器组，然后选择一个发布服务器。  
  
2.  单击 **“代理”** 选项卡。  
  
3.  右键单击在网格中，一个作业，然后单击 **作业开始** 或 **停止作业**。  
  
### 在 Management Studio 中查看和修改复制维护作业的属性  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到分发服务器，然后展开服务器节点。  
  
2.  展开 **“SQL Server 代理”** 文件夹，再展开 **“作业”** 文件夹。  
  
3.  右键单击一个作业，然后单击 **属性**。  
  
4.  在 **作业属性-\< 作业>** 对话框中，修改任何属性，如有必要，，然后单击 **确定**。  
  
### 在复制监视器中查看和修改复制维护作业的属性  
  
1.  在复制监视器中，展开发布服务器组，然后选择一个发布服务器。  
  
2.  单击 **“代理”** 选项卡。  
  
3.  右键单击在网格中，一个作业，然后单击 **属性**。  
  
4.  在 **作业属性-\< 作业>** 对话框中，修改任何属性，如有必要，，然后单击 **确定**。  
  
## 另请参阅  
 [启动和停止复制代理 & #40;SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [查看信息并为发布服务器和 #40; 执行任务复制监视器 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [复制代理管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  