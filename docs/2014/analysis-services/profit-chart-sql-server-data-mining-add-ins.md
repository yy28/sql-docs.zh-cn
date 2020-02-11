---
title: 利润图（SQL Server 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy chart
- profit chart
- mining models, charting
- mining models, testing
ms.assetid: 5c902543-4da9-4db3-99d5-4ce04c43d7ef
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 32ee1539c734c549f89d5b3db8ec4add467a72b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070593"
---
# <a name="profit-chart-sql-server-data-mining-add-ins"></a>利润图（SQL Server 数据挖掘外接程序）
  ![“数据挖掘”功能区中的“利润图”按钮](media/dmc-profitchart.gif "“数据挖掘”功能区中的“利润图”按钮")  
  
 利润图显示与使用挖掘模型相关联的预计利润增长，以确定公司应在业务方案中联系的客户。 图表的 Y 轴表示利润，而 X 轴表示公司所联系总体的百分比。 典型的利润图显示利润增长到一个最高点，利润在达到该点后将随所联系总体的增大而减少。  
  
## <a name="configuring-the-profit-chart"></a>配置利润图  
 准确性图表仅对预测正确与否的概率进行评估，但利润图则同时包含有关根据预测采取措施的结果的现实认知。 为此，运行向导时您要考虑指定下列因素：  
  
-   **人口数**  
  
     数据集中用于创建提升图的事例数。 例如，潜在客户数。  
  
-   **固定成本**  
  
     与业务问题关联的固定成本。 如果此参数用于目标邮件解决方案，则该成本不依赖于所拨打的销售电话数或所发送的促销邮件数等变量。  
  
-   **单项成本**  
  
     除固定成本之外的成本，可以与每个客户联系相关联。 例如，促销邮件或销售电话。  
  
-   **每个人收入**  
  
     与每个成功销售相关联的收入金额。  
  
## <a name="using-the-profit-chart-wizard"></a>使用利润图向导  
 若要创建利润图，必须参考现有数据挖掘模型。 您可以通过单击 "**管理模型**" 或 "**浏览**" 来浏览模型，查找与数据匹配的模型，以查看有关已使用的算法和挖掘模型中的列的详细信息。  
  
 有关详细信息，请参阅[在 Excel 中浏览模型 &#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)和[管理模型 &#40;SQL Server 数据挖掘外接程序&#41;](manage-models-sql-server-data-mining-add-ins.md)。  
  
#### <a name="to-create-a-profit-chart"></a>创建利润图  
  
1.  选择一个现有模型。  
  
2.  指定要预测的列，如果需要，还请指定目标值。  
  
3.  选择源数据，这意味着数据将传递给模型来创建预测。 此数据应不同于创建模型所用的数据。  
  
4.  将新（源）日期中的列映射到数据挖掘模型中所用的列。 如果列名称类似，向导将自动映射它们。  
  
5.  输入向导所需的开销信息：固定成本、单项成本、总体以及预期收入。  
  
6.  （可选）可以输入一系列渐变的成本（单击浏览 **（...）** 按钮）。 例如，增加发送的邮件数量时，发送一封邮件的成本可能会降低，因此，您可以根据邮件数量输入不同成本，向导将自动调整每个样本大小的成本。  
  
7.  向导将创建包含针对该模型的成本收益分析的图表。  
  
### <a name="requirements"></a>要求  
 如果预测的是离散数值，则必须选择要预测的精确目标值。  
  
## <a name="understanding-the-profit-chart"></a>了解利润图  
 利润图包含一条灰色竖线，单击该图表中的某一位置可以移动该竖线。 "**挖掘图例**" 显示与图表上的灰色线条位置相关联的分数、总体正确和预测概率。 如果通过使用灰线选择了图表中的最大利润点，可以使用预测概率值确定联系客户的概率阈值。  
  
 例如，如果利润曲线的峰值位于总体的 55% 处，并且相关联的预测概率为 20%，这表明，若要获取最大利润，应只联系其答复概率被预测为 20% 或更高的客户。  
  
## <a name="see-also"></a>另请参阅  
 [验证模型和使用模型进行预测 &#40;Excel 数据挖掘外接程序&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
