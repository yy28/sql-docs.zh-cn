---
title: "查看资源运行状况策略结果（SQL Server 实用工具） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# 查看资源运行状况策略结果（SQL Server 实用工具）
  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的实用工具仪表板，可以查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]￼ 的托管实例和数据层应用程序的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具资源参数。 有关详细信息，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
##  <a name="SSMSProcedure"></a>  
  
#### 查看 SQL Server 实用工具的资源运行状况策略结果  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中，单击“视图”，然后单击“实用工具资源管理器”以便查看实用工具资源管理器导航窗格。 若要查看内容窗格，请单击 **“视图”**，然后单击 **“实用工具资源管理器内容”**。  
  
2.  在导航窗格中，单击 ![](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")“连接到实用工具”。 如果尚未创建实用工具控制点 (UCP)，或者尚未将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例或者数据层应用程序注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
3.  单击 UCP 节点可以查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例和数据层应用程序的摘要数据（右键单击可以刷新）。 面板数据将显示在内容窗格中。  
  
4.  单击“托管实例”节点可以查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例的列表视图数据（右键单击可以刷新）。 列表视图数据将显示在内容窗格中。  
  
5.  单击“已部署的数据层应用程序”节点可查看数据层应用程序的列表视图（右键单击可刷新）。 列表视图数据将显示在内容窗格中。  
  
## 另请参阅  
 [SQL Server 实用工具的功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)   
 [已部署的数据层应用程序详细信息（SQL Server 实用工具）](../Topic/Deployed%20Data-tier%20Application%20Details%20\(SQL%20Server%20Utility\).md)   
 [托管实例详细信息（SQL Server 实用工具）](../Topic/Managed%20Instance%20Details%20\(SQL%20Server%20Utility\).md)   
 [实用工具管理（SQL Server 实用工具）](../Topic/Utility%20Administration%20\(SQL%20Server%20Utility\).md)  
  
  