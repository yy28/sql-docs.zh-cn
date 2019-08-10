---
title: TopCount (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d4b91b06470c9cb22e98ac76ea52494728a7ca11
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893104"
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  按指定数量返回最前面的行，并以表达式指定的降序排列。  
  
## <a name="syntax"></a>语法  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>适用范围  
 返回表的表达式, 如\<表列引用 > 或返回表的函数。  
  
## <a name="return-type"></a>返回类型  
 \<表表达式 >  
  
## <a name="remarks"></a>备注  
 \<排名表达式 > 参数提供的值确定\<在表表达式 > 参数中提供的行的降序顺序, 以及在中指定的最上面的行的数目。\<返回 > 参数的计数。  
  
 最初引入的 TopCount 函数用于启用关联预测, 并且通常会生成与包含**SELECT TOP**和**ORDER BY**子句的语句相同的结果。 如果使用**预测 (DMX)** 函数, 则可以获得更好的关联预测性能, 此函数支持指定要返回的预测数。  
  
 但是, 在某些情况下, 你可能仍需要使用 TopCount。 例如, DMX 不支持在子选择语句中使用**顶级**限定符。 [ &#40;PredictHistogram DMX&#41; ](../dmx/predicthistogram-dmx.md)函数也不支持添加**TOP**。  
  
## <a name="examples"></a>示例  
 下面的示例是针对使用[数据挖掘基础教程](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)生成的关联模型的预测查询。 查询返回相同的结果, 但第一个示例使用 TopCount, 第二个示例使用预测函数。  
  
 若要了解 TopCount 的工作原理, 最好先执行只返回嵌套表的预测查询。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  在本示例中，作为输入而提供的值包含一个单引号；因此，必须通过在该值前面加一个单引号来进行转义。 如果不熟悉有关插入转义符的语法，则您可以使用预测查询生成器创建查询。 从下拉列表中选择值时，会为您插入所需的转义符。 有关详细信息, 请参阅[在数据挖掘设计器中创建单独查询](https://docs.microsoft.com/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer)。  
  
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
  
 TopCount 函数获取此查询的结果, 并返回指定数目的最小值行。  
  
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
  
 TopCount 函数的第一个参数是表列的名称。 在此示例中, 通过调用 Predict 函数并使用 INCLUDE_STATISTICS 参数来返回嵌套表。  
  
 TopCount 函数的第二个参数是用于对结果进行排序的嵌套表中的列。 在此示例中，INCLUDE_STATISTICS 选项返回 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY 列。 该示例使用 $SUPPORT 对结果进行排名。  
  
 TopCount 函数的第三个参数指定要返回的行数 (整数)。 若要获取按 $SUPPORT 排序的前三个产品，请键入 3。  
  
 示例结果：  
  
|“模型”|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29 。|0.25 。|  
|Water Bottle|2866|0.19 。|0.17 。|  
|Patch kit|2113|0.14 。|0.13 。|  
  
 但是，此查询类型可能会影响生产设置的性能。 这是因为此查询返回算法的所有预测集，对这些预测进行排序并返回前 3 个产品。  
  
 以下示例提供返回相同结果但执行速度明显加快的替代语句。 此示例将 TopCount 替换为 Predict 函数, 该函数接受许多预测作为参数。 此示例还使用 **$SUPPORT**关键字直接检索嵌套表列。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 结果包含按支持值排序的前 3 个预测。 您可以将 $SUPPORT 替换为 $PROBABILITY 或 $ADJUSTED_PROBABILITY，以便返回按概率或调整后的概率排名的预测。 有关详细信息, 请参阅**预测 (DMX)** 。  
  
## <a name="see-also"></a>请参阅  
 [函数&#40;DMX&#41;](../dmx/functions-dmx.md)   
 [一般预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)   
 [TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)   
 [TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)  
  
  
