---
title: "挖掘结构和结构列的属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "挖掘结构 [Analysis Services], 列属性"
  - "数据挖掘 [Analysis Services], 属性"
  - "列 [数据挖掘], 属性"
  - "属性 [数据挖掘]"
ms.assetid: ce90f684-bb8c-4eca-b9e6-000794dbee16
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 23
---
# 挖掘结构和结构列的属性
  可以使用数据挖掘设计器的 **“挖掘结构”** 选项卡，为挖掘结构及其关联的列和嵌套表设置或更改属性。 在该选项卡中设置的属性将传播到与结构相关联的每个挖掘模型。  
  
> [!NOTE]  
>  如果更改挖掘结构中的任何属性的值，即使是名称或说明等元数据，也必须首先重新处理该挖掘结构及其模型，然后才能查看或查询模型。  
  
## 挖掘结构和挖掘结构列的属性  
 下表描述挖掘结构和挖掘结构列的属性，这些属性特定于数据挖掘，并且可以在 **“挖掘结构”** 选项卡中进行查看和配置。 若要查看或配置这些属性，请在树视图中右键单击元素，然后单击“属性”。  
  
-   若要查看结构的属性，请单击挖掘结构标题。  
  
-   若要查看列或嵌套表的属性，请单击列名称。  
  
### 挖掘结构的属性  
  
|属性|Description|  
|--------------|-----------------|  
|**CacheMode**|指定在定型中使用的事例在定型完成之后应缓存还是放弃。 **注意：**此属性必须设置为 **KeepTrainingCases** 以启用钻取和维持功能。|  
|**排序规则**|指定列的默认排序规则。 如果没有指定排序规则，则将使用服务器的排序规则。|  
|**Description**|描述挖掘结构。 该描述应陈述结构中数据的目的和构成，这是最佳的做法。|  
|**ErrorConfiguration（默认值）**|指定错误的特殊处理（如果有）选项。|  
|**HoldoutMaxCases**|指定可保留为测试数据集的最大结构事例数。  如果同时为 **HoldoutMaxCases** 和 **HoldoutPercent**指定了值，则这些条件将结合使用。 **注意：**若要设置此属性，<xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> 必须设置为 **KeepTrainingCases**。|  
|**HoldoutPercent**|指定保留为测试数据集的结构事例的百分比。 如果同时为 **HoldoutMaxCases** 和 **HoldoutPercent**指定了值，则这些条件将结合使用。 **注意：**若要设置此属性，<xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> 必须设置为 **KeepTrainingCases**。|  
|**HoldoutSeed**|指定用于初始化维持测试集分区的种子，以确保可以重新创建测试数据集。 **注意：**若要设置此属性，<xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> 必须设置为 **KeepTrainingCases**。|  
|**ID**|显示挖掘结构的唯一标识符。<br /><br /> 创建挖掘结构时为其分配的名称将用作 ID。 如果之后通过为 **Name** 属性键入新值而更改了名称，则此新名称仅用作别名；但 ID 不会更改。|  
|**语言**|指定挖掘结构中标题的语言。|  
|**名称**|指定挖掘结构的名称或别名。<br /><br /> 如果更改了 Name 属性的值，则新的名称仅用作标题或别名；但挖掘结构的标识符不会更改。|  
|**数据源**|显示数据源的名称和类型。|  
  
### 挖掘结构列的属性  
  
|属性|Description|  
|--------------|-----------------|  
|**ClassifiedColumns**|标识已分类列所说明的列。|  
|**内容**|列的内容类型。|  
|**Description**|描述列。 列的描述应提供有关列中的数据如何针对数据挖掘派生或更改的信息，这是最佳的做法。|  
|**DiscretizationBucketCount**|显示离散化列中的存储桶数。<br /><br /> 仅当内容类型设置为 **Discretized**时启用。<br /><br /> 该属性为只读。|  
|**DiscretizationMethod**|显示用于离散化列的方法。<br /><br /> 仅当内容类型设置为 **Discretized**时启用。<br /><br /> 该属性为只读。|  
|**Distribution**|指定列中内容的分布。|  
|**ID**|显示列的标识符。<br /><br /> 如果您更改了列的 Name 属性的值，则不会影响 ID 属性的值。|  
|**IsKey**|指示列是否为键列。|  
|**KeyColumns**|包含用作属性键（或属性键的一部分）的列的定义。|  
|**ModelingFlags**|设置算法可用的其他参数。|  
|**名称**|列的名称。|  
|**NameColumn**|标识提供父元素名称的列。|  
|**数据源**|显示列的源。<br /><br /> 对于关系数据源，其值始终为 **(none)**。<br /><br /> 对于基于 OLAP 多维数据集的结构，其值为对用作嵌套表源的切片进行定义的 MDX 语句。|  
|**SourceMeasureGroup**|显示度量值组的源。<br /><br /> 对于关系数据源，其值始终为 **(none)**。<br /><br /> 对于基于 OLAP 多维数据集的结构，其值为对用作嵌套表源的切片进行定义的 MDX 语句。|  
|**类型**|列中内容的数据类型。|  
  
 有关设置或更改属性的详细信息，请参阅[挖掘结构任务和操作指南](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)。  
  
## 另请参阅  
 [创建关系挖掘结构](../../analysis-services/data-mining/create-a-relational-mining-structure.md)   
 [挖掘结构列](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  