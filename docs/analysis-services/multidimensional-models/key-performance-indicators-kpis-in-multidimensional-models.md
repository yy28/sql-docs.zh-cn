---
title: "密钥多维模型中的性能指标 (Kpi) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing Key Performance Indicators
- Key Performance Indicators [Analysis Services]
- KPIs [Analysis Services]
- OLAP objects [Analysis Services], performance indicators
- weights [Analysis Services]
- displaying Key Performance Indicators
- parent KPIs [Analysis Services]
- child KPIs
ms.assetid: 73aee2da-da30-44f1-829c-0a4c078a7768
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 396ac061fca578b06766830948001387c65b036e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="key-performance-indicators-kpis-in-multidimensional-models"></a>多维模型中的关键绩效指标 (KPI)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]在业务术语中，关键绩效指标 (KPI) 是用于测定业务成功的可量化度量。  
  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，KPI 是指与用于评估业务绩效的多维数据集中某个度量值组关联的计算的集合。 这些计算通常是多维表达式 (MDX) 或计算成员的组合。 KPI 还包括其他的元数据，该元数据提供有关客户端应用程序如何显示 KPI 计算结果的信息。  
  
 KPI 处理关于目标集、多维数据集中记录的性能的实际公式以及用于显示性能走向和状态的度量的信息。 AMO 用于定义针对 KPI 值的公式以及其他定义。 查询接口（如 ADOMD.NET）由客户端应用程序用于检索操作并向最终用户公开 KPI 值。 有关详细信息，请参阅 [使用 ADOMD.NET 进行开发](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)。  
  
 一个简单的 <xref:Microsoft.AnalysisServices.Kpi> 对象由基本信息、目标、获取的实际值、状态值、走向值以及在其中查看 KPI 的文件夹组成。 基本信息包括 KPI 的名称和说明。 目标是计算结果为数字的 MDX 表达式。 实际值是计算结果为数字的 MDX 表达式。 状态值和走向值是计算结果为数字的 MDX 表达式。 文件夹是向客户端显示 KPI 时的推荐位置。  
  
 在业务术语中，关键绩效指标 (KPI) 是一个用于测定业务绩效的可计量度量值。 经常会在一段时间内评估 KPI。 例如，一个单位的销售部门可以使用每月的毛利润作为 KPI，但同一单位的人力资源部门可以使用每季度流失的雇员作为 KPI。 这两个都是 KPI 的示例。 业务主管经常使用以业务计分卡形式分组在一起的 KPI 获取迅速且精确的业务绩效历史摘要。  
  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，KPI 是指与用于评估业务绩效的多维数据集中某个度量值组关联的计算的集合。 这些计算通常是多维表达式 (MDX) 和计算成员的组合。 KPI 还包括其他的元数据，该元数据提供有关客户端应用程序如何显示 KPI 计算结果的信息。  
  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中使用 KPI 的一个主要优点为，它们是基于服务器的 KPI，可以由不同的客户端应用程序使用。 与来自个别客户端应用程序的个别真实版本相比较，基于服务器的 KPI 只提供单个真实版本。 此外，在服务器上而不是在每台客户端计算机上执行有时很复杂的计算可能对性能有好处。  
  
## <a name="common-kpi-terms"></a>常用 KPI 术语  
 下表提供了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中常见 KPI 术语的定义。  
  
|术语|定义|  
|----------|----------------|  
|目的|一个返回 KPI 目标值的 MDX 数值表达式或计算。|  
|ReplTest1|一个返回 KPI 实际值的 MDX 数值表达式。|  
|“登录属性”|一个表示指定时间点 KPI 状态的 MDX 表达式。<br /><br /> 状态 MDX 表达式应返回介于 -1 到 1 之间的标准化值。 等于或小于 -1 的值将作为“差值”或“低值”。 零值 (0) 被理解为“可接受值”或“中间值”。 等于或大于 1 的值将作为“优值”或“高值”。<br /><br /> 如果受客户端应用程序支持，则可以有选择地返回不限制数目的中间值，并使用这些值来显示任意数目的附加状态。|  
|走向|一个评估一段时间内 KPI 值的 MDX 表达式。 走向可以是任何基于时间的条件，该条件在特定的业务上下文中很有用。<br /><br /> 使用走向 MDX 表达式，业务用户可以确定 KPI 是随时间升高还是随时间降低。|  
|状态指示器|一个提供 KPI 状态快速指示的可见元素。 该元素的显示内容由评估状态的 MDX 表达式的值确定。|  
|走向指示器|一个提供 KPI 走向的快速指示的可见元素。 该元素的显示内容由评估走向的 MDX 表达式的值确定。|  
|显示文件夹|KPI 所在的文件夹将在用户浏览多维数据集时显示出来。|  
|父级 KPI|一个对现有 KPI 的引用，该引用使用子级 KPI 的值作为父级 KPI 计算的一部分。 有时，单个 KPI 是由其他 KPI 的值组成的计算。 该属性便于正确显示客户端应用程序中父级 KPI 下的子级 KPI。|  
|当前时间成员|一个返回标识 KPI 临时上下文的成员的 MDX 表达式。|  
|Weight|一个为 KPI 分配相对重要性的 MDX 数值表达式。 如果将 KPI 分配给一个父级 KPI，则在计算父级 KPI 的值时，将使用权重按比例调整子级 KPI 值的结果。|  
  
## <a name="parent-kpis"></a>父级 KPI  
 一个单位可以跟踪不同级别的不同商务跃点。 例如，仅使用两个或三个 KPI 即可测定整个公司的业务绩效，但是这些公司范围内的 KPI 可能基于三个或四个由整个公司内的业务单元跟踪的其他 KPI。 同样，公司内的业务单元可以使用不同的统计信息来计算相同的 KPI，其结果汇总到公司范围内的 KPI 中。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可让你定义 KPI 之间的父子关系。 这种父子关系允许使用子级 KPI 的结果来计算父级 KPI 的结果。 客户端应用程序也可以使用此关系来正确显示父级和子级 KPI。  
  
## <a name="weights"></a>权重  
 还可以将权重分配给子级 KPI。 当计算父级 KPI 的值时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可使用权重按比例调整子级 KPI 的结果。  
  
## <a name="retrieving-and-displaying-kpis"></a>检索和显示 KPI  
 KPI 的显示内容依赖于客户端应用程序的实现。 例如，在多维数据集设计器的 **KPI** 选项卡上的工具栏上选择 **“浏览器视图”** 可说明一种可能的客户端实现，其中图形用于显示状态指示器和走向指示器，显示文件夹用于对 KPI 进行分组，并且子级 KPI 显示在父级 KPI 下。  
  
 您可以使用 MDX 函数检索 KPI 的各个部分（如值或目标）以便在 MDX 表达式、语句以及脚本中使用。  
  
  
