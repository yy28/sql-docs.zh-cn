---
title: Analysis Services 个性化扩展 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- personalization extensions [Multidimensional Databases]
ms.assetid: 0f144059-24e0-40c0-bde4-d48c75e46598
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9354e441f3b94205b1be055f48dcf4b279fc708a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125266"
---
# <a name="analysis-services-personalization-extensions"></a>Analysis Services 个性化设置扩展
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化扩展是了解实现插件体系结构的基础。 在插件体系结构中，您可以动态地开发新的多维数据集对象和功能，并可以与其他开发人员方便地共享。 在这种情况下，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]个性化设置扩展提供了使它能够实现以下功能：  
  
-   **动态设计和部署**立即后，你可以设计和部署[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]个性化扩展，用户在下一步的用户会话的开始处有权访问的对象和功能。  
  
-   **接口独立性**无论接口，用于创建[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]个性化扩展，用户可以使用任何接口访问的对象和功能。  
  
-   **会话上下文**[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]个性化扩展都不是永久对象中的现有基础结构，不需要重新处理该多维数据集。 在用户连接到数据库时，它们将公开并为该用户创建，并在整个用户会话期间保持可用。  
  
-   **快速分发**共享[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]个性化扩展与其他软件开发人员而无需进入有关在何处的详细的规范或如何查找此扩展的功能。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化设置扩展具有多种用途。 例如，您的公司的销售涉及到多种货币。 您可创建一个计算成员，以本地货币返回访问此多维数据集的人员的总销售额。 首先要此成员创建为个性化设置扩展。 然后，将此计算成员与一组用户共享。 共享后，这些用户将拥有立即访问计算成员，只要用户连接到服务器。 即使用户使用的接口不是用于创建该计算成员的接口，也可以访问该计算成员。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化扩展现有的托管程序集体系结构的简单又优雅修改并在整个公开[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]<xref:Microsoft.AnalysisServices.AdomdServer>对象模型、 多维表达式 (MDX) 语法和架构行集。  
  
## <a name="logical-architecture"></a>逻辑体系结构  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化设置扩展的体系结构以托管程序集体系结构以及以下四个基本元素为基础：  
  
 [PlugInAttribute] 自定义属性  
 启动服务时,[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]加载所需的程序集，并确定哪些类具有<xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute>自定义属性。  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 将定义自定义属性作为描述代码及影响运行时行为的方式。 有关详细信息，请参阅主题中，"[的特性概述](http://go.microsoft.com/fwlink/?LinkId=82929)，"在[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]MSDN 上的开发人员指南。  
  
 对于所有类<xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute>自定义特性，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]调用其默认构造函数。 调用在启动的所有构造函数提供用来创建新对象的常见位置和独立于任何用户活动。  
  
 除了生成创作和管理个性化设置相关信息的少量缓存，类构造函数通常会订阅 <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> 和 <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing> 事件。 未能订阅这些事件可能会导致将类错误地标记为由公共语言运行时 (CLR) 垃圾收集器进行清理。  
  
 会话上下文  
 对于基于个性化设置扩展的那些对象，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 会在客户端会话期间创建执行环境，并在此环境中动态地生成大多数对象。 与其他任何 CLR 程序集一样，此执行环境还可以访问其他函数和存储过程。 用户会话结束时，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中删除动态创建的对象和关闭的执行环境。  
  
 事件  
 对象创建是由会话事件 `On-Cube-OpenedCubeOpened` 和 `On-Cube-ClosingCubeClosing` 触发的。  
  
 客户端与服务器之间的通信是通过特定事件发生的。 这些事件使客户端了解会导致生成客户端对象的情况。 客户端环境是使用两种事件动态创建的：会话事件和多维数据集事件。  
  
 会话事件与服务器对象关联。 当客户端登录到服务器，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]创建一个会话和触发器<xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened>事件。 客户端结束在服务器上，会话时[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]触发器<xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>事件。  
  
 多维数据集事件与连接对象关联。 连接到多维数据集会触发 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened> 事件。 关闭到多维数据集的连接（通过关闭多维数据集或更改到其他多维数据集）将触发 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing> 事件。  
  
 可跟踪性和错误处理  
 使用 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 可跟踪所有活动。 未处理的错误会报告给 Windows 事件日志。  
  
 所有对象的创作和管理都是独立于此体系结构，是对象的开发人员的唯一责任。  
  
## <a name="infrastructure-foundations"></a>基础结构基础  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化设置扩展基于现有组件。 下面简要列出了提供个性化设置扩展功能的增强功能和改进功能。  
  
### <a name="assemblies"></a>程序集  
 可以将自定义属性 <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> 添加到自定义程序集，用以标识 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化设置扩展类。  
  
### <a name="changes-to-the-adomdserver-object-model"></a>对 AdomdServer 对象模型的更改  
 <xref:Microsoft.AnalysisServices.AdomdServer> 对象模型中的下列对象已得到增强或已添加到模型。  
  
#### <a name="new-adomdconnection-class"></a>新增 AdomdConnection 类  
 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection> 类是新增的，并通过属性和事件公开多个性化设置扩展。  
  
 **属性**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.SessionID%2A>，只读字符串值，表示当前连接的会话 ID。  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.ClientCulture%2A>，对与当前会话关联的客户端区域性的只读引用。  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.User%2A>，对表示当前用户的标识接口的只读引用。  
  
 **事件**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing>  
  
#### <a name="new-properties-in-the-context-class"></a>上下文类中的新增属性  
 <xref:Microsoft.AnalysisServices.AdomdServer.Context> 类具有两个新增属性：  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.Server%2A>，对新增服务器对象的只读引用。  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentConnection%2A>，对新增 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection> 对象的只读引用。  
  
#### <a name="new-server-class"></a>新增服务器类  
 <xref:Microsoft.AnalysisServices.AdomdServer.Server> 类是新增的，并通过类属性和事件公开多个性化设置扩展。  
  
 **属性**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Name%2A>，表示服务器名称的只读字符串值。  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Culture%2A>，对与服务器关联的全局区域性的只读引用。  
  
 **事件**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>  
  
#### <a name="adomdcommand-class"></a>AdomdCommand 类  
 <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> 类现在支持以下 MDX 命令：  
  
-   [创建成员语句&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)  
  
-   [更新成员语句&#40;MDX&#41;](/sql/mdx/mdx-data-definition-update-member)  
  
-   [DROP 成员语句&#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-member)  
  
-   [创建 SET 语句&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-set)  
  
-   [拖放 SET 语句&#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-set)  
  
-   [创建 KPI 语句&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-kpi)  
  
-   [DROP KPI 语句&#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-kpi)  
  
### <a name="mdx-extensions-and-enhancements"></a>MDX 扩展和增强功能  
 通过 `caption` 属性、`display_folder` 属性和 `associated_measure_group` 属性对 CREATE MEMBER 命令进行了增强。  
  
 添加 UPDATE MEMBER 命令是为了在求解计算丢失优先顺序时需要更新的情况下避免重新创建成员。 更新无法更改计算成员的作用域，无法将计算成员移动到其他父级，也无法定义其他 `solveorder`。  
  
 通过 `caption` 属性、`display_folder` 属性和新 `STATIC | DYNAMIC` 关键字对 CREATE SET 命令进行了增强。 *静态*意味着，仅在创建时被评估为组。 *动态*意味着，对集进行评估在查询中使用集每次。 如果省略关键字，默认值则为 `STATIC`。  
  
 在 MDX 语法中增加了 CREATE KPI 和 DROP KPI 命令。 可以从任意 MDX 脚本动态创建 KPI。  
  
### <a name="schema-rowsets-extensions"></a>架构行集扩展  
 上 MDSCHEMA_MEMBERS*作用域*添加列。 作用域值如下：MDMEMBER_SCOPE_GLOBAL=1、MDMEMBER_SCOPE_SESSION=2。  
  
 上 MDSCHEMA_SETS *set_evaluation_context*添加列。 将计算上下文值设置为：MDSET_RESOLUTION_STATIC = 1、MDSET_RESOLUTION_DYNAMIC = 2。  
  
 在 MDSCHEMA_KPIS 上，增加了作用域列。 作用域值如下：MDKPI_SCOPE_GLOBAL=1、MDKPI_SCOPE_SESSION=2。  
  
  
