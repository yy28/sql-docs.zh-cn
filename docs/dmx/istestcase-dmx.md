---
title: 则 IsTestCase (DMX) |Microsoft 文档
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eefb9269a3eb0dc7a6b95e84accb4c68c6737a13
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2018
ms.locfileid: "34841790"
---
# <a name="istestcase-dmx"></a>IsTestCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指示事例是否用作指定数据挖掘模型或挖掘结构的测试事例。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>结果类型  
 返回**true**如果这种情况是测试数据集; 的一部分否则为**false**。  
  
## <a name="remarks"></a>Remarks  
 如果使用数据挖掘向导创建挖掘结构和相关的挖掘模型，则默认情况下将留出 30% 的事例用作测试数据集。 其余事例用于定型数据挖掘模型。 同一测试数据集可用于所有基于该结构的模型。 但是，如果使用 DMX 创建挖掘模型，则默认情况下所有数据都将用于定型模型，而不创建任何测试集。 若要启用创建的测试数据集，必须设置与维持子句的参数。  
  
 通过查看 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> 和 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> 属性的值，可以确定是否已对特定的挖掘结构创建测试集。  
  
> [!NOTE]  
>  如果你想要使用则 IsTrainingCase 或则 IsTestCase 函数返回在特定模型的事例的详细信息，必须对模型启用钻取功能。 有关详细信息，请参阅 [对挖掘模型启用钻取](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)。  
  
 若要返回属于的训练数据集的情况下，使用该函数[则 IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)。  
  
## <a name="examples"></a>示例  
 下面的示例使用`Targeted Mailing`中创建的挖掘结构[Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。 查询将返回该结构中所有用于测试的事例。  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 有关如何查询数据挖掘中使用的事例的详细信息，请参阅[SELECT FROM&#60;模型&#62;。用例&#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md)和[SELECT FROM&#60;结构&#62;。用例](../dmx/select-from-structure-cases.md)。  
  
## <a name="see-also"></a>请参阅  
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [数据挖掘查询](../analysis-services/data-mining/data-mining-queries.md)   
 [定型数据集和测试数据集](../analysis-services/data-mining/training-and-testing-data-sets.md)  
  
  
