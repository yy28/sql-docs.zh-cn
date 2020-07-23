---
title: 则 istestcase （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ef4dc17d77707ca5bf08f935fb4a62f6d979ae05
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969532"
---
# <a name="istestcase-dmx"></a>IsTestCase (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指示事例是否用作指定数据挖掘模型或挖掘结构的测试事例。  
  
## <a name="syntax"></a>语法  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>结果类型  
 如果事例是测试数据集的一部分，则返回**true** ;否则**为 false**。  
  
## <a name="remarks"></a>备注  
 如果使用数据挖掘向导创建挖掘结构和相关的挖掘模型，则默认情况下将留出 30% 的事例用作测试数据集。 其余事例用于定型数据挖掘模型。 同一测试数据集可用于所有基于该结构的模型。 但是，如果使用 DMX 创建挖掘模型，则默认情况下所有数据都将用于定型模型，而不创建任何测试集。 若要允许创建测试数据集，必须使用 WITH 维持子句设置参数。  
  
 通过查看 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> 和 <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A> 属性的值，可以确定是否已对特定的挖掘结构创建测试集。  
  
> [!NOTE]  
>  如果要使用则 istrainingcase 或则 istestcase 函数返回有关特定模型中事例的详细信息，则必须对该模型启用钻取功能。 有关详细信息，请参阅 [对挖掘模型启用钻取](https://docs.microsoft.com/analysis-services/data-mining/enable-drillthrough-for-a-mining-model)。  
  
 若要返回定型数据集中的事例，请使用函数[则 istrainingcase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `Targeted Mailing` 在[数据挖掘基础教程](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)中创建的挖掘结构。 查询将返回该结构中所有用于测试的事例。  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 有关如何查询数据挖掘中使用的事例的详细信息，请参阅[SELECT FROM &#60;model&#62;。&#40;DMX&#41;的事例](../dmx/select-from-model-cases-dmx.md)，并[从 &#60;结构&#62; 中进行选择。事例](../dmx/select-from-structure-cases.md)。  
  
## <a name="see-also"></a>另请参阅  
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [数据挖掘查询](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)   
 [定型数据集和测试数据集](https://docs.microsoft.com/analysis-services/data-mining/training-and-testing-data-sets)  
  
  
