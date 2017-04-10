---
title: "从挖掘模型钻取到事例数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "钻取 [Analysis Services]"
ms.assetid: b4d3f350-e543-4ea9-b3a2-b4f7c0a9ae27
caps.latest.revision: 21
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 21
---
# 从挖掘模型钻取到事例数据
  如果挖掘模型已配置为允许钻取到模型事例，在浏览此模型时，可以检索与用于创建此模型的事例的详细信息。 此外，如果基础挖掘结构已配置为允许钻取到结构事例，并且您具备相应的权限，则可返回挖掘结构的信息。 其中可以包括挖掘模型中未包含的列。  
  
 如果挖掘结构不允许钻取到基础数据，但挖掘模型允许，则可查看模型事例的信息，而无法查看挖掘结构的信息。  
  
> [!NOTE]  
>  可以通过将 **AllowDrillthrough** 属性设置为 **True**，向现有的挖掘模型添加钻取功能。 但是，在启用钻取功能之后，必须先重新处理相应的模型，然后才能查看事例数据。 有关详细信息，请参阅[对挖掘模型启用钻取](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)。  
  
 根据您所使用的查看器的类型，您可以按照下面的方式选择钻取节点：  
  
|查看器名称|窗格或选项卡名称|选择节点|  
|-----------------|----------------------|-----------------|  
|**Microsoft 树查看器**|**“决策树”** 选项卡|单击树节点。<br /><br /> **注意** 请避免对 **All** 节点使用钻取，否则要花很长时间才能返回结果。|  
|**Microsoft 分类查看器**|**分类关系图**|单击群集节点。|  
|**Microsoft 分类查看器**|**分类剖面图**|单击分类列中的任意位置。|  
|**Microsoft 关联查看器**|**“规则”** 选项卡|单击包含一组规则的行。|  
|**Microsoft 关联查看器**|**“项集”** 选项卡|单击包含项集的行。|  
|**Microsoft 顺序分析和聚类分析查看器**|**“规则”** 选项卡|单击包含一组规则的行。|  
|**Microsoft 顺序分析和聚类分析查看器**|**“项集”** 选项卡|单击包含项集的行。|  
  
> [!NOTE]  
>  某些模型不能使用钻取。 能否使用钻取取决于创建模型所用的算法。 有关支持钻取功能的挖掘模型类型的列表，请参阅[钻取查询（数据挖掘）](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
### 查看挖掘模型的钻取数据  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含想要的挖掘模型的挖掘结构。  
  
2.  在数据挖掘设计器中，单击 **“挖掘模型查看器”** 选项卡。  
  
3.  从“挖掘模型”下拉列表中选择模型。  
  
4.  从“查看器”下拉列表中选择一个查看器，然后右键单击特定节点。  
  
5.  选择 **“钻取”**，然后选择 **“仅限于模型列”**或 **“模型和结构列”** 以打开 **“钻取”** 窗口。  
  
6.  若要将数据复制到剪贴板，请右键单击表中的任何行，并选择“全部复制”。  
  
## 另请参阅  
 [钻取查询（数据挖掘）](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
  