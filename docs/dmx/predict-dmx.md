---
title: 预测 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb939c45d298117fa81b05d6188aa3a4c5cd7c4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008160"
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **Predict**函数将返回预测的值或一组值，指定列。  
  
## <a name="syntax"></a>语法  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>适用范围  
 标量列引用或表列引用。  
  
## <a name="return-type"></a>返回类型  
 \<标量列引用 >  
  
 或  
  
 \<表的列引用 >  
  
 返回类型取决于应用此函数的列的类型。  
  
> [!NOTE]  
>  INCLUSIVE、EXCLUSIVE、INPUT_ONLY 和 INCLUDE_STATISTICS 只适用于表列引用；EXCLUDE_NULL 和 INCLUDE_NULL 只适用于标量列引用。  
  
## <a name="remarks"></a>备注  
 选项包括 EXCLUDE_NULL（默认值）、INCLUDE_NULL、INCLUSIVE、EXCLUSIVE（默认值）、INPUT_ONLY 和 INCLUDE_STATISTICS。  
  
> [!NOTE]  
>  对于时序模型，预测函数不支持 INCLUDE_STATISTICS。  
  
 INCLUDE_NODE_ID 参数在结果中返回 $NODEID 列。 NODE_ID 是为特定事例而对其执行预测的内容节点。 使用上表中的列的预测时，此参数是可选的。  
  
 *N*参数适用于表中的列。 该参数根据预测类型设置返回的行数。 如果基础列是序列，则会调用**PredictSequence**函数。 如果基础列是时序，则会调用**PredictTimeSeries**函数。 对于关联类型的预测，它将调用**PredictAssociation**函数。  
  
 **Predict**函数支持多态性。  
  
 下面的替代缩写形式较为常用：  
  
-   [性别] 是用于替代项**Predict**([Gender]，EXCLUDE_NULL)。  
  
-   [Products Purchases] 用于替代**Predict**([Products Purchases]，EXCLUDE_NULL，EXCLUSIVE)。  
  
    > [!NOTE]  
    >  此函数的返回类型本身被视为列引用。 这意味着**Predict**函数可以用作列引用作为参数的其他函数中的自变量 (除**Predict**函数本身)。  
  
 将 INCLUDE_STATISTICS 传递给预测表值的列上添加的列 **$Probability**并 **$Support**生成的表。 这些列说明了关联的嵌套表记录的存在概率。  
  
## <a name="examples"></a>示例  
 以下示例使用 Predict 函数可返回四个产品中最有可能一起销售的 Adventure Works 数据库。 该函数针对关联规则挖掘模型预测，因为它会自动使用**PredictAssociation**函数如前面所述。  
  
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
  
## <a name="see-also"></a>请参阅  
 [数据挖掘扩展插件&#40;DMX&#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [通用预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
