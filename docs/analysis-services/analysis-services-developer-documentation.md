---
title: Analysis Services 开发人员文档 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 44be6e7ab0bb3598b2478f1a5f94e64fee48d05a
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449979"
---
# <a name="analysis-services-developer-documentation"></a>Analysis Services 开发人员文档
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

在 Analysis Services 中，几乎每个对象和工作负荷可编程的并且通常没有多个方法可供选择。  选项包括编写托管代码、 脚本或使用 XMLA 和 MSOLAP 等开放标准，如果你的解决方案要求不使用.NET framework。

## <a name="what-you-can-accomplish-in-code"></a>可以在代码中完成的操作
典型的编程方案包括服务器和数据库部署、 管理、 模型和创建数据库和从你的自定义应用程序和报表使用 Analysis Services 数据的数据访问。 所有这些情况下是固定的体系结构和对象定义包含的层次结构，跨数据定义、 处理和查询工作负荷的易于理解操作。

尽管对象和工作负荷进行编程，但它们不可扩展。 具体而言，不能创建自定义数据盒从不支持的数据源检索数据、 自定义或替换公式或存储引擎行为的也可以在创建新类型的对象元数据上服务器、 数据库或模型。

若要进一步详述了有关创建新的对象类型的最后一个点： 无法创建新类型的对象，也可以创建计算的对象在运行时从表达式或代码生成。 并非所有模型中的内容都需要预定义并映射到现有数据结构。 此外，您可以扩展通过 AMO 将特定于对象的信息传递给客户端应用程序中的批注的架构。

## <a name="choose-a-platform-or-approach-to-development"></a>选择平台或开发方法
Analysis Services 提供了多种可以自定义解决方案，通过代码，但大多数开发人员使用托管的 Api 或脚本。

- 托管的 Api 包括[AMO 和 TOM](http://msdn.microsoft.com/library/mt436122.aspx)的数据定义和管理任务，并[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx)以提供从客户端代码的查询支持。 在 SQL Server 2016 中，AMO 将更新为新的表格元数据用于创建或升级到兼容级别 1200年及更高版本的模型。

- 通常，脚本可以实现与可执行文件，与可能较少工作的程序相同的结果。

  - 您可以编写 PowerShell 脚本使用直接调用 AMO 类型的 Analysis Services PowerShell 组件。 在 PowerShell 中，您还可以创建和执行 ASSL/XMLA 或 TMSL （在 JSON 中) 脚本。

  - ASSL 和 TMSL 是提供在中使用对象的脚本语言发现和执行操作。 使用哪种类型的脚本依赖于基础服务器、 数据库或模型。

  - 表格模型或数据库兼容级别 1200年及更高版本使用表格模型脚本语言 (TMSL)，这是在 JSON 中。

  - 多维模型和兼容级别 1050年-1103年的表格模型使用 Analysis Services 脚本语言 (ASSL)，这是 XMLA 开放标准的 Analysis Services 扩展插件。

  - 你可以在 Management Studio 中生成 ASSL 或 TMSL 脚本。 此外可以使用**查看代码**SQL Server Data Tools 在 ASSL 或 TMSL 中查看模型定义中。

- 尽管可以生成基于开放标准的 XMLA 和 MDX 的解决方案，但它是很少见，若要执行此操作。 没有任何文档以外 XMLA 和 MDX 参考，可帮助你和大多数社区和论坛支持绘制从使用.NET 或本机 (MSOLAP) 技术的体验。

## <a name="programming-in-analysis-services"></a>在 Analysis Services 中的编程
[数据挖掘编程](../analysis-services/data-mining/data-mining-programming.md)介绍构建解决方案，其中包括数据挖掘对象的方法。

[多维模型编程](../analysis-services/multidimensional-models/multidimensional-model-programming.md)介绍的开发任务和集成自定义解决方案中的多维模型对象的方法。

[表格模型编程兼容级别 1200年及更高版本](../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)
**SQL Server 2016 中的新增功能**。  总结了的接口和脚本语言，用于以编程方式使用表格 1200年模型和更高版本的模型。

[表格模型编程兼容级别 1050 1103年通过为](../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)本文档适用于开发人员支持在更低的兼容性级别的表格模型。 它描述了在 XML 语法定义表格模型的 CSDL 扩展插件。 它还包括有关表格对象模型的定义和语法的信息。

[Analysis Services 管理对象 (AMO)](https://msdn.microsoft.com/library/mt436122.aspx)托管的提供 Analysis Services 管理对象 (AMO)，数据定义和管理，包括处理程序的开发人员参考文档。

[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx)用于编程数据访问和查询工作负荷的托管提供程序，ADOMD.NET 中，开发人员参考文档。

[Analysis Services 架构行集](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets)介绍提供有关服务器状态、 服务器操作和数据库对象的信息的架构行集。

[用于分析 XML &#40;XMLA&#41;引用](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)介绍了 XMLA 概念，它们可以帮助您了解 XMLA 如何影响你的自定义解决方案。 它还说明遵从 XMLA 1.1 规范的级别。

[Analysis Services 脚本语言&#40;支持 XMLA 的 ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)介绍的 XMLA ASSL 扩展。 ASSL 提供补充 XMLA 规范的 Analysis Services 多维模型的数据定义和操作语言。

[表格模型脚本语言&#40;TMSL&#41;引用](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)TMSL 是兼容性级别 1200年及更高版本的表格模型的 JSON 表示形式。 对象定义基于如表、 列和关系而不是多维元数据可能不熟悉，如果您不熟悉 Analysis Services 数据建模在表格模式下的表格元数据构造。

[Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md)记录了用于管理的功能，以及常规用途的 cmdlet **Invoke-ascmd**接受任何脚本或查询作为输入的 cmdlet。

## <a name="see-also"></a>请参阅
[技术参考](../analysis-services/powershell/technical-reference-ssas.md)
[查询和表达式语言参考&#40;Analysis Services&#41;](http://msdn.microsoft.com/library/gg492188.aspx)
