---
title: SystemGetClusterCrossValidationResults (Analysis Services-数据挖掘) |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SystemGetClusterCrossValidationResults
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
ms.assetid: 79de9b81-9f2e-4f20-ace9-e3b19d6a9759
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1880a3a1a6de67c953dabd6b58b383fe5ea8e7be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="systemgetclustercrossvalidationresults-analysis-services---data-mining"></a>SystemGetClusterCrossValidationResults（Analysis Services - 数据挖掘）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  将挖掘结构分区为指定数目的交叉部分，并对每个分区为模型定型，然后返回每个分区的准确性指标。  
  
 **注意** ：此存储过程只能用于包含至少一个聚类分析模型的挖掘结构。 若要对非聚类模型进行交叉验证，必须使用 [SystemGetCrossValidationResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
SystemGetClusterCrossValidationResults(  
<structure name>,   
[,<mining model list>]  
,<fold count>}  
,<max cases>  
<test list>])  
```  
  
## <a name="arguments"></a>参数  
 *挖掘结构 (mining structure)*  
 当前数据库中挖掘结构的名称。  
  
 （必需）  
  
 *挖掘模型列表*  
 要验证的挖掘模型的逗号分隔列表。  
  
 如果未指定挖掘模型列表，则对与指定结构关联的所有聚类分析模型执行交叉验证。  
  
> [!NOTE]  
>  若要对非聚类模型进行交叉验证，必须使用单独的存储过程 [SystemGetCrossValidationResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)。  
  
 （可选）  
  
 *折叠计数 (fold count)*  
 整数，指定将数据集分入的分区的数目。 最小值为 2。 最大倍数为 **maximum integer** 或事例数，取两者中的较低者。  
  
 每个分区包含的事例数都将大致为：最大事例数/折叠计数。  
  
 没有默认值。  
  
> [!NOTE]  
>  折叠数会在很大程度上影响执行交叉验证所需的时间。 如果选择的数目过高，查询可能需要运行较长时间，在某些情况下，服务器可能会停止响应或超时。  
  
 （必需）  
  
 *最大事例数*  
 整数，指定可以测试的最大事例数。  
  
 值 0 指示将使用数据源中的所有事例。  
  
 如果指定的数目大于数据集中的实际事例数，则使用数据源中的所有事例。  
  
 （必需）  
  
 *测试列表*  
 指定测试选项的字符串。  
  
 **注意** ：此参数留待将来使用。  
  
 （可选）  
  
## <a name="return-type"></a>返回类型  
 返回类型表包含每个分区的分数以及所有模型的聚合。  
  
 下表介绍返回的列。  
  
|列名|Description|  
|-----------------|-----------------|  
|ModelName|所测试模型的名称。|  
|AttributeName|可预测列的名称。 对于分类模型，始终为 **null**。|  
|AttributeState|可预测列中的指定目标值。 对于分类模型，始终为 **null.**|  
|PartitionIndex|一个从 1 开始的索引，用于标识结果适用于哪个分区。|  
|PartitionSize|一个整数，指示每个分区中包含的事例数。|  
|测试|所执行测试的类型。|  
|度量值|测试返回的度量值的名称。 每个模型的度量值都取决于可预测值的类型。 有关每个度量值的定义，请参阅[交叉验证（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)。<br /><br /> 有关为每个可预测类型返回的度量值的列表，请参阅 [交叉验证报表中的度量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。|  
|“值”|指定的测试度量值的值。|  
  
## <a name="remarks"></a>注释  
 若要为整个数据集返回准确性指标，请使用 [SystemGetClusterAccuracyResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)。  
  
 此外，如果挖掘模型已分区为若干折叠，可以使用 [SystemGetClusterAccuracyResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何将挖掘结构分区为三个折叠，然后测试与该挖掘结构关联的两个聚类分析模型。  
  
 代码的第三行列出了要测试的特定挖掘模型。 如果未指定此列表，则使用与该结构关联的所有聚类分析模型。  
  
 代码的第四行指定了折叠数，第五行指定了要使用的最大事例数。  
  
 由于这些模型是聚类分析模型，您不需要指定可预测属性或值。  
  
```  
CALL SystemGetClusterCrossValidationResults(  
[v Target Mail],  
[Cluster 1], [Cluster 2],  
3,  
10000  
)  
```  
  
 示例结果：  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|测试|度量值|“值”|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|群集 1|||1|3025|群集|事例可能性|0.930524511864121|  
|群集 1|||2|3025|群集|事例可能性|0.919184178430778|  
|分类 1|||3|3024|群集|事例可能性|0.929651120490248|  
|Cluster 2|||1|1289|群集|事例可能性|0.922789726933607|  
|Cluster 2|||2|1288|群集|事例可能性|0.934865535691068|  
|Cluster 2|||3|1288|群集|事例可能性|0.924724595688798|  
  
## <a name="requirements"></a>需求  
 从 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] 开始，交叉验证仅在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中可用。  
  
## <a name="see-also"></a>另请参阅  
 [SystemGetCrossValidationResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services-数据挖掘&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults & #40;Analysis Services-数据挖掘 & #41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
