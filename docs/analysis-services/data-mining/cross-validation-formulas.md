---
title: "交叉验证公式 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fd1ea582-29a1-4154-8de2-47bab3539b4d
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9ae8b6960e04fbbe04a7a536cc75c361d36c907f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="cross-validation-formulas"></a>交叉验证公式
  生成交叉验证报表后，它将包含每个模型的准确性度量值，具体取决于挖掘模型的类型（即，用于创建模型的算法）、可预测属性的数据类型和可预测属性值（如果有）。  
  
 本节列出了交叉验证报表中使用的度量值，并介绍了计算方法。  
  
 有关按模型类型细分准确性度量值，请参阅 [交叉验证报表中的度量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。  
  
## <a name="formulas-used-for-cross-validation-measures"></a>用于交叉验证度量值的公式  
  
> [!NOTE]  
>  **重要：** 这些准确性度量值是针对每个目标属性计算的。 对于每个属性，您可指定或省略目标值。 如果数据集中的事例不具有任何目标属性值，则会将该事例视为包含名为“缺失值” 的特殊值。 在针对特定目标属性计算准确性度量值时，具有缺失值的行不计算在内。 注意，由于分数是针对每个属性分别计算的；如果目标属性存在值，但其他属性缺失值，则不会影响目标属性的分数。  
  
|度量值|适用范围|实现|  
|-------------|----------------|--------------------|  
|**真正**|离散属性，值已指定|满足以下条件的事例计数：<br /><br /> 事例包含目标值。<br /><br /> 模型已预测事例包含目标值。|  
|**真负**|离散属性，值已指定|满足以下条件的事例计数：<br /><br /> 事例不包含目标值。<br /><br /> 模型已预测事例不包含目标值。|  
|**假正**|离散属性，值已指定|满足以下条件的事例计数：<br /><br /> 实际值等于目标值。<br /><br /> 模型已预测事例包含目标值。|  
|**假负**|离散属性，值已指定|满足以下条件的事例计数：<br /><br /> 实际值不等于目标值。<br /><br /> 模型已预测事例不包含目标值。|  
|**通过/失败**|离散属性，无指定的目标|满足以下条件的事例计数：<br /><br /> 如果具有最高概率的预测状态与输入状态相同并且概率大于 **“状态阈值”**的值，则通过。<br /><br /> 否则，将会失败。|  
|**提升**|离散属性。 可以指定目标值，但目标值并不是必需的。|具有目标属性值的所有行的平均对数可能性，其中，每个事例的对数可能性计算为 Log(ActualProbability/MarginalProbability)。 为了计算该平均值，对数可能性值的总和将除以输入数据集的行数（但不包括缺少目标属性值的那些行）。<br /><br /> 提升可以为正值，也可以为负值。 正值意味着有效模型优于随机推测。|  
|**对数评分**|离散属性。 可以指定目标值，但目标值并不是必需的。|每个事例的实际概率的对数和除以输入数据集中的行数，不包括缺少目标属性值的行。<br /><br /> 由于概率用小数表示，因此，对数分数始终是负数。 接近 0 的分数是较好的分数。|  
|**事例可能性**|分类|所有事例的分类可能性得分的总和除以分区中的事例数，不包括缺少目标属性值的行。|  
|**平均绝对误差**|连续属性|分区中所有事例的绝对误差的总和除以分区中的事例数。|  
|**均方根误差**|连续属性|分区的平均平方误差的平方根。|  
|**均方根误差**|离散属性。 可以指定目标值，但目标值并不是必需的。|概率得分补数的平方的平方根除以分区中的事例数，不包括缺少目标属性值的行。|  
|**均方根误差**|离散属性，无指定的目标。|概率得分补数的平方的平方根除以分区中的事例数，不包括缺少目标属性值的事例。|  
  
## <a name="see-also"></a>另请参阅  
 [测试和验证（数据挖掘）](../../analysis-services/data-mining/testing-and-validation-data-mining.md)   
 [交叉验证（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)  
  
  

