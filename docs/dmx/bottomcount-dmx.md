---
title: BottomCount （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0bbd80998f7a6fd74f76f641cc16fe81ba715dde
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68889851"
---
# <a name="bottomcount-dmx"></a>BottomCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  按指定数量返回最底部的行，以表达式指定的升序排列。  
  
## <a name="syntax"></a>语法  
  
```  
  
BottomCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>应用于  
 返回表的表达式，如\<表列引用> 或返回表的函数。  
  
## <a name="return-type"></a>返回类型  
 \<表表达式>  
  
## <a name="remarks"></a>备注  
 \<排名表达式> 参数提供的值确定在\<表表达式> 参数中提供的行的排名的递增顺序，并返回在\<count> 参数中指定的最底部的行数。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个针对使用[数据挖掘基础教程](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)生成的关联模型的预测查询。  
  
 若要了解 BottomCount 的工作原理，最好先执行只返回嵌套表的预测查询。  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  在本示例中，作为输入而提供的值包含一个单引号；因此，必须通过在该值前面加一个单引号来进行转义。 如果不熟悉有关插入转义符的语法，则您可以使用预测查询生成器创建查询。 从下拉列表中选择值时，会为您插入所需的转义符。 有关详细信息，请参阅[在数据挖掘设计器中创建单独查询](https://docs.microsoft.com/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer)。  
  
 示例结果：  
  
|型号|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
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
  
 BottomCount 函数获取此查询的结果，并返回与指定百分比求和的最小值行。  
  
```  
SELECT   
BottomCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 BottomCount 函数的第一个参数是表列的名称。 在此示例中，通过调用 Predict 函数并使用 INCLUDE_STATISTICS 参数来返回嵌套表。  
  
 BottomCount 函数的第二个参数是用于对结果进行排序的嵌套表中的列。 在此示例中，INCLUDE_STATISTICS 选项返回 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY 列。 此示例使用 $SUPPORT，因为支持值不带有小数，所以很容易进行验证。  
  
 BottomCount 函数的第三个参数指定行数。 若要获取按 $SUPPORT 排序的排名最低的最后三个行，请键入 3。  
  
 示例结果：  
  
|型号|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
  
 **注意**提供此示例只是为了说明如何使用 BottomCount。 运行此查询可能需要很长时间，具体取决于数据集的大小。  
  
## <a name="see-also"></a>另请参阅  
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [&#40;DMX&#41;的常规预测函数](../dmx/general-prediction-functions-dmx.md)   
 [BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)   
 [BottomSum &#40;DMX&#41;](../dmx/bottomsum-dmx.md)   
 [TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)  
  
  
