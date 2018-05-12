---
title: 度量值和度量值组 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 04eb5a41bec6e9abb62cfde516f2dad2ff820521
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="measures-and-measure-groups"></a>度量值和度量值组
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  多维数据集包括 *度量值组* 中的 *度量值*、业务逻辑和给出上下文用于计算度量值提供的数值数据的维度集合。 度量值和度量值组都是多维数据集的必备组件。 多维数据集不能缺少其中的任何一项。  
  
 本主题将介绍 [Measures](#bkmk_measure) 和 [Measure Groups](#bkmk_mg)。 它还包含以下表格，以及指向有关创建和配置度量值和度量值组的过程步骤的链接。  
  
|**链接**|**Description**|  
|--------------|---------------------|  
|[在多维模型中创建度量值和度量值组](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|选择多种方法中的其中一种来创建度量值和度量值组。|  
|[配置度量值属性](../../analysis-services/multidimensional-models/configure-measure-properties.md)|如果使用多维数据集向导来启动多维数据集，则在聚合值之前可能需要更改聚合方法、应用数据格式、在客户端应用程序中设置该度量值的可见性，或添加度量值表达式以处理数据。|  
|[配置度量值组属性](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)|在多维模型中，度量值组相当于源数据仓库中的事实数据表。 通过度量值组的属性，你可以指定缓存行为、存储以及在度量值组级别统一操作的处理指令。 分区配置部分确定于你在度量值组对象上设置的属性。|  
|[使用聚合函数](../../analysis-services/multidimensional-models/use-aggregate-functions.md)|了解可分配给度量值的聚合方法。|  
|[定义半累加性行为](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)|半累加性行为是指对某些维度有效而对其他维度无效的聚合。 常见示例为银行帐户余额。 你可能想按客户和地域（而不是时间）来聚合余额。 例如，您可能不想连续数日从相同帐户添加余额。 若要定义半累加性行为，请使用“添加商业智能向导”。|  
|[链接度量值组](../../analysis-services/multidimensional-models/linked-measure-groups.md)|重用同一数据库中或不同 Analysis Services 数据库中其他多维数据集的现有度量值组。|  
  
##  <a name="bkmk_measure"></a> Measures  
 度量值表示一个列，其中包含可以聚合的可计量数据（通常是数值）。 度量值表示组织活动的一些方面，这些方面以货币术语（如收入、利润或成本）表示，按计数（库存水平、员工数、客户或订单），或者按采用业务逻辑的更复杂的计算表示。  
  
 每个多维数据集必须至少具有一个度量值，不过大多数都有很多个度量值，有时达到数百个。 从结构上来说，度量值通常映射到事实数据表中的源列，该列提供用于加载度量值的值。 或者，你还可以用 MDX 定义度量值。  
  
 度量值与上下文相关，在上下文的数值数据上运行，该上下文由碰巧包含在查询中的任何维度成员确定。 例如，计算“分销商销售”的度量值将由 **Sum** 运算符支持，并且将添加查询中包含的每个维度成员的销售额。  无论查询指定单个产品、 汇总到一个类别，还是按时间或地域进行切分，该度量值都应生成对查询中所含维度有效的操作。  
  
 在此示例中，“分销商销售”沿“销售区域”层次结构聚合为各种级别。  
  
 ![数据透视表的度量值和维度调出](../../analysis-services/multidimensional-models/media/ssas-keyconcepts-pivot1-measures-dimensions.png "的度量值和维度调出的数据透视表")  
  
 当包含数值源数据的事实数据表也包含查询中使用的维度表的指针时，度量值将产生有效结果。 使用分销商销售示例时，如果存储了销售额的各行还存储了产品表、日期表或销售区域表的指针，则包含这些维度的成员的查询将会正确解析。  
  
 如果该度量值与查询中使用的维度无关，将发生什么？ 通常，Analysis Services 将显示默认度量值，并且所有成员的值都相同。 在此示例中，用联机目录测量客户进行的直接销售的“Internet 销售”与销售组织无关。   
  
 ![数据透视表显示重复度量值](../../analysis-services/multidimensional-models/media/ssas-unrelatedmeasure.PNG "数据透视表显示重复度量值")  
  
 为了尽量减少在客户端应用程序遇到这些行为的机会，你可在同一数据库中生成多个多维数据集或透视，并确保每个多维数据集或透视仅包含相关对象。 需要检查的关系位于度量值组（映射到事实数据表）和维度之间。  
  
##  <a name="bkmk_mg"></a> Measure Groups  
 在多维数据集中，度量值按照其基础事实数据表分组为多个度量值组。 度量值组用于使维度和度量值相互关联。 度量值组还可用于将非重复计数作为其聚合行为的度量值。 将每个非重复计数度量值放入自己的度量值组后，可优化聚合处理。  
  
 一个简单的 <xref:Microsoft.AnalysisServices.MeasureGroup> 对象包含组名、存储模式和处理模式等基本信息。 它还包含其组成部分；度量值、维度和构成度量值组的分区。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的多维数据集](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)   
 [在多维模型中创建度量值和度量值组](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)  
  
  
