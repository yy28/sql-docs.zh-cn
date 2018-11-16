---
title: IsTestCase (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b7e80f8a9dfb82f13350b94b310690a081fae1de
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606637"
---
# <a name="istestcase-dmx"></a>IsTestCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  指示事例是否用作指定数据挖掘模型或挖掘结构的测试事例。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>结果类型  
 返回 **，则返回 true**案例是否属于测试数据集; 否则为**false**。  
  
## <a name="remarks"></a>备注  
 如果使用数据挖掘向导创建挖掘结构和相关的挖掘模型，则默认情况下将留出 30% 的事例用作测试数据集。 其余事例用于定型数据挖掘模型。 同一测试数据集可用于所有基于该结构的模型。 但是，如果使用 DMX 创建挖掘模型，则默认情况下所有数据都将用于定型模型，而不创建任何测试集。 若要允许创建测试数据集，必须设置 WITH HOLDOUT 子句的参数。  
  
 通过查看 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> 和 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> 属性的值，可以确定是否已对特定的挖掘结构创建测试集。  
  
> [!NOTE]  
>  如果想要使用的则 IsTrainingCase 或则 IsTestCase 函数以返回处于特定模型的事例的相关详细信息，必须对模型启用钻取功能。 有关详细信息，请参阅 [对挖掘模型启用钻取](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)。  
  
 若要返回定型数据集的一部分的情况下，使用函数[IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)。  
  
## <a name="examples"></a>示例  
 下面的示例使用`Targeted Mailing`中创建的挖掘结构[数据挖掘基础教程](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。 查询将返回该结构中所有用于测试的事例。  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 有关如何查询数据挖掘中使用的事例的详细信息，请参阅[SELECT FROM&#60;模型&#62;。用例&#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md)并[FROM&#60;结构&#62;。用例](../dmx/select-from-structure-cases.md)。  
  
## <a name="see-also"></a>请参阅  
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [数据挖掘查询](../analysis-services/data-mining/data-mining-queries.md)   
 [定型数据集和测试数据集](../analysis-services/data-mining/training-and-testing-data-sets.md)  
  
  
