---
title: 选择准确性图表类型和设置图表选项 |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13d55fe9e4837bdacb248ddb63aad8b4064a88a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62705404"
---
# <a name="choose-an-accuracy-chart-type-and-set-chart-options"></a>选择准确性图表类型和设置图表选项
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了多种用于确定挖掘模型的有效性的方法。 您可以为每个模型或结构创建的准确性图表的类型取决于以下因素：  
  
-   用于创建模型的算法的类型  
  
-   可预测属性的数据类型  
  
-   要进行度量的可预测属性的数量  
  
 本主题概述了不同的准确性图表。  
  
 **注意** 图表及其定义都不会保存。 如果您关闭包含图表的窗口，则必须重新创建该图表。  
  
## <a name="accuracy-chart-types"></a>准确性图表类型  
 根据选择的图表类型，您可以进一步配置选项、浏览图表，或者将图表复制到剪贴板，以及在 Excel 中处理数据。  
  
#### <a name="lift-chart"></a>提升图  
 配置模型和测试数据的选项后，单击 **“提升图”** 选项卡可查看结果。 也可以将图表复制到剪贴板，或者在挖掘图例中查看各条趋势线或数据点的详细信息。  
  
#### <a name="profit-chart"></a>利润图  
 配置模型和测试数据的选项后，单击 **“提升图”** 选项卡，从 **“图表类型”** 列表中选择 **“利润图”** 可设置利润图选项，然后单击 **“确定”** 可查看结果。  
  
 您可以根据需要多次使用 **“利润图设置”** 对话框来尝试不同的成本选项以及重新显示图表。 对于每个模型，挖掘图例会包含有关估计利润的详细信息。 也可以将挖掘图例的图表和内容复制到剪贴板，然后在 Excel 中进行处理。  
  
#### <a name="scatter-plot"></a>散点图  
 如果已选择适当类型的模型，则单击 **“提升图”** 选项卡时，图表类型会自动设置为 **“散点图”** 并显示一个散点图。 不能进一步进行配置。 也可以将图表复制到剪贴板，然后将该图表作为图形粘贴到 Excel 或其他应用程序。  
  
#### <a name="classification-matrix"></a>分类矩阵  
 对于分类矩阵，使用 **“输入选择”** 选项卡选择模型和测试数据，然后单击 **“分类矩阵”** 选项卡可查看结果。  
  
 分类矩阵的内容对于所有模型类型都是相同的，并且无法进行配置。 可以将图表中的数据复制到剪贴板，然后在 Excel 中进行处理。  
  
#### <a name="cross-validation-report"></a>交叉验证报表  
 对于交叉验证报表，在解决方案资源管理器中选择挖掘结构或挖掘模型后，单击“交叉验证”选项卡，配置所有相关选项，然后单击“获取结果”生成报表。 不能进一步进行配置。  
  
 对于所有模型类型，交叉验证报表的格式均相同，并且无法进行配置。 但报表的内容会有所不同，具体取决于要分析的模型的类型和可预测属性的数据类型。 也可以将报表的结果复制到剪贴板，然后在 Excel 中处理该数据。  
  
  
