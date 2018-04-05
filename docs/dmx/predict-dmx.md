---
title: 预测 (DMX) |Microsoft 文档
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
- PREDICT
dev_langs:
- DMX
helpviewer_keywords:
- Predict function
ms.assetid: f02ff4b3-9bd7-409d-ad14-ead67b3206c4
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 448507936bab886a8d081ee487ab323a3a4a2ef4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **预测**函数将返回预测的值或值，指定的列集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>适用范围  
 标量列引用或表列引用。  
  
## <a name="return-type"></a>返回类型  
 \<标量列引用 >  
  
 或多个  
  
 \<表的列引用 >  
  
 返回类型取决于应用此函数的列的类型。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 和 INCLUDE_STATISTICS 只适用于表列引用；EXCLUDE_NULL 和 INCLUDE_NULL 只适用于标量列引用。  
  
## <a name="remarks"></a>Remarks  
 选项包括 EXCLUDE_NULL（默认值）、INCLUDE_NULL、INCLUSIVE、EXCLUSIVE（默认值）、INPUT_ONLY 和 INCLUDE_STATISTICS。  
  
> [!NOTE]  
>  对时序模型，预测函数不支持 INCLUDE_STATISTICS。  
  
 INCLUDE_NODE_ID 参数在结果中返回 $NODEID 列。 NODE_ID 是为特定事例而对其执行预测的内容节点。 使用上表中的列的预测时，此参数是可选的。  
  
  *n* 参数适用于表中的列。 该参数根据预测类型设置返回的行数。 如果基础列是序列，则会调用**PredictSequence**函数。 如果基础列是时序，则会调用**PredictTimeSeries**函数。 对于关联类型的预测，它调用**PredictAssociation**函数。  
  
 **预测**函数支持多态性。  
  
 下面的替代缩写形式较为常用：  
  
-   [性别] 是的备用**预测**([性别] EXCLUDE_NULL)。  
  
-   [产品购买] 是的备用**预测**([产品购买] EXCLUDE_NULL，独占)。  
  
    > [!NOTE]  
    >  此函数的返回类型本身被视为列引用。 这意味着，**预测**函数可以用作其他采用列引用作为参数的函数中的自变量 (除**预测**函数本身)。  
  
 将 INCLUDE_STATISTICS 传递给预测表值的列上添加列**$Probability**和**$Support**向得到的表。 这些列说明了关联的嵌套表记录的存在概率。  
  
## <a name="examples"></a>示例  
 下面的示例使用预测函数可返回最有可能一起销售 Adventure Works 数据库中的四个产品。 针对关联规则挖掘模型预测函数，因为它会自动使用**PredictAssociation**函数如前面所述。  
  
```  
SELECT  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,4)  
FROM     [Association]  
```  
  
 示例结果：  
  
 虽然此查询返回的单个数据行 `Expression` 仅有一列，但该列包含下面的嵌套表。  
  
|“模型”|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016331743|0.252695851192499|  
|Water Bottle|2866|0.192620471805901|0.175205052318795|  
|Patch Kit|2113|0.142012232004839|0.132389356196586|  
|Mountain Tire Tube|1992|0.133879965051415|0.125304947722259|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
