---
title: "SystemGetCrossValidationResults (Analysis Services-数据挖掘) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SystemGetCrossValidationResults
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
ms.assetid: f70c3337-c930-434a-b278-caf1ef0c3b3b
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 499e62070cb0ec0fed8e814c926d915f7e69bbe3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="systemgetcrossvalidationresults-analysis-services---data-mining"></a>SystemGetCrossValidationResults（Analysis Services - 数据挖掘）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]为指定数量的剖面，挖掘结构的分区训练模型为每个分区，然后返回每个分区的准确性度量值。  
  
> [!NOTE]  
>  此存储过程不能用于交叉验证聚类分析模型，也不能交叉验证使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 时序算法或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 顺序分析和聚类分析算法生成的模型。 若要交叉验证聚类分析模型，可使用单独的存储过程 [SystemGetClusterCrossValidationResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SystemGetCrossValidationResults(  
<mining structure>  
[, <mining model list>]  
,<fold count>  
,<max cases>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>参数  
 *挖掘结构 (mining structure)*  
 当前数据库中挖掘结构的名称。  
  
 （必需）  
  
 *挖掘模型列表*  
 要验证的挖掘模型的逗号分隔列表。  
  
 如果模型名称中包含任何对于标识符名称无效的字符，则必须将名称用方括号括起来。  
  
 如果未指定挖掘模型列表，则对与指定结构关联并包含可预测属性的所有模型执行交叉验证。  
  
> [!NOTE]  
>  若要交叉验证聚类分析模型，必须使用单独的存储过程 [SystemGetClusterCrossValidationResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)。  
  
 （可选）  
  
 *折叠计数 (fold count)*  
 整数，指定将数据集分入的分区的数目。 最小值为 2。 最大倍数为 **maximum integer** 或事例数，取两者中的较低者。  
  
 每个分区包含的事例数都将大致为：最大事例数/折叠计数。  
  
 没有默认值。  
  
> [!NOTE]  
>  折叠数会在很大程度上影响执行交叉验证所需的时间。 如果选择的数目过高，查询可能需要运行较长时间，在某些情况下，服务器会停止响应或超时。  
  
 （必需）  
  
 *最大事例数*  
 整数，指定可以在所有折叠间进行测试的最大事例数。  
  
 值 0 指示将使用数据源中的所有事例。  
  
 如果指定的值大于数据集中的实际事例数，则使用数据源中的所有事例。  
  
 没有默认值。  
  
 （必需）  
  
 *目标属性*  
 包含可预测属性的名称的字符串。 可预测属性可以是挖掘模型的列、嵌套表列或嵌套表键列。  
  
> [!NOTE]  
>  仅在运行时才会验证目标属性是否存在。  
  
 （必需）  
  
 *目标状态*  
 指定要预测的值的公式。 如果指定了目标值，将只针对指定的值收集指标。  
  
 如果未指定值，或为 **null**，则针对每个预测最有可能的状态计算指标。  
  
 默认值为 **null**。  
  
 如果指定的值对于指定属性无效，或公式不是指定属性的正确类型，则在验证期间会引发错误。  
  
 （可选）  
  
 目标阈值  
 **Double** 大于 0 且小于 1。 指示要将指定目标状态的预测视为正确而必须取得的最小概率分数。  
  
 概率小于或等于此值的预测将被视为不正确。  
  
 如果未指定值，或为 **null**，则使用最有可能的状态，无论其概率分数如何。  
  
 默认值为 **null**。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]如果你设置不会引发错误*状态阈值*为 0.0，但你应永远不会使用此值。 实际上，阈值为 0.0 意味着概率为 0% 的预测也将视为正确。  
  
 （可选）  
  
 *测试列表*  
 指定测试选项的字符串。  
  
 **注意** ：此参数留待将来使用。  
  
 （可选）  
  
## <a name="return-type"></a>返回类型  
 返回的行集包含每个模型中每个分区的分数。  
  
 下表对行集中的列进行了说明。  
  
|列名|Description|  
|-----------------|-----------------|  
|ModelName|所测试模型的名称。|  
|AttributeName|可预测列的名称。|  
|AttributeState|可预测列中的指定目标值。 如果此值为 **null**，则使用了最有可能的预测。<br /><br /> 如果此列包含一个值，则只针此值评估模型的准确性。|  
|PartitionIndex|一个从 1 开始的索引，用于标识结果适用于哪个分区。|  
|PartitionSize|一个整数，指示每个分区中包含的事例数。|  
|测试|所执行测试的类别。 有关各类别以及每个类别中包含的测试的说明，请参阅 [交叉验证报表中的度量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。|  
|度量值|测试返回的度量值的名称。 每个模型的度量值都取决于可预测值的类型。 有关每个度量值的定义，请参阅[交叉验证（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)。<br /><br /> 有关为每个可预测类型返回的度量值的列表，请参阅 [交叉验证报表中的度量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。|  
|ReplTest1|指定的测试度量值的值。|  
  
## <a name="remarks"></a>Remarks  
 若要为完整数据集返回准确性指标，请使用 [SystemGetAccuracyResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)。  
  
 如果挖掘模型已分区为若干折叠，可以使用 [SystemGetAccuracyResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何将进行交叉验证的挖掘结构分区为两个折叠，然后测试与该挖掘结构 `[v Target Mail]`关联的两个挖掘模型。  
  
 代码的第三行列出了要测试的挖掘模型。 如果未指定此列表，则使用与该结构关联的所有非聚类分析模型。 代码的第四行指定了分区数。 由于没有为 *max cases*指定值，因此将使用挖掘结构中的所有事例，并在各分区间平均分布。  
  
 第五行指定了可预测属性 Bike Buyer，第六行指定了要预测的值 1（表示“是，将要购买”）。  
  
 第七行的 NULL 值指示没有必须满足的最小概率限制。 因此，在评估准确性时将使用具有非零概率的第一个预测。  
  
```  
CALL SystemGetCrossValidationResults(  
[v Target Mail],  
[Target Mail DT], [Target Mail NB],  
2,  
'Bike Buyer',  
1,  
NULL  
)  
```  
  
 示例结果：  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|测试|度量值|ReplTest1|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Target Mail DT|Bike Buyer|@shouldalert|@shouldalert|500|分类|真正|144|  
|Target Mail DT|Bike Buyer|@shouldalert|@shouldalert|500|分类|假正|105|  
|Target Mail DT|Bike Buyer|@shouldalert|@shouldalert|500|分类|真负|186|  
|Target Mail DT|Bike Buyer|@shouldalert|@shouldalert|500|分类|假负|65|  
|Target Mail DT|Bike Buyer|@shouldalert|@shouldalert|500|可能性|对数评分|-0.619042807138345|  
|Target Mail DT|Bike Buyer|@shouldalert|@shouldalert|500|可能性|提升|0.0740963734002671|  
|Target Mail DT|Bike Buyer|@shouldalert|@shouldalert|500|可能性|均方根误差|0.346946279977653|  
|Target Mail DT|Bike Buyer|@shouldalert|2|500|分类|真正|162|  
|Target Mail DT|Bike Buyer|@shouldalert|2|500|分类|假正|86|  
|Target Mail DT|Bike Buyer|@shouldalert|2|500|分类|真负|165|  
|Target Mail DT|Bike Buyer|@shouldalert|2|500|分类|假负|87|  
|Target Mail DT|Bike Buyer|@shouldalert|2|500|可能性|对数评分|-0.654117781086519|  
|Target Mail DT|Bike Buyer|@shouldalert|2|500|可能性|提升|0.038997399132084|  
|Target Mail DT|Bike Buyer|@shouldalert|2|500|可能性|均方根误差|0.342721344892651|  
  
## <a name="requirements"></a>要求  
 从 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] 开始，交叉验证仅在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中可用。  
  
## <a name="see-also"></a>另请参阅  
 [SystemGetCrossValidationResults](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services-数据挖掘 &#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services-数据挖掘 &#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
