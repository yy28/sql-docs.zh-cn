---
description: Predict (DMX)
title: 预测 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4f53f331b078fce4f02e548a83a145dce8ba6a91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426199"
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  **Predict**函数为指定列返回一个预测值或一组值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>适用于  
 标量列引用或表列引用。  
  
## <a name="return-type"></a>返回类型  
 \<scalar column reference>  
  
 或  
  
 \<table column reference>  
  
 返回类型取决于应用此函数的列的类型。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 和 INCLUDE_STATISTICS 只适用于表列引用；EXCLUDE_NULL 和 INCLUDE_NULL 只适用于标量列引用。  
  
## <a name="remarks"></a>备注  
 选项包括 EXCLUDE_NULL（默认值）、INCLUDE_NULL、INCLUSIVE、EXCLUSIVE（默认值）、INPUT_ONLY 和 INCLUDE_STATISTICS。  
  
> [!NOTE]  
>  对于时序模型，Predict 函数不支持 INCLUDE_STATISTICS。  
  
 INCLUDE_NODE_ID 参数在结果中返回 $NODEID 列。 NODE_ID 是为特定事例而对其执行预测的内容节点。 在对表列使用 Predict 时，此参数是可选的。  
  
 *N*参数适用于表列。 该参数根据预测类型设置返回的行数。 如果基础列是序列，则它会调用 **PredictSequence** 函数。 如果基础列是时序，它将调用 **PredictTimeSeries** 函数。 对于关联类型的预测，它会调用 **PredictAssociation** 函数。  
  
 **Predict**函数支持多态性。  
  
 下面的替代缩写形式较为常用：  
  
-   [性别] 是 **预测** ( [性别] EXCLUDE_NULL) 的替代方法。  
  
-   [产品购买] 是 **预测** ( [产品购买]，EXCLUDE_NULL，独家) 的替代方法。  
  
    > [!NOTE]  
    >  此函数的返回类型本身被视为列引用。 这意味着，可以将 **Predict** 函数用作作为参数的其他函数中的参数 (除了 **预测** 函数本身) 。  
  
 将 INCLUDE_STATISTICS 传递给表值列的预测时，会将 **$Probability** 和 **$Support** 的列添加到生成的表中。 这些列说明了关联的嵌套表记录的存在概率。  
  
## <a name="examples"></a>示例  
 下面的示例使用 Predict 函数返回艾德公司数据库中最有可能一起销售的四种产品。 由于函数是根据关联规则挖掘模型进行预测的，因此它会自动使用前面所述的 **PredictAssociation** 函数。  
  
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
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数 ](../dmx/general-prediction-functions-dmx.md)  
  
  
