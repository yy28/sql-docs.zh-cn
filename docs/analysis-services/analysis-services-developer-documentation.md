---
title: "Analysis Services 开发人员文档 |Microsoft 文档"
ms.custom: 
ms.date: 03/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- multidimensional data [Analysis Services], developer's guide
- developer's guide [Analysis Services - multidimensional data]
ms.assetid: 0a6eda76-1c5e-487e-9c8b-1feb09f1a34c
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4694fd3def6dea209929f99559fcc61fe833972a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-developer-documentation"></a>Analysis Services 开发人员文档
在 Analysis Services 中，几乎每个对象和工作负荷可编程的并且通常没有可供选择的多个方法。  选项包括编写托管代码、 脚本或使用开放标准，如 XMLA 和 MSOLAP，如果你的解决方案要求不使用.NET framework。

## <a name="what-you-can-accomplish-in-code"></a>可以在代码中完成的新增功能
典型的编程方案包括服务器和数据库部署、 管理、 模型和数据库创建和从你的自定义应用程序和使用 Analysis Services 数据的报表的数据访问。 所有这些情况下是固定体系结构和对象定义层次结构，与跨数据定义、 处理和查询工作负荷的易于理解操作。

尽管对象和工作负荷是可编程的但它们都不可扩展。 具体而言，不能创建自定义数据盒从不支持的数据源检索数据、 自定义或替换公式或存储引擎行为，也可以您创建新类型的对象元数据在服务器、 数据库或模型。

若要进一步详细阐述有关创建新对象类型在最后一个点上： 尽管你无法创建新类型的对象，你可以创建计算的对象在运行时从表达式或代码生成。 您的模型中不是全部需要预定义和映射到现有数据结构。 此外，你可以扩展通过 AMO 将特定于对象的信息传递给客户端应用程序中的批注架构。

## <a name="choose-a-platform-or-approach-to-development"></a>选择平台或开发方法
Analysis Services 提供了许多方法，以自定义解决方案，通过代码，但大多数开发人员使用托管的 Api 或脚本。

- 托管的 Api 包括[AMO 和 TOM](http://msdn.microsoft.com/library/mt436122.aspx)数据定义和管理任务和[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx)以提供查询支持从客户端代码。 在 SQL Server 2016 中，AMO 更新为使用的模型创建或升级到兼容性级别 1200年或更高版本的新表格元数据。

- 脚本通常可以获得相同的结果作为可执行文件、 使用工作较少可能程序。

  - 你可以编写 PowerShell 脚本中使用直接调用 AMO 类型的 Analysis Services PowerShell 组件。 在 PowerShell 中，你还可以创建和执行 ASSL/XMLA 或 TMSL （在 JSON) 脚本。

  - ASSL 和 TMSL 是提供在使用对象的脚本语言发现和执行操作。 你使用哪种类型的脚本依赖于基础的服务器、 数据库或模型。

  - 表格模型或数据库兼容级别 1200年或更高版本使用表格模型脚本语言 (TMSL)，这是 json 格式。

  - 多维模型和兼容性级别 1050年 1103年表格模型使用 Analysis Services 脚本语言 (ASSL)，这是 XMLA 开放标准的 Analysis Services 扩展插件。

  - 你可以在 Management Studio 中生成 ASSL 或 TMSL 脚本。 你还可以使用**查看代码**SQL Server Data Tools，若要查看在 ASSL 或 TMSL 的模型定义中。

- 但也可以生成基于开放标准的 XMLA 和 MDX 的解决方案，它是非常罕见，若要这样做。 没有任何文档以外 XMLA 和 MDX 引用来帮助你，和大多数社区和支持的论坛绘制通过使用.NET 或本机 (MSOLAP) 技术的体验。

## <a name="programming-in-analysis-services"></a>Analysis Services 中的编程
[数据挖掘编程](../analysis-services/data-mining-programming.md)描述生成解决方案，其中包括数据挖掘对象的方法。

[多维模型编程](../analysis-services/multidimensional-models/multidimensional-model-programming.md)描述开发任务和集成自定义解决方案中的多维模型对象的方法。

[表格模型编程的兼容性级别 1200年及更高版本](../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)
**SQL Server 2016 中的新增功能**。  总结了的接口和用于以编程方式使用表格 1200年和更高版本的模型的脚本语言。

[模型编程表格通过 1103年兼容性级别 1050年](../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)本文档适用于开发人员支持更早版本兼容性级别的表格模型。 它描述了在 XML 语法定义表格模型的 CSDL 扩展。 它还包括有关表格对象模型定义和语法的信息。

[Analysis Services 管理对象 (AMO)](https://msdn.microsoft.com/library/mt436122.aspx)托管的提供 Analysis Services 管理对象 (AMO)，数据定义和管理，包括处理程序的开发人员参考文档。

[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx)用于编程的数据访问和查询工作负荷管理的提供程序，ADOMD.NET，开发人员参考文档。

[Analysis Services 架构行集](../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)描述提供有关服务器状态、 服务器操作和数据库对象的信息的架构行集。

[XML for Analysis &#40;XMLA &#41;引用](../analysis-services/xmla/xml-for-analysis-xmla-reference.md)描述 XMLA 概念可帮助你了解如何 XMLA 有助于构建你自定义解决方案。 它还说明遵从 XMLA 1.1 规范的级别。

[Analysis Services 脚本语言 &#40;ASSL 为 XMLA &#41;](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)介绍的 XMLA ASSL 扩展。 ASSL 提供补充 XMLA 规范的 Analysis Services 多维模型的数据定义和操作语言。

[表格模型脚本语言 &#40;TMSL &#41;引用](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)TMSL 是的 JSON 表示形式在兼容级别 1200年或更高的表格模型。 对象定义基于表格元数据结构，比如表、 列和关系而不是多维可能不熟悉，如果你不熟悉 Analysis Services 数据建模在表格模式下的元数据。

[Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md)时记录该对象用于管理功能，加上通用的 cmdlet **Invoke ASCmd**接受任何脚本或查询作为输入的 cmdlet。

## <a name="see-also"></a>另请参阅
[技术参考 &#40;SSAS &#41;](../analysis-services/powershell/technical-reference-ssas.md) 
[查询和表达式语言参考 &#40;Analysis Services &#41;](http://msdn.microsoft.com/library/gg492188.aspx)

