---
title: 散点图（Analysis Services 数据挖掘） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- charts [Analysis Services]
- mining models [Analysis Services], validating
- scatter charts
- regression algorithms [Analysis Services]
ms.assetid: 166812ec-fd1c-47c8-88db-d5041142be91
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d3319b72f1c3b37805a653d1f315aa0a3363521a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082940"
---
# <a name="scatter-plot-analysis-services---data-mining"></a>散点图（Analysis Services - 数据挖掘）
  “散点图” ** 以图形方式对照显示数据中的实际值与模型预测的值。 其沿 X 轴显示实际值，沿 Y 轴显示预测值。 该图还显示一条显示完美预测的线，在这条线上预测值和实际值完全匹配。 某个点与该条理想 45 度角线的距离指示进行的预测的准确程度。  
  
## <a name="understanding-the-scatter-plot"></a>了解散点图  
 考虑下面这个模型：公司的市场部根据其在促销电子邮件中发送的链接的点击数来预测日销售额。 由于点击数和销售额均为连续数值，因此，可以以图形方式将点击数显示为独立变量，将销售额显示为依赖变量。 这样，图中的直线显示预期线性关系，而散布在该直线周围的点显示实际数据偏离预期值的程度。 一目了然，该分析指出一组结果与某个特定输入相关联的紧密程度，以及所生成的模型与理想模型之间有多大差异  
  
## <a name="interpreting-the-results"></a>解释结果  
 下面的关系图显示散点图的一个示例，该图是为刚刚说明的应用场景而创建的。  
  
 ![线性回归的散点图示例](../media/scatterplot-callctr.gif "线性回归的散点图示例")  
  
 将鼠标悬停在散布在该直线周围的任一点上方即可在工具提示中查看预测值和实际值。 散点图没有 **“挖掘图例”** ，但该图表本身包含一个显示与该模型关联的分数的图例。 有关解释分数的详细信息，请参阅[线性回归模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)。  
  
 可以将该图表的可视表示复制到剪贴板，但无法复制基础数据或公式。 如果希望查看对应于此条线的回归公式，则可以对该模型创建内容查询。 有关详细信息，请参阅 [线性回归模型查询示例](linear-regression-model-query-examples.md)。  
  
## <a name="restrictions-on-scatter-plots"></a>针对散点图的限制  
 如果在 **“输入选择”** 选项卡上选择的模型包含连续可预测属性，则只能创建散点图。 不必进行其他选择；基于模型和属性类型在 **“提升图”** 选项卡中自动显示散点图图表类型。  
  
 尽管时序模型预测连续数值，但是您不能使用散点图度量时序模型的准确性。 可以使用其他方法，例如保留一部分历史记录数据。 有关详细信息，请参阅[时序模型查询示例](time-series-model-query-examples.md)。  
  
## <a name="related-content"></a>相关内容  
 下列主题包含有关如何生成和使用散点图以及相关准确性图表的详细信息。  
  
|主题|链接|  
|------------|-----------|  
|提供如何创建目标邮递模型的提升图的演练。|[数据挖掘基础教程](../../tutorials/basic-data-mining-tutorial.md)<br /><br /> [利用提升图测试准确性 &#40;基本数据挖掘教程&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)|  
|说明相关的图表类型。|[Analysis Services &#40;提升图表&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [利润图 &#40;Analysis Services 数据挖掘&#41;](profit-chart-analysis-services-data-mining.md)<br /><br /> [分类矩阵 &#40;Analysis Services 数据挖掘&#41;](classification-matrix-analysis-services-data-mining.md)|  
|说明如何将交叉验证用于挖掘模型和挖掘结构。|[交叉验证 &#40;Analysis Services 数据挖掘&#41;](cross-validation-analysis-services-data-mining.md)|  
|说明用于创建提升图和其他准确性图表的步骤。|[测试和验证任务以及操作方法 &#40;数据挖掘&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>另请参阅  
 [测试和验证 &#40;数据挖掘&#41;](testing-and-validation-data-mining.md)  
  
  
