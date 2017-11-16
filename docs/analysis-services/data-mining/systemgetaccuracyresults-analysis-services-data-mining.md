---
title: "SystemGetAccuracyResults (Analysis Services-数据挖掘) |Microsoft 文档"
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
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- SystemGetAccuracyResults
- cross-validation [data mining]
ms.assetid: 54ff584c-c6ce-4c31-9515-0a645719bd1a
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6b2eca528b40afd905661e2508e93529159b8627
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="systemgetaccuracyresults-analysis-services---data-mining"></a>SystemGetAccuracyResults（Analysis Services - 数据挖掘）
  返回挖掘结构和所有相关模型（不包括聚类分析模型）的交叉验证准确性指标。  
  
 此存储过程将为作为单个分区的整个数据集返回指标。 若要将数据集分区为交叉部分，并返回每个分区的度量值，请使用 [SystemGetCrossValidationResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)。  
  
> [!NOTE]  
>  使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法生成的模型不支持此存储过程。 此外，对于聚类分析模型，请使用单独的存储过程 [SystemGetClusterAccuracyResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SystemGetAccuracyResults(<mining structure>,   
[,<mining model list>]  
,<data set>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>参数  
 *挖掘结构 (mining structure)*  
 当前数据库中挖掘结构的名称。  
  
 （必需）  
  
 *模型列表*  
 要验证的模型的逗号分隔列表。  
  
 默认值为 **null**。 这意味着将使用所有适用的模型。 使用默认值时，聚类分析模型将自动从处理候选列表中排除。  
  
 （可选）  
  
 *数据集 (data set)*  
 一个整数值，指示挖掘结构中用于测试的分区。 此值派生自位掩码，该位掩码表示以下值的总和，其中任一单个值是可选的：  
  
|||  
|-|-|  
|定型事例|0x0001|  
|测试事例|0x0002|  
|模型筛选器|0x0004|  
  
 有关可能的值的完整列表，请参阅本主题的“备注”部分。  
  
 （必需）  
  
 *目标属性*  
 包含可预测对象的名称的字符串。 可预测对象可以是挖掘模型的列、嵌套表列或嵌套表键列。  
  
 （必需）  
  
 *目标状态*  
 包含要预测的特定值的字符串。  
  
 如果指定了值，将针对该特定状态收集指标。  
  
 如果未指定值，或指定 Null，将针对每个预测最有可能的状态计算指标。  
  
 默认值为 **null**。  
  
 （可选）  
  
 *目标阈值*  
 0.0 到 1 之间的数字，用于指定预测值视为正确的最小概率。  
  
 默认值为 **null**，表示所有的预测都视为正确。  
  
 （可选）  
  
 *测试列表*  
 指定测试选项的字符串。 此参数留待将来使用。  
  
 （可选）  
  
## <a name="return-type"></a>返回类型  
 返回的行集包含每个分区的分数以及所有模型的聚合。  
  
 下表列出了 **GetValidationResults**返回的列。  
  
|列名|Description|  
|-----------------|-----------------|  
|Model|所测试模型的名称。 **All** 指示结果为所有模型的聚合。|  
|AttributeName|可预测列的名称。|  
|AttributeState|可预测列中的目标值。<br /><br /> 如果此列包含一个值，则只针对指定的状态收集指标。<br /><br /> 如果未指定此值，或为 Null，则针对每个预测最有可能的状态计算指标。|  
|PartitionIndex|表示结果适用的分区。<br /><br /> 对于此过程，始终为 0。|  
|PartitionCases|一个整数，指示事例集，基于中的行数*\<数据集 >*参数。|  
|测试|所执行测试的类型。|  
|度量值|测试返回的度量值的名称。 每个模型的度量值取决于模型类型以及可预测值的类型。<br /><br /> 有关为每个可预测类型返回的度量值的列表，请参阅[交叉验证报表中的度量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。<br /><br /> 有关每个度量值的定义，请参阅[交叉验证（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)。|  
|“值”|指定的度量值的值。|  
  
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
 此示例返回单个决策树模型 `v Target Mail DT`的准确性度量值，该模型与 `vTargetMail` 挖掘结构关联。 第四行的代码指示结果应基于通过每个模型特定的筛选器为对应模型筛选的测试事例。  `[Bike Buyer]` 指定要预测的列，下一行的 1 指示仅针对特定值 1（表示“是，将要购买”）对模型进行评估。  
  
 代码的最后一行指定状态阈值为 0.5。 这意味着，计算准确性时，概率大于 50% 的预测就应视为“准确”的预测。  
  
```  
CALL SystemGetAccuracyResults (  
[vTargetMail],  
[vTargetMail DT],  
6,  
'Bike Buyer',  
1,  
0.5  
)  
```  
  
 示例结果：  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|测试|度量值|“值”|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|v Target Mail DT|Bike Buyer|1|0|1638|分类|真正|605|  
|v Target Mail DT|Bike Buyer|1|0|1638|分类|假正|177|  
|v Target Mail DT|Bike Buyer|1|0|1638|分类|真负|501|  
|v Target Mail DT|Bike Buyer|1|0|1638|分类|假负|355|  
|v Target Mail DT|Bike Buyer|1|0|1638|可能性|对数评分|-0.598454638753028|  
|v Target Mail DT|Bike Buyer|1|0|1638|可能性|提升|0.0936717116894395|  
|v Target Mail DT|Bike Buyer|1|0|1638|可能性|均方根误差|0.361630800104946|  
  
## <a name="requirements"></a>要求  
 从 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] 开始，交叉验证仅在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中可用。  
  
## <a name="see-also"></a>另请参阅  
 [SystemGetCrossValidationResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services-数据挖掘 &#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  

