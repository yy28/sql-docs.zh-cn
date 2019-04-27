---
title: 比较预测的预测模型 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ead8a1fe-60d8-4017-8fb8-6fe32168e46d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 26cc445d3bad5c628628353d5c0c84ffa4755e97
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63066328"
---
# <a name="comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial"></a>比较预测模型的预测（数据挖掘中级教程）
  在本教程前面的步骤中，您已经创建了多个时序模型：  
  
-   区域和型号的每个组合的预测，只基于单个型号和区域的数据。  
  
-   每个区域的预测，基于更新的数据。  
  
-   在全球范围对所有型号的预测，基于聚合数据。  
  
-   在北美区域对 M200 型号的预测，基于聚合模型。  
  
 为了汇总时序预测的功能，您将查看变化以了解在使用用于扩展数据或替换数据的选项时是如何影响预测结果的。  
  
 [EXTEND_MODEL_CASES](#bkmk_EXTEND)  
  
 [REPLACE_MODEL_CASES](#bkmk_REPLACE)  
  
##  <a name="bkmk_EXTEND"></a> 添加数据后比较原始结果和结果  
 让我们看一下只是 M200 产品系列，太平洋地区，若要查看使用新数据更新模型如何影响结果的数据。 请记住原始数据序列在 2004 年 6 月结束，我们获取了 7 月、8 月和 9 月的新数据。  
  
-   第一列显示添加的新数据。  
  
-   第二列显示基于原始数据序列 7 月和之后的预测。  
  
-   第三列显示基于扩展数据的预测。  
  
|**M200 Pacific**|更新的实际销售额数据|添加数据之前的预测|扩展的预测|  
|----------------------|-----------------------------|------------------------------------|-------------------------|  
|7-25-2008|**65**|32|**65**|  
|8-25-2008|**54**|37|**54**|  
|9-25-2008|**61**|32|**61**|  
|10-25-2008|无数据|36|32|  
|11-25-2008|无数据|31|41|  
|12-25-2008|无数据|34|32|  
  
 您将注意到使用扩展数据（此处用粗体显示）的预测完全重复实际数据点。 重复是默认设置。 只要有要使用的实际数据点，预测查询将返回实际值，仅在新的实际数据点用完后才输出新的预测值。  
  
 通常，算法给予新数据中的更改的权重比模型开始就有的数据更改的权重大。 但是，在这种情况下，新销售额数字表示仅相对前一阶段增长了 20-30％，因此仅对预测的销售额稍有增加，在销售预测再次向下后，与新数据之前的月份的趋势更为一致。  
  
##  <a name="bkmk_REPLACE"></a> 比较原始和交叉预测结果  
 请记住，原始挖掘模型揭示在区域之间以及产品系列之间存在较大的差异。 例如，M200 型号的销售很强，而 T1000 型号的销售在所有区域中都比较弱。 此外，某些系列没有太多数据。 序列不规则，这表示它们没有相同的起始点。  
  
 ![时序预测 M200 和 T1000 数量](../../2014/tutorials/media/6series-defaultforecasting.gif "时序预测 M200 和 T1000 数量")  
  
 因此，当您基于通用模型进行预测时预测如何变化，该模型基于全球范围内的销售额而非原始数据集？ 为了确保您没有丢失任何信息或进行错误预测，可以将结果存储到一个表中，将预测表与历史记录数据表联接，然后用图形表示两组历史记录数据和预测数据。  
  
 以下关系图仅基于一个产品系列（M200）。 该图比较了初始挖掘模型的预测值和使用聚合挖掘模型的预测值。  
  
 ![比较预测的 Excel 图表](../../2014/tutorials/media/m200-predictions-compared.gif "比较预测的 Excel 图表")  
  
 从此关系图中，您可以看到聚合挖掘模型在使得各个数据序列中的波动尽量最小的同时保持整体范围和值的趋势。  
  
## <a name="conclusion"></a>结束语  
 您学习了如何创建和自定义可用于预测的时序模型。  
  
 您学习了通过使用 EXTEND_MODEL_CASES 参数添加新数据和创建预测来更新时序模型，而不必重新处理它们。  
  
 您学习了通过使用 REPLACE_MODEL_CASES 参数和将模型应用到不同数据序列，创建可用于交叉预测的模型。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘中级教程&#40;Analysis Services-数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [时序模型查询示例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
