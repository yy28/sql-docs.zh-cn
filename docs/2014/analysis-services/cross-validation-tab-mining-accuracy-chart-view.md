---
title: 交叉验证选项卡 （挖掘准确性图表视图） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.crossvalidation.f1
ms.assetid: bd215a68-1ad7-4046-9c44-ec8e2be13a64
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f5a8508218ed6a2b4407943fe962959e3cd4f97d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086619"
---
# <a name="cross-validation-tab-mining-accuracy-chart-view"></a>“交叉验证”选项卡（“挖掘准确性图表”视图）
  通过使用交叉验证，可以将挖掘结构分区为交叉部分，并针对每个交叉部分循环定型和测试模型。 您可以指定要将数据划分成多少个折叠，每个折叠反过来会用作测试数据，而其余的数据用于为新模型定型。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 然后为每个模型生成一组标准准确性指标。 通过比较为每个交叉部分生成的模型的指标，可以清楚地了解挖掘模型对于整个数据集的可靠程度。  
  
 有关详细信息，请参阅[交叉验证（Analysis Services - 数据挖掘）](data-mining/cross-validation-analysis-services-data-mining.md)。  
  
> [!NOTE]  
>  交叉验证不能用于使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 顺序分析和聚类分析算法生成的模型。 如果对包含这些模型类型的挖掘结构运行报表，则这些模型将不会包括在报表中。  
  
## <a name="task-list"></a>任务列表  
  
-   指定折叠数。  
  
-   指定将用于交叉验证的最大事例数。  
  
-   指定可预测列。  
  
-   可以选择指定可预测状态。  
  
-   可以选择设置控制如何评估预测准确性的参数。  
  
-   单击“获取结果”可显示交叉验证的结果。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **折叠计数**  
 指定要创建的折叠数或分区数。 最小值是 2，这表示数据集的一半用于测试，另一半用于定型。  
  
 对于会话挖掘结构，最大值是 10。  
  
 如果挖掘结构存储在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的实例中，则最大值为 256。  
  
> [!NOTE]  
>  随着您增加折叠数，执行交叉验证所需的时间近似增加 n 倍。 如果事例数很大且“折叠计数”的值也很大，可能遇到性能问题。  
  
 **最大事例数**  
 指定将用于交叉验证的最大事例数。 任一特定折叠中的事例数等于 **“最大事例数”** 值除以 **“折叠计数”** 值。  
  
 如果使用 **0**，则源数据中的所有事例都用于交叉验证。  
  
 没有默认值。  
  
> [!NOTE]  
>  如果增加事例数，处理时间也会增加。  
  
 **目标属性**  
 从在所有模型中找到的可预测列的列表中选择列。 每次执行交叉验证时，只能选择一个可预测列。  
  
 若要只测试聚类分析模型，请选择 **“分类”**。  
  
 **目标状态**  
 键入一个值，或者从值的下拉列表中选择一个目标值。  
  
 默认值为 `null`，表示将测试所有状态。  
  
 对聚类分析模型禁用。  
  
 **目标****阈值**  
 指定一个 0 到 1 之间的值，该值指示预测概率，高于此概率的预测状态被计为正确。 可以使用 0.1 为增量来设置该值。  
  
 默认值为 `null`，表明将可能性最大的预测计为正确。  
  
> [!NOTE]  
>  虽然可以将值设置为 0.0，但这样做会增加处理时间，而且不会产生有意义的结果。  
  
 **获取结果**  
 单击此项将使用指定参数开始模型的交叉验证。  
  
 模型被分区为指定数量的折叠，并为每个折叠测试单独的模型。 因此，交叉验证可能需要一些时间才能返回结果。  
  
 有关如何解释交叉验证报告的结果的详细信息，请参阅 [交叉验证报表中的度量值](data-mining/measures-in-the-cross-validation-report.md)。  
  
## <a name="setting-the-accuracy-threshold"></a>设置准确性阈值  
 您可以通过设置 **“目标阈值”** 的值来控制度量预测准确性的标准。 阈值表示一种准确性栏。 为每个预测分配一个预测值正确的概率。 因此，如果将 **“目标阈值”**  的值设置为接近 1，则要求任一特定预测的概率很高才能计为准确的预测。 反之，如果将 **“目标阈值”**  设置为接近 0，则即使具有较低概率值的预测也会计为“准确的”预测。  
  
 由于任何预测的概率都取决于数据量以及所进行预测的类型，因此没有建议的阈值。 应查看不同概率级别的一些预测，以确定适用于您的数据的准确性栏。 进行此操作非常重要，因为对 **“目标阈值”**  设置的值会影响模型的度量准确性。  
  
 例如，假设对特定目标状态进行了三次预测，每次预测的概率分别是 0.05、0.15 和 0.8。 如果将阈值设置为 0.5，则仅有一个预测计为正确。 如果将 **“目标阈值”**  设置为 0.10，则两个预测将计为正确。  
  
 当**目标****阈值**设置为`null`，这是默认值，每个事例最有可能的预测计为正确。 在上面的示例中，0.05、0.15 和 0.8 是三个不同事例中的预测概率。 虽然概率差别较大，但每个预测都记为正确，因为每个事例只生成一个预测，而这些预测是这些事例的最佳预测。  
  
## <a name="see-also"></a>请参阅  
 [测试和验证（数据挖掘）](data-mining/testing-and-validation-data-mining.md)   
 [交叉验证（Analysis Services - 数据挖掘）](data-mining/cross-validation-analysis-services-data-mining.md)   
 [交叉验证报表中的度量值](data-mining/measures-in-the-cross-validation-report.md)   
 [数据挖掘存储过程（Analysis Services - 数据挖掘）](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  
