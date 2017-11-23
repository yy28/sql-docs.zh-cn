---
title: "Microsoft 线性回归算法技术参考 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AUTO_DETECT_PERIODICITY parameter
- linear regression algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 7807b5ff-8e0d-418d-a05b-b1a9644536d2
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 188666c119f92bc0093877c055ed4097cc2e1471
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-linear-regression-algorithm-technical-reference"></a>Microsoft 线性回归算法技术参考
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法是 Microsoft 决策树算法的特殊版本，该线性回归算法针对连续属性的建模对进行了优化。 本主题说明该算法的实现，介绍如何自定义该算法的行为，并提供指向有关模型查询的其他信息的链接。  
  
## <a name="implementation-of-the-linear-regression-algorithm"></a>线性回归算法的实现  
 Microsoft 决策树算法可用于多种任务：线性回归、分类或关联分析。 若要为进行线性回归而实现此算法，应控制算法的参数以限制树的增长，并使模型中的所有数据都位于单个节点中。 也就是说，虽然线性回归基于决策树，但该树仅包含一个根节点而没有任何分支：所有数据都位于根节点中。  
  
 为实现这一目的，算法的 *MINIMUM_LEAF_CASES* 参数应设置为大于或等于该算法用于为挖掘模型定型的总事例数。 通过以这种方式设置该参数，算法在任何情况下都不会创建拆分，从而执行线性回归。  
  
 表示回归线的公式采用了通式 y = ax + b，该公式称为回归公式。 变量 Y 表示输出变量，X 表示输入变量，a 和 b 是可调整的系数。 您可以通过查询已完成的挖掘模型来检索回归公式的系数、截距和其他信息。 有关详细信息，请参阅 [线性回归模型查询示例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)。  
  
### <a name="scoring-methods-and-feature-selection"></a>计分方法和功能选择  
 所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据挖掘算法都会自动使用功能选择来改善分析效果以及减轻处理工作量。 线形回归中所用的功能选择方法为兴趣性分数，原因是该模型仅支持连续列。 下表列出了线性回归算法和决策树算法中功能选择上的差异，以供参考。  
  
|算法|分析方法|注释|  
|---------------|------------------------|--------------|  
|线性回归|兴趣性分数|默认值。<br /><br /> 决策树算法中可用的其他功能选择方法仅适用于离散变量，因此不适用于线性回归模型。|  
|决策树|兴趣性分数<br /><br /> Shannon 平均信息量<br /><br /> Bayesian with K2 Prior<br /><br /> 使用统一先验的 Bayesian Dirichlet（默认）|如果任何列包含非二进制连续值，则兴趣性分数将用于所有列，以确保一致性。 否则，将使用默认方法或指定的方法。|  
  
 控制决策树模型的功能选择的算法参数为 MAXIMUM_INPUT_ATTRIBUTES 和 MAXIMUM_OUTPUT。  
  
## <a name="customizing-the-linear-regression-algorithm"></a>自定义线性回归算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法支持多个参数，这些参数会影响所生成的挖掘模型的行为、性能和准确性。 您还可以对挖掘模型列或挖掘结构列设置建模标志来控制数据的处理方式。  
  
### <a name="setting-algorithm-parameters"></a>设置算法参数  
 下表列出了为 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法提供的参数。  
  
|参数|Description|  
|---------------|-----------------|  
|*MAXIMUM_INPUT_ATTRIBUTES*|定义算法在调用功能选择之前可以处理的输入属性数。 如果将此值设置为 0，则表示关闭功能选择。<br /><br /> 默认值为 255。|  
|*MAXIMUM_OUTPUT_ATTRIBUTES*|定义算法在调用功能选择之前可以处理的输出属性数。 如果将此值设置为 0，则表示关闭功能选择。<br /><br /> 默认值为 255。|  
|*FORCE_REGRESSOR*|强制算法将指示的列用作回归量，而不考虑算法为这些列计算出的重要性。|  
  
### <a name="modeling-flags"></a>建模标志  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法支持下列建模标志。 创建挖掘结构或挖掘模型时，定义建模标志以指定分析期间如何处理每列中的值。 有关详细信息，请参阅[建模标志（数据挖掘）](../../analysis-services/data-mining/modeling-flags-data-mining.md)。  
  
|建模标志|Description|  
|-------------------|-----------------|  
|NOT NULL|指示该列不能包含 Null。 如果 Analysis Services 在模型定型过程中遇到 Null 值，将会导致错误。<br /><br /> 适用于挖掘结构列。|  
|REGRESSOR|指示该列包含在分析过程中应被视为潜在独立变量的连续数值。 适用于挖掘模型列。<br /><br /> 注意：将列标记为回归量不能确保该列将在最终模型中用作回归量。|  
  
### <a name="regressors-in-linear-regression-models"></a>线性回归模型中的回归量  
 线性回归模型基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法。 但是，即使不使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法，任何决策树模型也都可以包含表示连续属性的回归的树或节点。  
  
 您无需指定连续列表示回归量。 即使不对列设置 REGRESSOR 标志， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 决策树算法也会将数据集分区成具有有意义模式的区域。 其差异是：如果设置建模标志，此算法将尝试查找 `a*C1 + b*C2 + ...` 形式的回归等式，以适合树中节点的模式。 将对剩余的总和进行计算，如果偏差过大，则在树中执行强制拆分。  
  
 例如，如果是将 income 用作属性来预测客户购买行为，并对 [Income] 列设置了 REGRESSOR 建模标志，则该算法将使用标准回归公式先尝试拟合该值。 如果偏差过大，则放弃使用回归公式，并根据其他一些属性对树进行拆分。 拆分后，决策树算法将尝试在每个分支中拟合收入的回归量。  
  
 可以使用 FORCED_REGRESSOR 参数来保证该算法将使用某一特定的回归量。 此参数可用于 Microsoft 决策树算法和 Microsoft 线性回归算法。  
  
## <a name="requirements"></a>要求  
 线性回归模型必须包含一个键列、若干输入列和至少一个可预测列。  
  
### <a name="input-and-predictable-columns"></a>输入列和可预测列  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 线性回归算法支持下表中列出的特定输入列和可预测列。 有关内容类型在用于挖掘模型中时的含义的详细信息，请参阅[内容类型（数据挖掘）](../../analysis-services/data-mining/content-types-data-mining.md)。  
  
|列|内容类型|  
|------------|-------------------|  
|输入属性|Continuous、Cyclical、Key、Table 和 Ordered|  
|可预测属性|Continuous、Cyclical 和 Ordered|  
  
> [!NOTE]  
>  支持**Cyclical** 和 **Ordered** content types are supported, but the algorithm treats them as discrete values 和 does not perform special processing.  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 线性回归算法](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)   
 [线性回归模型查询示例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)   
 [线性回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
