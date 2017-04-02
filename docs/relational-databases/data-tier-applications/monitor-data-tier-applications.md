---
title: "监视数据层应用程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-data-tier-apps"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "监视 [SQL Server], 数据层应用程序"
  - "监视服务器性能 [SQL Server], DAC"
  - "数据层应用程序 [SQL Server], 监视"
ms.assetid: d2765828-2385-4019-aef2-1de3ab7d1b26
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# 监视数据层应用程序
  可以从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中的**实用工具资源管理器**和**对象资源管理器**以及系统视图和表中监视数据层应用程序 (DAC)。 此外，可以使用标准数据库和[!INCLUDE[ssDE](../../includes/ssde-md.md)]监视技术监视 DAC 中包含的数据库中的所有对象。  
  
## 开始之前  
 如果您将 DAC 部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的托管实例，在下次将实用工具收集组从该实例发送到实用工具控制点时，与部署的 DAC 有关的信息将合并到 SQL Server 实用工具中。 然后，您可以通过使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **实用工具资源管理器**，查看与该 DAC 有关的基本运行状况信息。  
  
 SSMS **“对象资源管理器”** 显示与部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的每个 DAC 有关的基本配置信息，而与该实例是否在 SQL Server 实用工具中进行管理无关。 此外，可以使用与用于监视任何数据库的相同过程来监视与部署的 DAC 相关联的数据库。  
  
## 使用 SQL Server 实用工具  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **实用工具资源管理器**中的“已部署的数据层应用程序”详细信息页显示一个仪表板，该仪表板报告已部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的托管实例的所有 DAC 的资源利用率。 该详细信息页的顶部窗格列出每个已部署的 DAC，同时还列出直观的指示器，显示 CPU 和文件资源的使用率是否超出为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具定义的策略。 如果您在列表视图中选择任何 DAC，则进一步的详细信息将显示在该页面的底部窗格的选项卡中。 有关详细信息页上提供的信息的详细信息，请参阅[已部署的数据层应用程序详细信息（SQL Server 实用工具）](../Topic/Deployed%20Data-tier%20Application%20Details%20\(SQL%20Server%20Utility\).md)。  
  
 在使用“已部署的数据层应用程序”详细信息页迅速确定导致硬件资源利用不足或压力过大的 DAC 后，你可以制订计划以便解决任何问题。 未充分利用其当前硬件资源的多个 DAC 可被合并为单个服务器，从而释放某些服务器以用于其他用途。 如果某一 DAC 对其当前服务器上的资源压力过大，则可以将该 DAC 移到性能更高的服务器上，或者向当前服务器添加更多的资源。  
  
 针对资源利用率的最低和最高限制由在 **“实用工具管理”** 详细信息页中定义的应用程序监视策略定义。 数据库管理员可以对策略进行定制，以便匹配其组织建立的限制。 例如，一个公司可以将 75% 设置为针对某一 DAC 的最高 CPU 利用率，而另一个公司可以将该最高值设置为 80%。 有关设置应用程序监视策略的详细信息，请参阅[实用工具管理（SQL Server 实用工具）](../Topic/Utility%20Administration%20\(SQL%20Server%20Utility\).md)。  
  
 查看“已部署的数据层应用程序”详细信息页：  
  
1.  选择“视图/实用工具资源管理器”菜单。  
  
2.  将“实用工具资源管理器”连接到实用工具控制点 (UCP)。  
  
3.  选择“视图/实用工具资源管理器详细信息”菜单。  
  
4.  在“实用工具资源管理器”中选择“已部署的数据层应用程序”节点。  
  
 “已部署的数据层应用程序”详细信息页中的信息来自实用工具管理数据仓库中的数据，实用工具管理数据仓库默认为每 15 分钟收集数据。 还可以使用 **“实用工具管理”** 详细信息页定制该间隔。  
  
## 使用对象资源管理器  
 SSMS **“对象资源管理器”** 显示与部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的每个 DAC 有关的基本配置信息。 这包括已在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中注册的托管实例，以及无法在“实用工具资源管理器”中查看的独立实例。  
  
 查看与部署到[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的 DAC 有关的详细信息：  
  
1.  选择“视图/对象资源管理器”菜单。  
  
2.  从对象资源管理器窗格连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
3.  选择“视图/对象资源管理器详细信息”菜单。  
  
4.  在“对象资源管理器”中选择映射到该实例的服务器节点，然后导航到“管理\数据层应用程序”节点。  
  
5.  详细信息页的顶部窗格中的列表视图列出部署到[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的每个 DAC。 在页面的底部选择要在详细信息窗格中显示信息的 DAC。  
  
 “数据层应用程序”节点的右键单击菜单还用于部署新的 DAC 或者删除现有 DAC。  
  
## 使用 DAC 系统视图和表  
 msdb.dbo.sysdac_history_internal 系统表记录对[!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例执行的所有 DAC 管理操作是成功还是失败。 该表记录发生每个操作的时间，以及执行了操作的登录名。 有关详细信息，请参阅 [sysdac_history_internal (Transact-SQL)](../Topic/sysdac_history_internal%20\(Transact-SQL\).md)。  
  
 DAC 系统视图报告基本的目录信息。 有关详细信息，请参阅[数据层应用程序视图 (Transact-SQL)](../Topic/Data-tier%20Application%20Views%20\(Transact-SQL\).md)。  
  
## 监视 DAC 数据库  
 在已成功部署某一 DAC 后，在该 DAC 中包含的数据库将像任何其他数据库一样操作。 使用标准[!INCLUDE[ssDE](../../includes/ssde-md.md)]技术和工具来监视数据库的性能、日志、事件和资源利用率。  
  
## 另请参阅  
 [数据层应用程序](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [部署数据层应用程序](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)  
  
  