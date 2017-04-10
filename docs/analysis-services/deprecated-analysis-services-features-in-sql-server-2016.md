---
title: "SQL Server 2016 中不推荐使用的 Analysis Services 功能 | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services 向后兼容性"
  - "SSAS, 向后兼容性"
  - "SQL Server Analysis Services, 向后兼容性"
  - "不推荐使用的功能 [Analysis Services]"
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
caps.latest.revision: 52
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 52
---
# SQL Server 2016 中不推荐使用的 Analysis Services 功能
  *不推荐使用的功能* 是指将从未来版本的产品中删除、但在当前版本中仍受支持并提供以保持向后兼容性的功能。 一般情况下，主版本会删除不推荐使用的功能，通常是在原始公告的两个版本内提供。 例如， [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 很可能不支持 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]中公布不推荐使用的功能。  
  
 **SQL Server 的下一个主版本中不支持的功能**  
  
|||  
|-|-|  
|**类别**|**功能**|  
|多维|远程分区|  
|多维|远程链接的度量值组|  
|多维|维度写回|  
|多维|链接的维度|  
  
 **SQL Server 未来版本中不支持的功能**  
  
|||  
|-|-|  
|**类别**|**功能**|  
|多维|主动缓存的 SQL Server 表通知。  <br />替代功能将对主动缓存使用轮询。 <br />请参阅[主动缓存（维度）](../analysis-services/multidimensional-models-olap-logical-dimension-objects/proactive-caching-dimensions.md)和[主动缓存（分区）](../Topic/Proactive%20Caching%20\(Partitions\).md)。|  
|多维|会话多维数据集。 没有替代功能。|  
|多维|本地多维数据集。 没有替代功能。|  
|表格|未来版本中将不支持表格模型 1100 和 1103 兼容性级别。 替代功能设置兼容性级别 1200 的模型，将模型定义转换为表格元数据。 请参阅 [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。|  
|工具|SQL Server Profiler for Trace Capture<br /><br /> 替代功能使用 SQL Server Management Studio 中嵌入的扩展事件探查器。  <br /> 请参阅 [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)。|  
|工具|跟踪重播 <br />替代功能的 Server Profiler。 没有替代功能。|  
|跟踪管理对象和跟踪 API|Microsoft.AnalysisServices.Trace 对象（包含 Analysis Services 跟踪和重播对象的 API）。 替代功能由多个部分组成：<br /><br /> -   跟踪配置：Microsoft.SqlServer.Management.XEvent<br />-   跟踪读取：Microsoft.SqlServer.XEvent.Linq<br />-   跟踪重播：无|  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中以前弃用的功能公告仍然有效。 由于尚未从本产品中删除支持这些功能的代码，因此该版本中仍存在其中的许多功能。 虽然可以访问以前弃用的功能，但这些功能仍视为已弃用， [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 发行期间可能会将它们从本产品中删除。 在基于 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]的任何新模型或应用程序中，强烈建议你避免使用已弃用的功能。  
  
## 另请参阅  
 [Analysis Services 向后兼容性](../analysis-services/analysis-services-backward-compatibility.md)   
 [SQL Server 2016 中废弃的 Analysis Services 功能](../analysis-services/discontinued-analysis-services-functionality-in-sql-server-2016.md)  
  
  