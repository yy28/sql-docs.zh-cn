---
title: "交叉验证报表中的度量值 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- root mean square error [data mining]
- cross-validation [data mining]
- mean absolute error [data mining]
- log score [data mining]
- likelihood [data mining]
ms.assetid: a07b1665-7f72-4266-82a4-43a91ae2571d
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 52d3932d577ed93c3c1ab4122323a04a1c27771e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="measures-in-the-cross-validation-report"></a>交叉验证报表中的度量值
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]交叉验证期间[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]将挖掘结构中的数据划分为多个剖面，然后以迭代方式测试的结构和任何关联的挖掘模型。 基于此分析，它将为该结构和每个模型输出一组标准的准确性度量值。  
  
 该报表包含有关数据中折叠数以及每个折叠中的数据量的一些基本信息，还包含描述数据分布的一组一般性的指标。 通过比较各交叉部分的一般性的指标，您可以评估该结构或模型的可靠性。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还为挖掘模型显示一组详细的度量值。 这些度量值依赖于模型类型以及要分析的属性的类型：例如，是离散的还是连续的。  
  
 本节提供“交叉验证”报表中包含的度量值列表以及各度量值的含义。 有关如何计算各度量值的详细信息，请参阅[交叉验证公式](../../analysis-services/data-mining/cross-validation-formulas.md)。  
  
## <a name="list-of-measures-in-the-cross-validation-report"></a>交叉验证报表中度量值的列表  
 下表列出了交叉验证报表中出现的度量值。 这些度量值按测试类型进行分组，测试类型在下表的左侧列中提供。 右侧列列出了度量值在报表中出现时的名称，并且简要解释了其含义。  
  
|测试类型|度量值和说明|  
|---------------|-------------------------------|  
|群集|应用于聚类分析模型的度量值|  
||**事例可能性**:<br />                      该度量值通常指示某个事例属于特定分类的可能性。 对于交叉验证，将对分数求和，然后除以事例数，因此在这里，分数是平均事例可能性。|  
|分类|应用于分类模型的度量值|  
||**真正**/**真负**/**假正**/**假负**：<br /><br /> 预测的状态与目标状态匹配并且预测概率大于指定的阈值的分区中行或值的计数。<br /><br /> 排除对于目标属性具有缺失值的事例，这意味着所有值的计数可能未加总。|  
||**通过/失败**：<br />                      预测的状态与目标状态匹配并且预测概率值大于 0 的分区中行或值的计数。|  
|可能性|可能性度量值适用于多种模型类型。|  
||**提升**:<br />                      测试事例中实际预测概率与边缘概率的比率。 排除对目标属性具有缺失值的行。<br /><br /> 此度量值通常显示使用模型时目标结果的概率提高的程度。|  
||**均方根误差**:<br />                      所有分区事例的平均误差的平方根除以分区中的事例数，不包括目标属性缺失值的行。<br /><br /> RMSE 是预测模型的一种流行的估计器。 该分数对每个事例的余数求平均值，以便生成模型误差的单个指示器。|  
||**对数评分**:<br />                      每个事例的实际概率的对数和除以输入数据集中的行数，不包括目标属性缺失值的行。<br /><br /> 由于概率用小数表示，因此，对数分数始终是负数。 接近 0 的数字是较好的分数。 原始分数可以具有非常不规则或扭曲的分布，而对数评分与百分比相似。|  
|估计|仅适用于估算模型的度量值，将预测连续数值属性。|  
||**均方根误差**:<br />                      预测值与实际值进行比较时的平均误差。<br /><br /> RMSE 是预测模型的一种流行的估计器。 该分数对每个事例的余数求平均值，以便生成模型误差的单个指示器。|  
||**平均绝对误差**:<br />                      预测值与实际值进行比较时的平均误差，计算为误差的绝对值之和的平均值。<br /><br /> 平均绝对误差用于理解预测与实际值在整体上的接近程度。 较小的分数意味着预测更准确。|  
||**对数评分**:<br />                      每个事例的实际概率的对数和除以输入数据集中的行数，不包括目标属性缺失值的行。<br /><br /> 由于概率用小数表示，因此，对数分数始终是负数。 接近 0 的数字是较好的分数。 原始分数可以具有非常不规则或扭曲的分布，而对数评分与百分比相似。|  
|聚合|聚合度量值指示每个分区的结果中的方差。|  
||**意味着**:<br />                      特定度量值的分区值的平均值。|  
||**标准偏差**:<br />                      一个模型的所有分区中相对于特定度量值平均值的偏差的平均值。<br /><br /> 对于交叉验证，此分数值越高，则意味着折叠之间的差异越大。|  
  
## <a name="see-also"></a>另请参阅  
 [测试和验证（数据挖掘）](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
