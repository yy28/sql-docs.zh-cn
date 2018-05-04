---
title: 则 IsTestCase (DMX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IsTestCase
dev_langs:
- DMX
helpviewer_keywords:
- IsTestCase function
ms.assetid: 7ff4b895-9bb4-4e26-ab1b-c9049cfc2291
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 8754f92f96740c02470081b12b8fe1056c2fe04a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>注释  
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
  
## <a name="see-also"></a>另请参阅  
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [数据挖掘查询](../analysis-services/data-mining/data-mining-queries.md)   
 [定型集和测试数据集](../analysis-services/data-mining/training-and-testing-data-sets.md)  
  
  
