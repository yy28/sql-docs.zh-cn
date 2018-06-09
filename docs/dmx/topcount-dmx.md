---
title: TopCount (DMX) |Microsoft 文档
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 182c83cf6b2850941c2f21924395c0ebe160db01
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842770"
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  按指定数量返回最前面的行，并以表达式指定的降序排列。  
  
## <a name="syntax"></a>语法  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>适用范围  
 一个表达式，返回一个表，如\<表列引用 >，或函数返回一个表。  
  
## <a name="return-type"></a>返回类型  
 \<表表达式 >  
  
## <a name="remarks"></a>Remarks  
 由提供的值\<排名表达式 > 自变量确定中提供的行级别的递减顺序\<表表达式 > 自变量，并在指定的最顶层的行数\<计数 > 返回自变量。  
  
 TopCount 函数引入最初了启用关联的预测，并通常情况下，生成与包含语句相同的结果**选择前**和**ORDER BY**子句。 如果你使用，您将获得更好的性能，关联的预测**预测 (DMX)** 函数，该支持多个预测，以返回的规范函数。  
  
 但是，有一些你可能仍需要使用 TopCount 的情形。 例如，不支持 DMX**顶部**在嵌套 select 语句中的限定符。 [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md)函数也不支持添加**顶部**。  
  
## <a name="examples"></a>示例  
 以下示例是针对关联模型，你通过使用生成的预测查询[Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)。 查询返回相同的结果，但第一个示例使用 TopCount，和第二个示例使用预测函数。  
  
 若要了解 TopCount 的工作原理，它可能是第一次执行返回嵌套的表的预测查询很有帮助。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  在本示例中，作为输入而提供的值包含一个单引号；因此，必须通过在该值前面加一个单引号来进行转义。 如果不熟悉有关插入转义符的语法，则您可以使用预测查询生成器创建查询。 从下拉列表中选择值时，会为您插入所需的转义符。 有关详细信息，请参阅[在数据挖掘设计器中创建单独查询](../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md)。  
  
 示例结果：  
  
|“模型”|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Water Bottle|2866|0.192620472|0.175205052|  
|Patch kit|2113|0.142012232|0.132389356|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
  
 TopCount 函数采用此查询的结果，并返回指定的数目的最小值行。  
  
```  
SELECT   
TopCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 TopCount 函数的第一个参数是一个表列的名称。 在此示例中，嵌套的表返回通过调用预测函数并使用 INCLUDE_STATISTICS 自变量。  
  
 TopCount 函数的第二个参数是使用对结果进行排序的嵌套表中的列。 在此示例中，INCLUDE_STATISTICS 选项返回 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY 列。 该示例使用 $SUPPORT 对结果进行排名。  
  
 TopCount 函数的第三个参数指定要返回整数形式的行数。 若要获取按 $SUPPORT 排序的前三个产品，请键入 3。  
  
 示例结果：  
  
|“模型”|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29…|0.25…|  
|Water Bottle|2866|0.19…|0.17…|  
|Patch kit|2113|0.14…|0.13…|  
  
 但是，此查询类型可能会影响生产设置的性能。 这是因为此查询返回算法的所有预测集，对这些预测进行排序并返回前 3 个产品。  
  
 以下示例提供返回相同结果但执行速度明显加快的替代语句。 此示例将 TopCount 替换接受作为自变量数目的预测的预测函数。 此示例还使用 **$SUPPORT**关键字来直接检索嵌套的表列。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 结果包含按支持值排序的前 3 个预测。 您可以将 $SUPPORT 替换为 $PROBABILITY 或 $ADJUSTED_PROBABILITY，以便返回按概率或调整后的概率排名的预测。 有关详细信息，请参阅**预测 (DMX)**。  
  
## <a name="see-also"></a>请参阅  
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [常规预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)   
 [TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)   
 [TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)  
  
  
