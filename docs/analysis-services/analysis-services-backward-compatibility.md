---
title: SQL Server 2016 Analysis Services 向后兼容性 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ab4f304d865992a3269b4ee83c9e25f61069e8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210262"
---
# <a name="analysis-services-backward-compatibility-sql-server-2016"></a>Analysis Services 向后兼容性 (SQL Server 2016)
[!INCLUDE[ssas-appliesto-sql2016](../includes/ssas-appliesto-sql2016.md)]

本文描述了中功能可用性和当前版本和以前的版本之间行为的更改。

## <a name="deprecated-features"></a>已弃用的功能
一个*弃用的功能*将停用从产品中未来版本中，但仍支持并包含在当前版本，以保持向后兼容性。 建议您停止使用新的和现有项目中已弃用的功能以保持与将来的版本兼容。
  
在此版本中已弃用以下功能：
  
|||  
|-|-|  
|**模式/类别**|**功能**|  
|多维|远程分区|  
|多维|远程链接的度量值组|  
|多维|维度写回|  
|多维|链接的维度|   
|多维|主动缓存的 SQL Server 表通知。  <br />替代功能将对主动缓存使用轮询。 <br />请参阅[主动缓存（维度）](../analysis-services/multidimensional-models-olap-logical-dimension-objects/proactive-caching-dimensions.md)和[主动缓存（分区）](../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。|  
|多维|会话多维数据集。 没有替代功能。|  
|多维|本地多维数据集。 没有替代功能。|  
|表格|未来版本中将不支持表格模型 1100 和 1103 兼容性级别。 替换是将模型设置兼容级别 1200年或更高版本，将模型定义转换为表格元数据。 请参阅 [Analysis Services 中表格模型的兼容级别](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。|  
|工具|SQL Server Profiler for Trace Capture<br /><br /> 替代功能使用 SQL Server Management Studio 中嵌入的扩展事件探查器。  <br /> 请参阅 [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)。|  
|工具|跟踪重播 <br />替代功能的 Server Profiler。 没有替代功能。|  
|跟踪管理对象和跟踪 API|Microsoft.AnalysisServices.Trace 对象（包含 Analysis Services 跟踪和重播对象的 API）。 替代功能由多个部分组成：<br /><br /> -跟踪配置：Microsoft.SqlServer.Management.XEvent<br />-跟踪读取：Microsoft.SqlServer.XEvent.Linq<br />-跟踪重播：无|  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中以前弃用的功能公告仍然有效。 由于尚未从本产品中删除支持这些功能的代码，因此该版本中仍存在其中的许多功能。 在以前已弃用的功能时可能是可访问，它们仍被视为已弃用，并且可能以物理方式从产品中删除在任何时间。  

## <a name="discontinued-features"></a>废弃的功能
一个*停用功能*在早期版本中已弃用。 它包含在当前版本中，可以继续但不再受支持。 废弃的功能可能会删除完全在以后发布或更新。

以下功能在早期版本中已弃用，不再支持此版本中。

|||  
|-|-|  
|**功能**|**替代功能或解决方法**|  
|[CalculationPassValue (MDX)](../mdx/calculationpassvalue-mdx.md)|无。 SQL Server 2005 中已弃用此功能。|  
|[CalculationCurrentPass (MDX)](../mdx/calculationcurrentpass-mdx.md)|无。 SQL Server 2005 中已弃用此功能。|  
|NON_EMPTY_BEHAVIOR 查询优化器提示|无。 SQL Server 2008 中已弃用此功能。|  
|COM 程序集|无。 SQL Server 2008 中已弃用此功能。|  
|CELL_EVALUATION_LIST 内部单元属性|无。 SQL Server 2005 中已弃用此功能。|  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中以前弃用的功能公告仍然有效。 由于尚未从本产品中删除支持这些功能的代码，因此该版本中仍存在其中的许多功能。 在以前已弃用的功能时可能是可访问，它们仍被视为已弃用，并且可能以物理方式从产品中删除在任何时间。  

## <a name="breaking-changes"></a>重大更改
*重大更改* 导致数据模型、应用程序代码或脚本在模型或服务器升级后不再工作。
  
### <a name="net-40-version-upgrade"></a>.NET 4.0 版本升级  
 Analysis Services 管理对象 (AMO)、 ADOMD.NET 和表格对象模型 (TOM) 客户端库现在面向.NET 4.0 运行时。 这可能是对指向 .NET 3.5 的应用程序的重大更改。 使用这些程序集的较新版本的应用程序现在必须指向.NET 4.0 或更高版本。  
  
### <a name="amo-version-upgrade"></a>AMO 版本升级  
 此版本是版本升级[Analysis Services 管理对象&#40;AMO&#41; ](https://msdn.microsoft.com/library/mt436122.aspx)在某些情况下属于重大更改。  调入 AMO 的现有代码和脚本将继续运行，和从以前的版本升级之前一样。 但是，如果你需要*重新编译*你的应用程序为目标的 SQL Server 2016 Analysis Services 实例，则必须添加以下命名空间才能使代码或脚本正常运行：  
  
```  
  
using Microsoft.AnalysisServices;  
using Microsoft.AnalysisServices.Core;  
  
```  
  
 现在，无论何时在你的代码中引用 Microsoft.AnalysisServices 程序集，都需要 [Microsoft.AnalysisServices.Core](https://msdn.microsoft.com/library/microsoft.analysisservices.core.aspx) 命名空间。 对于以前只能在 **Microsoft.AnalysisServices** 命名空间中的对象，如果它们在表格和多维方案中使用的方式相同，则在此版本中会移到核心命名空间。  例如，服务器相关的 API 将重新安置到核心命名空间中。  
  
 尽管现在有多个命名空间，但它们都在同一程序集 (Microsoft.AnalysisServices.dll) 中。  
  
### <a name="xevent-discover-changes"></a>XEvent DISCOVER 更改  
 若要更好地支持的 XEvent DISCOVER 流在 SSMS 中的 SQL Server 2016 Analysis Services，`DISCOVER_XEVENT_TRACE_DEFINITION`将替换为以下 XEvent 跟踪：  
  
-   DISCOVER_XEVENT_PACKAGES  
  
-   DISCOVER_XEVENT_OBJECT  
  
-   DISCOVER_XEVENT_OBJECT_COLUMNS  
  
-   DISCOVER_XEVENT_SESSION_TARGETS  

## <a name="behavior-changes"></a>行为更改
与早期版本的 SQL Server 相比，当前版本中功能的操作或交互方式会受到 *行为更改* 的影响。
  
产品中行为更改的示例包括对默认值、完成升级或还原功能所需的手动配置或现有功能的新实现的修订。
  
此处列出了在此版本中更改的功能行为，这些功能虽已更改但尚不会中断现有模型或代码后期升级。
  
### <a name="analysis-services-in-sharepoint-mode"></a>SharePoint 模式下的 Analysis Services
 不再需要运行 PowerPivot 配置向导这一安装后任务。 这适用于所有受支持版本的 SharePoint，从当前的 SQL Server 2016 Analysis Services 中加载模型。
  
### <a name="directquery-mode-for-tabular-models"></a>表格模型中的 DirectQuery 模式
 *DirectQuery* 是表格模型的数据访问模式，在此模式下，查询执行将在后端相关数据库上执行，实时检索结果集。 它通常用于无法存储在内存中的大型数据集，或者常用在当数据不稳定并想在查询中返回针对表格模型的最新数据时。
  
 DirectQuery 在最近的几个版本中作为数据访问模式存在。 在 SQL Server 2016 Analysis Services 中实现具有已稍微有所更改，假定表格模型位于兼容性级别为 1200年或更高版本。 DirectQuery 的限制比之前更少。 它还具有不同的数据库属性。
  
 如果在现有的表格模型中使用 DirectQuery，则可以在当前的兼容级别 1100 或 1103 上保留该模型并继续使用 DirectQuery 作为其对这两种级别的实现。 或者，你可以升级到 1200年或更高版本才能受益于针对 DirectQuery 所做的增强功能。
  
 从较旧的兼容性级别设置的较新的 1200年及更高版本的兼容性级别中没有完全对应在于 DirectQuery 模型无就地升级。 如果必须在 DirectQuery 模式下运行的现有表格模型，您应在 SQL Server Data Tools 中打开模型，关闭 DirectQuery，设置**兼容性级别**属性设为 1200年或更高版本，以及然后重新配置 DirectQuery属性。 请参阅[DirectQuery 模式下](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)有关详细信息。


## <a name="see-also"></a>请参阅
[Analysis Services 向后兼容性 (SQL Server 2017)](analysis-services-backward-compatibility-sql2017.md)
