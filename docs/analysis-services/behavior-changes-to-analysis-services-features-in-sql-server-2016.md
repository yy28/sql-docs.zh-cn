---
title: "SQL Server 2016 中 Analysis Services 功能的行为更改 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# SQL Server 2016 中 Analysis Services 功能的行为更改
  与早期版本的 SQL Server 相比，当前版本中功能的操作或交互方式会受到 *行为更改* 的影响。  
  
 产品中行为更改的示例包括对默认值、完成升级或还原功能所需的手动配置或现有功能的新实现的修订。  
  
 此处列出了在此版本中更改的功能行为，这些功能虽已更改但尚不会中断现有模型或代码后期升级。  
  
> [!NOTE]  
>  对比 *行为更改*， *中断更改* 将阻止与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 集成的数据模型或应用程序在升级某个服务器、客户端工具或模型之后运行。 若要查看该列表，请访问 [SQL Server 2016 中 Analysis Services 功能的重大更改](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md)。  
  
## SharePoint 模式下的 Analysis Services  
 不再需要运行 PowerPivot 配置向导这一安装后任务。 这适用于从 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的当前 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本加载模型的所有受支持的 SharePoint 版本。  
  
## 表格模型中的 DirectQuery 模式  
 *DirectQuery* 是表格模型的数据访问模式，在此模式下，查询执行将在后端相关数据库上执行，实时检索结果集。 它通常用于无法存储在内存中的大型数据集，或者常用在当数据不稳定并想在查询中返回针对表格模型的最新数据时。  
  
 DirectQuery 在最近的几个版本中作为数据访问模式存在。 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]中，该实现已稍微有所更改，假定表格模型位于兼容级别 1200。 DirectQuery 的限制比之前更少。 它还具有不同的数据库属性。  
  
 如果在现有的表格模型中使用 DirectQuery，则可以在当前的兼容级别 1100 或 1103 上保留该模型并继续使用 DirectQuery 作为其对这两种级别的实现。 或者，你可以升级到 1200，以从此版本的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中针对 DirectQuery 所做的增强功能获益。  
  
 由于较旧的兼容级别设置与较新的 1200 兼容级别并不完全对应，因此 DirectQuery 模型无法就地升级。 如果具有以 DirectQuery 模式运行的现有表格模型，则应在 SQL Server Data Tools 中打开该模型，关闭 DirectQuery，将  “兼容级别”属性设置为 1200，然后如定义表格 1200 模型一样，重新配置 DirectQuery 属性。 有关详细信息，请参阅 [DirectQuery 模式（SSAS 表格）](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)。  
  
## 另请参阅  
 [向后兼容性_已删除](../Topic/Backward%20Compatibility_deleted.md)   
 [SQL Server 2016 中 Analysis Services 功能的重大更改](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md)   
 [Analysis Services 中表格模型的兼容级别](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [下载 SQL Server Data Tools](https://msdn.microsoft.com/en-us/library/mt204009.aspx)  
  
  