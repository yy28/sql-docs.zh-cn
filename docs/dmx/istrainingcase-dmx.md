---
title: "则 IsTrainingCase (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
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
ms.topic: language-reference
f1_keywords:
- IsTrainingCase
dev_langs:
- DMX
helpviewer_keywords:
- IsTrainingCase function
ms.assetid: 63eab315-e743-470d-9c4c-edfc3f4058a3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ed062df083d4c11c635f9241eac38b4ec4406a32
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="istrainingcase-dmx"></a>IsTrainingCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指示事例是否用作指定数据挖掘模型或挖掘结构的定型事例。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsTrainingCase()  
```  
  
## <a name="result-type"></a>结果类型  
 返回**true**如果这种情况是定型数据集; 的一部分否则为**false**。  
  
## <a name="remarks"></a>備註  
 如果使用数据挖掘向导创建挖掘结构和相关的挖掘模型，则默认情况下将留出 30% 的事例用作测试数据集。 您指定的数据源中的其余事例用于定型模型。 但是，如果使用数据挖掘扩展插件 (DMX) 创建挖掘模型，则默认情况下所有数据都将用于定型模型，而不创建任何测试集。 若要允许创建测试数据集，必须设置 WITH HOLDOUT 子句的参数。  
  
 通过查看 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> 和 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> 属性的值，可以确定是否已将特定数据挖掘结构中的数据分区为测试集和定型集。  
  
> [!NOTE]  
>  如果你想要使用则 IsTrainingCase 或则 IsTestCase 函数来返回模型中的事例的详细信息，必须对模型启用钻取功能。 有关详细信息，请参阅 [对挖掘模型启用钻取](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)。  
  
 若要返回属于的测试数据集的情况下，使用该函数[则 IsTestCase &#40; DMX &#41;](../dmx/istestcase-dmx.md)。  
  
## <a name="examples"></a>示例  
 下面的示例使用聚类分析的数据挖掘模型中的目标邮递方案从[Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。 查询仅返回用于定型挖掘模型的那些事例。 而且，定型事例仅限于 40 岁以下的客户。  
  
```  
SELECT *  
FROM [TM Clustering].CASES  
WHERE IsTrainingCase()  
AND [Age] <40  
```  
  
 如何查询数据挖掘中使用的事例的其他示例，请参阅[SELECT FROM #60; 模型 &#62;。用例 &#40; DMX &#41;](../dmx/select-from-model-cases-dmx.md)和[SELECT FROM #60; 结构 &#62;。用例](../dmx/select-from-structure-cases.md)。  
  
## <a name="see-also"></a>另請參閱  
 [定型集和测试数据集](../analysis-services/data-mining/training-and-testing-data-sets.md)   
 [函数 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [数据挖掘查询](../analysis-services/data-mining/data-mining-queries.md)  
  
  

