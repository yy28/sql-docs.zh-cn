---
title: "监视数据层应用程序 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: data-tier-applications
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- monitoring [SQL Server], data-tier applications
- monitoring server performance [SQL Server], DACs
- data-tier application [SQL Server], monitor
ms.assetid: d2765828-2385-4019-aef2-1de3ab7d1b26
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a8bfc10f588c868693eb0d24308730a618db9df7
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2018
---
# <a name="monitor-data-tier-applications"></a>监视数据层应用程序
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 可以从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中的实用工具资源管理器和对象资源管理器以及系统视图和表中监视数据层应用程序 (DAC)。 此外，可以使用标准数据库和 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 监视技术监视 DAC 中包含的数据库中的所有对象。  
  
## <a name="before-you-begin"></a>开始之前  
 如果您将 DAC 部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的托管实例，在下次将实用工具收集组从该实例发送到实用工具控制点时，与部署的 DAC 有关的信息将合并到 SQL Server 实用工具中。 然后，您可以通过使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **实用工具资源管理器**，查看与该 DAC 有关的基本运行状况信息。  
  
 SSMS **“对象资源管理器”** 显示与部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的每个 DAC 有关的基本配置信息，而与该实例是否在 SQL Server 实用工具中进行管理无关。 此外，可以使用与用于监视任何数据库的相同过程来监视与部署的 DAC 相关联的数据库。  
  
## <a name="using-the-sql-server-utility"></a>使用 SQL Server 实用工具  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **实用工具资源管理器**中的“已部署的数据层应用程序”详细信息页显示一个面板，该面板报告已部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的托管实例的所有 DAC 的资源利用情况。 该详细信息页的顶部窗格列出每个已部署的 DAC，同时还列出直观的指示器，显示 CPU 和文件资源的使用率是否超出为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具定义的策略。 如果您在列表视图中选择任何 DAC，则进一步的详细信息将显示在该页面的底部窗格的选项卡中。 有关详细信息页上提供的信息的详细信息，请参阅[已部署的数据层应用程序详细信息（SQL Server 实用工具）](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)。  
  
 在使用“已部署的数据层应用程序”详细信息页迅速确定导致硬件资源利用不足或压力过大的 DAC 后，你可以制订计划以便解决任何问题。 未充分利用其当前硬件资源的多个 DAC 可被合并为单个服务器，从而释放某些服务器以用于其他用途。 如果某一 DAC 对其当前服务器上的资源压力过大，则可以将该 DAC 移到性能更高的服务器上，或者向当前服务器添加更多的资源。  
  
 针对资源利用率的最低和最高限制由在 **“实用工具管理”** 详细信息页中定义的应用程序监视策略定义。 数据库管理员可以对策略进行定制，以便匹配其组织建立的限制。 例如，一个公司可以将 75% 设置为针对某一 DAC 的最高 CPU 利用率，而另一个公司可以将该最高值设置为 80%。 有关设置应用程序监视策略的详细信息，请参阅[实用工具管理（SQL Server 实用工具）](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)。  
  
 查看“已部署的数据层应用程序”详细信息页：  
  
1.  选择“视图/实用工具资源管理器”菜单。  
  
2.  将“实用工具资源管理器”连接到实用工具控制点 (UCP)。  
  
3.  选择“视图/实用工具资源管理器详细信息”菜单。  
  
4.  在“实用工具资源管理器”中选择“已部署的数据层应用程序”节点。  
  
 “已部署的数据层应用程序”详细信息页中的信息来自实用工具管理数据仓库中的数据，实用工具管理数据仓库默认为每 15 分钟收集数据。 还可以使用 **“实用工具管理”** 详细信息页定制该间隔。  
  
## <a name="using-object-explorer"></a>使用对象资源管理器  
 SSMS **“对象资源管理器”** 显示与部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的每个 DAC 有关的基本配置信息。 这包括已在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中注册的托管实例，以及无法在“实用工具资源管理器”中查看的独立实例。  
  
 查看与部署到[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的 DAC 有关的详细信息：  
  
1.  选择“视图/对象资源管理器”菜单。  
  
2.  从对象资源管理器窗格连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
3.  选择“视图/对象资源管理器详细信息”菜单。  
  
4.  在“对象资源管理器”中选择映射到该实例的服务器节点，然后导航到“管理\数据层应用程序”节点。  
  
5.  详细信息页的顶部窗格中的列表视图列出部署到[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的每个 DAC。 在页面的底部选择要在详细信息窗格中显示信息的 DAC。  
  
 “数据层应用程序”节点的右键单击菜单还用于部署新的 DAC 或者删除现有 DAC。  
  
## <a name="using-the-dac-system-views-and-tables"></a>使用 DAC 系统视图和表  
 msdb.dbo.sysdac_history_internal 系统表记录对 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例执行的所有 DAC 管理操作是成功还是失败。 该表记录发生每个操作的时间，以及执行了操作的登录名。 有关详细信息，请参阅 [sysdac_history_internal (Transact-SQL)](../../relational-databases/system-tables/data-tier-application-tables-sysdac-history-internal.md)。  
  
 DAC 系统视图报告基本的目录信息。 有关详细信息，请参阅[数据层应用程序视图 (Transact-SQL)](http://msdn.microsoft.com/library/0de01328-d7a6-4677-b7a0-dcd3098c23d4)。  
  
## <a name="monitoring-dac-databases"></a>监视 DAC 数据库  
 在已成功部署某一 DAC 后，在该 DAC 中包含的数据库将像任何其他数据库一样操作。 使用标准 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 技术和工具来监视数据库的性能、日志、事件和资源利用率。  
  
## <a name="see-also"></a>另请参阅  
 [数据层应用程序](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [部署数据层应用程序](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)  
  
  
