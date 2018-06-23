---
title: 商业智能 (CSDLBI) 的 CSDL 批注 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: bf6f372a-bc67-45ea-a771-b2dc5b0527e5
caps.latest.revision: 19
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 0e545667bd907460b695f63cbe9f2f537c9be62d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015968"
---
# <a name="csdl-annotations-for-business-intelligence-csdlbi"></a>用于商业智能的 CSDL 批注 (CSDLBI)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持以 XML 格式（称为带商业智能注释的概念性架构定义语言 (CSDLBI)）来表示表格模型定义。  
  
 本主题概要介绍了 CSDLBI 以及如何将其与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据模型结合使用。  
  
## <a name="understanding-the-role-of-csdl"></a>理解 CSDL 的角色  
 概念性架构定义语言 (CSDL) 是一种描述实体、关系和函数的基于 XML 的语言。 CSDL 定义为实体数据框架的一部分。 BI 注释是一个扩展，旨在支持使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 来对数据建模。  
  
 尽管 CSDL 符合实体数据框架，但您无需理解实体关系模型或具有用于基于模型生成表格模型或报表的任何特殊工具。 您可以使用客户端工具（如 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]）或 API（如 AMO）来生成模型，并将模型部署到服务器。 客户端通过使用模型定义文件连接到模型，模型定义文件通常发布到报表设计人员和报表使用者可以使用该文件的 SharePoint 库。 有关详细信息，请参阅以下链接：  
  
-   [表格模型解决方案&#40;SSAS 表格&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
-   [表格模型解决方案部署&#40;SSAS 表格&#41;](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
-   [PowerPivot BI 语义模型连接&#40;.bism&#41;](../power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)  
  
 CSDLBI 架构是 Analysis Services 服务器为响应来自客户端（如 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]）的模型定义请求而生成的。 客户端应用程序将 XML 查询发送到承载模型数据的 Analysis Services 服务器。 在响应中，该服务器将发送一条 XML 消息，消息中使用 CSDLBI 注释包含该模型中实体的定义。 然后，报表客户端使用这些信息来展现可用于模型中的字段、聚合和度量值。 CSDLBI 注释还提供有关如何对数据进行分组、排序和格式设置的信息。  
  
 有关 CSDLBI 的常规信息，请参阅[CSDLBI 概念](csdlbi-concepts.md)。  
  
### <a name="working-with-csdl"></a>使用 CSDL  
 表示任何特定表格模型的 CSDLBI 注释集是一个 XML 文档，其中包含简单实体和复杂实体的集合。 实体定义表（或维度）、列（属性）、关联（关系）以及包含在计算列、度量值或 KPI 中的公式。  
  
 您不能直接使用 CSDL 修改这些对象，而必须使用为使用表格模型而提供的客户端工具和应用程序编程接口 (API)。  
  
 您可以通过将 DISCOVER 请求发送到承载某个模型的服务器，获取该模型的 CSDL。 必须通过指定服务器和模型（这两者是必需的）以及视图或透视（这两者是可选的）对该请求加以限定。 返回的消息是一个 XML 字符串。 某些元素是依赖于语言的，因此可能会根据当前连接的语言返回不同值。 有关详细信息，请参阅[DISCOVER_CSDL_METADATA 行集](../schema-rowsets/xml/discover-csdl-metadata-rowset.md)。  
  
### <a name="csdlbi-versions"></a>CSDLBI 版本  
 原始 CSDL 规范（来自实体数据框架）是为支持建模所需的大多数实体和属性提供的。 BI 注释支持表格模型的特殊要求、客户端（如 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]）所需的报告属性和多维模型所需的附加数据。 此部分介绍每个版本中的更新。  
  
 **CSDLBI 1.0**  
  
 最初为支持 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格模型而添加到 CSDL 架构的一系列内容包含注释，用于支持数据建模、自定义计算和增强的显示格式：  
  
-   支持表格模型的新元素和属性。 例如，添加了一个属性来指定用于填充模型的数据库查询的类型。  
  
-   针对现有实体的新属性和扩展插件。  例如，Association 元素已扩展为支持关系。  
  
-   可视化和导航属性。 例如，添加了一些属性以支持自定义排序字段、默认图像以及  
  
 **CSDLBI 1.1**  
  
 这一版本的 CSDLBI 架构添加的项用于支持多维数据库（如 OLAP 多维数据集）。 新元素和属性如下所示：  
  
-   支持将维度作为实体。  
  
-   支持层次结构。  
  
-   公开 ROLAP 分区。  
  
-   支持转换。  
  
-   支持透视。  
  
 有关 CSDLBI 注释中各个元素的详细信息，请参阅[BI 批注的 CSDL 到的技术参考](conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)。 有关核心 CSDL 规范的信息，请参阅[CSDL v3 规范](https://msdn.microsoft.com/en-us/data/jj652004)MSDN 上。  
  
## <a name="see-also"></a>请参阅  
 [了解表格对象模型](representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [CSDLBI 概念](csdlbi-concepts.md)   
 [了解表格对象模型](representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  