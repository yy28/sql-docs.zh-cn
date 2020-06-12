---
title: BottomPercent （DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6fdb1563f644b544fd9c0bd2ee0857bf4b403329
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669836"
---
# <a name="bottompercent-dmx"></a>BottomPercent (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  以升序的形式返回表中最下面的几行，这些行的累积合计至少达到指定百分比。  
  
## <a name="syntax"></a>语法  
  
```  
  
BottomPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="arguments"></a>参数  
 *\<表表达式>*  
 嵌套表列或表值表达式的名称。  
  
 *\<排名表达式>*  
 嵌套表中的列，或计算结果为列的表达式。  
  
 *\<>百分比*  
 指示总目标百分比的双精度数。  
  
## <a name="result-type"></a>结果类型  
 表。  
  
## <a name="remarks"></a>注解  
 **BottomPercent**函数以升序顺序返回最底层的行。 排名基于 \< 每行> 参数的排名表达式的计算值，因此， \< 排名表达式> 值的总和至少为 \< 百分比> 参数指定的给定百分比。 当仍满足指定的百分比值时， **BottomPercent**将返回尽可能少数量的元素。  
  
## <a name="examples"></a>示例  
 下面的示例创建一个针对您在[数据挖掘基础教程](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)中生成的关联模型的预测查询。  
  
 若要了解 BottomPercent 的工作原理，最好先执行只返回嵌套表的预测查询。  
  
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
  
 BottomPercent 函数获取此查询的结果，并返回与指定百分比求和的最小值行。  
  
```  
SELECT   
BottomPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 BottomPercent 函数的第一个参数是表列的名称。 在此示例中，通过调用 Predict 函数并使用 INCLUDE_STATISTICS 参数来返回嵌套表。  
  
 BottomPercent 函数的第二个参数是用于对结果进行排序的嵌套表中的列。 在此示例中，INCLUDE_STATISTICS 选项返回 $SUPPORT、$PROBABILTY 和 $ADJUSTED PROBABILITY 列。 此示例使用 $SUPPORT，因为支持值不带有小数，所以很容易进行验证。  
  
 BottomPercent 函数的第三个参数以 double 形式指定百分比。 若要获取表示支持的最下面百分之五十的行，可键入 50。  
  
 示例结果：  
  
|型号|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
  
 **注意**提供此示例只是为了说明 BottomPercent 的用法。 运行此查询可能需要很长时间，具体取决于数据集的大小。  
  
> [!WARNING]  
>  在用于计算百分比的值包含负数时，用于 TOPPERCENT 和 BOTTOMPERCENT 的 MDX 函数可能会生成意外结果。 此行为并不影响 DMX 函数。 有关详细信息，请参阅[BottomPercent &#40;MDX&#41;](../mdx/bottompercent-mdx.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40;DMX&#41; 函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [函数 &#40;DMX&#41;](../dmx/functions-dmx.md)  
  
  
