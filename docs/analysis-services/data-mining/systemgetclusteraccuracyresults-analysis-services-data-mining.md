---
title: "SystemGetClusterAccuracyResults (Analysis Services-数据挖掘) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- SystemGetClusterAccuracyResults
- cross-validation [data mining]
ms.assetid: e1701738-50d5-46b4-b406-f1e800545abb
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8e31548023acfa5ef3c202b978d7be3c46d788a0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="systemgetclusteraccuracyresults-analysis-services---data-mining"></a>SystemGetClusterAccuracyResults（Analysis Services - 数据挖掘）
  返回挖掘结构和相关聚类分析模型的交叉验证准确性指标。  
  
 此存储过程将为作为单个分区的整个数据集返回指标。 若要将数据集分区为交叉部分，并返回每个分区的度量值，请使用 [SystemGetClusterCrossValidationResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)。  
  
> [!NOTE]  
>  此存储过程只对聚类分析模型有效。 对于非聚类分析模型，使用 [SystemGetAccuracyResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SystemGetClusterAccuracyResults(  
<mining structure>   
[,<mining model list>]  
,<data set>  
,<test list>])  
```  
  
## <a name="arguments"></a>参数  
 *挖掘结构 (mining structure)*  
 当前数据库中挖掘结构的名称。  
  
 （必需）  
  
 *挖掘模型列表*  
 要验证的模型的逗号分隔列表。  
  
 默认值为 **null**，表示使用所有适用的模型。 使用默认值时，非聚类分析模型将自动从处理候选列表中排除。  
  
 （可选）  
  
 *数据集 (data set)*  
 一个整数值，指示挖掘结构中要用于测试的分区。 此值派生自位掩码，该位掩码表示以下值的总和，其中任一单个值是可选的：  
  
|||  
|-|-|  
|定型事例|0x0001|  
|测试事例|0x0002|  
|模型筛选器|0x0004|  
  
 有关可能的值的完整列表，请参阅本主题的“备注”部分。  
  
 （必需）  
  
 *测试列表*  
 指定测试选项的字符串。 此参数留待将来使用。  
  
 （可选）  
  
## <a name="return-type"></a>返回类型  
 一个包含每个分区的分数以及所有模型的聚合的表。  
  
 下表列出了 **SystemGetClusterAccuracyResults**返回的列。 若要了解有关如何解释存储过程返回的信息的详细信息，请参阅 [交叉验证报表中的度量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。  
  
|列名|Description|  
|-----------------|-----------------|  
|ModelName|所测试模型的名称。 **All** 指示结果为所有模型的聚合。|  
|AttributeName|不适用于聚类分析模型。|  
|AttributeState|不适用于聚类分析模型。|  
|PartitionIndex|指示分区的数字。<br /><br /> 对于此存储过程，该数字始终为 0。|  
|PartitionCases|一个整数，指示已测试的事例数。|  
|测试|所执行测试的类型。|  
|度量值|测试返回的度量值的名称。 每个模型的度量值取决于模型类型以及可预测值的类型。<br /><br /> 有关为每个可预测类型返回的度量值的列表，请参阅[交叉验证报表中的度量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。<br /><br /> 有关每个度量值的定义，请参阅[交叉验证（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)。|  
|“值”|指示分类事例可能性的概率分数。|  
  
## <a name="remarks"></a>注释  
 下表提供了一些值的示例，您可以使用这些值指定用于交叉验证的挖掘结构中的数据。 如果要将测试事例用于交叉验证，挖掘结构必须已包含测试数据集。 有关如何在创建挖掘结构时定义测试数据集的信息，请参阅 [定型数据集和测试数据集](../../analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
|整数值|Description|  
|-------------------|-----------------|  
|1|仅使用定型事例。|  
|2|仅使用测试事例。|  
|3|同时使用定型事例和测试事例。|  
|4|无效组合。|  
|5|仅使用定型事例，并应用模型筛选器。|  
|6|仅使用测试事例，并应用模型筛选器。|  
|7|同时使用定型事例和测试事例，并应用模型筛选器。|  
  
 有关可以在其中使用交叉验证的应用场景的详细信息，请参阅[测试和验证（数据挖掘）](../../analysis-services/data-mining/testing-and-validation-data-mining.md)。  
  
## <a name="examples"></a>示例  
 此示例返回名为 `Cluster 1` 和 `Cluster 2`的两个聚类分析模型的准确性度量值，这两个模型与 vTargetMail 挖掘结构关联。 第四行的代码指示结果应只基于测试事例，而不使用任何可能与每个模型关联的筛选器。  
  
```  
CALL SystemGetClusterAccuracyResults (  
[vTargetMail],  
[Cluster 1], [Cluster 2],  
2  
)  
```  
  
 示例结果：  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|测试|度量值|“值”|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|分类 1|||0|5545|群集|事例可能性|0.796514342249313|  
|Cluster 2|||0|5545|群集|事例可能性|0.732122471228572|  
  
## <a name="requirements"></a>要求  
 从 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] 开始，交叉验证仅在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中可用。  
  
## <a name="see-also"></a>另请参阅  
 [SystemGetCrossValidationResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services-数据挖掘 &#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services-数据挖掘 &#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemClusterGetAccuracyResults](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  

