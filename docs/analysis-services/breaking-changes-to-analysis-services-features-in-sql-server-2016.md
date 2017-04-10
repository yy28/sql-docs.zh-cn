---
title: "SQL Server 2016 中 Analysis Services 功能的重大更改 | Microsoft Docs"
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
helpviewer_keywords: 
  - "重大更改 [Analysis Services]"
  - "升级 Analysis Services"
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
caps.latest.revision: 55
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 53
---
# SQL Server 2016 中 Analysis Services 功能的重大更改
  *重大更改* 导致数据模型、应用程序代码或脚本在模型或服务器升级后不再工作。  
  
> [!NOTE]  
>  与此相反， *行为更改* 表现为代码更改，这不会中断模型或应用程序，但会引入与早期版本不同的行为。  例如，行为更改可能包括更改默认值，或不允许配置以前允许的属性或选项。 若要了解有关此版本中的行为更改的详细信息，请参阅 [Behavior Changes to Analysis Services Features in SQL Server 2016](../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)。  
  
## .NET 4.0 版本升级  
 Analysis Services 管理对象 (AMO)、ADOMD.NET 和 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 中的表格对象模型 (TOM) 中的客户端库现在指向 .NET 4.0 运行时。 这可能是对指向 .NET 3.5 的应用程序的重大更改。 使用这些程序集的较新版本的应用程序现在必须指向.NET 4.0 或更高版本。  
  
## AMO 版本升级  
 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 是 [Analysis Services 管理对象 (AMO)](../Topic/Analysis%20Services%20Management%20Objects%20\(AMO\).md) 的版本升级，在某些情况下属于重大更改。  调入 AMO 的现有代码和脚本将继续运行，和从以前的版本升级之前一样。 但是，如果你需要 *重新编译* 以 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 实例为目标的应用程序，必须添加以下命名空间才能使你的代码或脚本正常运行：  
  
```  
  
using Microsoft.AnalysisServices;  
using Microsoft.AnalysisServices.Core;  
  
```  
  
 现在，无论何时在你的代码中引用 Microsoft.AnalysisServices 程序集，都需要 [Microsoft.AnalysisServices.Core](../Topic/Microsoft.AnalysisServices.Core.md) 命名空间。 对于以前只能在 **Microsoft.AnalysisServices** 命名空间中的对象，如果它们在表格和多维方案中使用的方式相同，则在此版本中会移到核心命名空间。  例如，服务器相关的 API 将重新安置到核心命名空间中。  
  
 尽管现在有多个命名空间，但它们都在同一程序集 (Microsoft.AnalysisServices.dll) 中。  
  
## XEvent DISCOVER 更改  
 为了更好地支持 SSMS for [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]中的 XEvent DISCOVER 流，已将 `DISCOVER_XEVENT_TRACE_DEFINITION` 替换为以下 XEvent 跟踪：  
  
-   DISCOVER_XEVENT_PACKAGES  
  
-   DISCOVER_XEVENT_OBJECT  
  
-   DISCOVER_XEVENT_OBJECT_COLUMNS  
  
-   DISCOVER_XEVENT_SESSION_TARGETS  
  
## 另请参阅  
 [Analysis Services 向后兼容性](../analysis-services/analysis-services-backward-compatibility.md)  
  
  