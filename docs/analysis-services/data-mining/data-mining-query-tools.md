---
title: 数据挖掘查询工具 |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 697a1c06a2d30d5721c122c557f3e41836335b02
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449949"
---
# <a name="data-mining-query-tools"></a>数据挖掘查询工具
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  所有数据挖掘查询都使用数据挖掘扩展插件 (DMX) 语言。 DMX 可以用于为所有种类的机器学习任务创建模型，包括分类、风险分析、建议生成和线性回归。 还可以编写 DMX 查询以获取有关在处理模型时生成的模式和统计信息的信息。  
  
 可以编写自己的 DMX，也可以使用某种工具（如 **预测查询生成器** ）生成基本 DMX，然后进行修改。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 均提供了有助于生成 DMX 预测查询的工具。 本主题介绍如何使用这些工具创建和执行数据挖掘查询。  
  
-   [预测查询生成器](#bkmk_Builder)  
  
-   [查询编辑器](#bkmk_QueryEditor)  
  
-   [DMX 模板](#bkmk_Templates)  
  
-   [Integration Services](#bkmk_SSIS)  
  
-   [应用程序编程接口](#bkmk_API)  
  
##  <a name="bkmk_Builder"></a> 预测查询生成器  
 数据挖掘设计器的 **“挖掘模型预测”** 选项卡中提供了预测查询生成器，可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中使用。  
  
 使用该查询生成器时，可选择挖掘模型、添加新事例数据和添加预测函数。 随后可以切换到文本编辑器以手动修改查询，或切换到“结果”窗格以查看查询的结果。  
  
##  <a name="bkmk_QueryEditor"></a> 查询编辑器  
 通过 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的查询编辑器还可以生成和运行 DMX 查询。 可以连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的实例，然后选择数据库、挖掘结构列和挖掘模型。 **“元数据浏览器”** 包含可浏览的预测函数的列表。  
  
##  <a name="bkmk_Templates"></a> DMX 模板  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了可用于生成 DMX 查询的交互式 DMX 查询模板。 如果看不到模板列表，请单击工具栏上的 **“视图”** ，然后选择 **“模板资源管理器”**。 若要查看所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 模板，包括用于 DMX、MDX 和 XMLA 的模板，请单击多维数据集图标。  
  
 若要使用模板生成查询，您可以将模板拖入打开的查询窗口中，也可以双击模板以打开新的连接和新的查询窗格。  
  
 有关如何通过模板创建预测查询的示例，请参阅 [通过模板创建单独预测查询](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md)。  
  
> [!WARNING]  
>  针对 Microsoft Office Excel 的数据挖掘外接程序还包含多个模板以及可帮助您编写复杂的 DMX 语句的交互式查询生成器。 若要使用模板，请单击 **“查询”**，再单击数据挖掘客户端中的 **“高级”** 。  
  
##  <a name="bkmk_SSIS"></a> Integration Services 数据挖掘组件  
 还可以将预测查询包括在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包中。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的以下任务和转换支持创建和执行 DMX 预测查询和 DMX 语句。  
  
|组件|Description|  
|---------------|-----------------|  
|数据挖掘查询任务|将 DMX 查询和其他 DMX 语句作为控制流的一部分执行。<br /><br /> 任务编辑器提供了预测查询生成器和一个用于手动修改 DMX 查询的文本框。 但是，任务编辑器无法验证针对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 解决方案中的对象的查询。 因此，最好是在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中创建查询，然后将语句或查询的文本粘贴到任务编辑器中。|  
|数据挖掘查询转换|使用数据流源所提供的数据，在数据流内执行预测查询。<br /><br /> 任务编辑器提供了预测查询生成器和一个用于手动修改 DMX 查询的文本框。<br /><br /> 转换只能用于创建使用数据流中的数据的查询；即使用 PREDICTION JOIN 语法的查询。 此组件不能用于执行内容查询或其他类型的 DMX 语句。|  
  
##  <a name="bkmk_API"></a> 应用程序编程接口  
 您可以创建自定义应用程序，这些应用程序通过使用多种编程语言，并且与 OLE DB 或 Analysis Services ADOMD 客户端之类的服务器协议相结合，针对数据挖掘模型执行查询。 有关详细信息，请参阅 [数据挖掘编程](../../analysis-services/data-mining/data-mining-programming.md)。  
  
 但是，XMLA 构成了与 Analysis Service 服务器进行的所有交互的基础邮件格式。 在某一 XMLA 消息内，根据您是否基于 DMX、内容查询或使用数据挖掘架构行集检索模型元数据的查询发送预测查询，表示查询的方式也将有所不同。  
  
-   **预测查询**的文本（以及所有其他 DMX 语句）通过使用 [Execute 方法 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) 以 XMLA 形式发送，而 DMX 查询以文本的形式放置于 XMLA [Command 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/command-element-xmla) 的 [Statement 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) 内。  
  
-   若要检索**模型内容**和**模型元数据**，例如群集的数目、在决策树中使用的属性、上次处理模型的日期以及在创建模型时使用的算法参数，可以使用 [Discover 方法 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) 并在 [RequestType 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/requesttype-element-xmla) 标头中指定数据挖掘架构行集之一。 若要缩小查询范围，请在 [RestrictionList 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictionlist-element-xmla) 内输入限制条件。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件 (DMX) 参考](../../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘解决方案](../../analysis-services/data-mining/data-mining-solutions.md)   
 [了解 DMX Select 语句](../../dmx/understanding-the-dmx-select-statement.md)   
 [DMX 预测查询的结构和用法](../../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [使用预测查询生成器创建预测查询](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)   
 [在 SQL Server Management Studio 中创建一个 DMX 查询](../../analysis-services/data-mining/create-a-dmx-query-in-sql-server-management-studio.md)  
  
  
