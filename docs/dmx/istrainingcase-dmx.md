---
title: 则 istrainingcase （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e6bdfe1e3d22a2d2c4752e43df254231725fa447
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969448"
---
# <a name="istrainingcase-dmx"></a>IsTrainingCase (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指示事例是否用作指定数据挖掘模型或挖掘结构的定型事例。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsTrainingCase()  
```  
  
## <a name="result-type"></a>结果类型  
 如果事例是定型数据集的一部分，则返回**true** ;否则**为 false**。  
  
## <a name="remarks"></a>备注  
 如果使用数据挖掘向导创建挖掘结构和相关的挖掘模型，则默认情况下将留出 30% 的事例用作测试数据集。 您指定的数据源中的其余事例用于定型模型。 但是，如果使用数据挖掘扩展插件 (DMX) 创建挖掘模型，则默认情况下所有数据都将用于定型模型，而不创建任何测试集。 若要允许创建测试数据集，必须设置 WITH HOLDOUT 子句的参数。  
  
 通过查看 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> 和 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> 属性的值，可以确定是否已将特定数据挖掘结构中的数据分区为测试集和定型集。  
  
> [!NOTE]  
>  如果要使用则 istrainingcase 或则 istestcase 函数返回有关模型中事例的详细信息，则必须对该模型启用钻取功能。 有关详细信息，请参阅 [对挖掘模型启用钻取](https://docs.microsoft.com/analysis-services/data-mining/enable-drillthrough-for-a-mining-model)。  
  
 若要返回测试数据集中的事例，请使用函数[则 istestcase &#40;DMX&#41;](../dmx/istestcase-dmx.md)。  
  
## <a name="examples"></a>示例  
 下面的示例使用[数据挖掘基础教程](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)中的目标邮件方案中的聚类分析数据挖掘模型。 查询仅返回用于定型挖掘模型的那些事例。 而且，定型事例仅限于 40 岁以下的客户。  
  
```  
SELECT *  
FROM [TM Clustering].CASES  
WHERE IsTrainingCase()  
AND [Age] <40  
```  
  
 有关如何查询数据挖掘中使用的事例的其他示例，请参阅[SELECT FROM &#60;model&#62;。&#40;DMX&#41;的事例](../dmx/select-from-model-cases-dmx.md)，并[从 &#60;结构&#62; 中进行选择。事例](../dmx/select-from-structure-cases.md)。  
  
## <a name="see-also"></a>另请参阅  
 [定型和测试数据集](https://docs.microsoft.com/analysis-services/data-mining/training-and-testing-data-sets)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [数据挖掘查询](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)  
  
  
