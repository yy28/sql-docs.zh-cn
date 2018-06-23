---
title: 预测向导 （数据挖掘外接程序 excel） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- forecasting [data mining]
- time series [data mining]
ms.assetid: c5b33f75-42d4-4598-89e7-94815c142ce6
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 118d66a0bd06ced70860e7de91938115b1e499be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128212"
---
# <a name="forecast-wizard-data-mining-add-ins-for-excel"></a>预测向导（Excel 数据挖掘外接程序）
  ![数据挖掘功能区中的关联向导](media/dmc-forecast.gif "数据挖掘功能区中的关联向导")  
  
 使用预测向导可以预测时序中的值。 预测向导使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法，该算法是一个用于预测连续列（例如产品销售）的回归算法。  
  
 每个预测模型都必须包含一个事例序列，即区分序列中不同点的列。 举例来说，如果您使用历史数据来预测几个月内的销售情况，您会用到一个列，其中包含一系列日期来作为事例序列。  
  
 您可以从预测模型中创建预测信息，而无需提供新的输入数据。  
  
 [预测&#40;for Excel 表分析工具&#41;](forecast-table-analysis-tools-for-excel.md)工具，在**分析**功能区，还允许你创建预测模型，但它是不太可自定义，在 Excel 表中只能使用数据。  
  
## <a name="using-the-forecast-wizard"></a>使用预测向导  
  
1.  在**数据挖掘**功能区上，单击**预测**。  
  
2.  在**选择源数据**，选择 Excel 表、 范围或外部数据源以使用作为输入。  
  
     如果使用外部数据源，您可以定义自定义视图或查询并将其另存为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源。  
  
3.  上**预测**页上，为**时间戳**，选择一列以包含唯一可用作事例序列的数字值 （这包括日期和时间值）。 必须按此列以升序顺序对数据源进行排序。  
  
     如果你的数据没有这样的列，则可以使用选项\<无时间戳 >。 此向导将为输入数据添加一个唯一的排序列；因此，您必须确保首先按照您希望的方式对数据进行排序，然后再运行此向导和选择此选项。  
  
4.  （可选） 你可以单击**参数**和自定义挖掘模型的行为。  
  
     预测模型支持以下几种不同的算法：  
  
    -   ARIMA  
  
    -   ARTXP（一种回归模型）  
  
    -   组合的 ARTXP 和 ARIMA  
  
     有关的差异的信息，请参阅[Microsoft Time Series Algorithm Technical Reference](data-mining/microsoft-time-series-algorithm-technical-reference.md)。  
  
     您还可以为模型添加周期提示、指定平滑选项以及自定义回归选项。  
  
5.  上**完成**页上，提供你的数据集和模型的描述性名称，设置以下控制工作完成的模型的方式的选项：  
  
    -   **浏览模型**。 选中此选项后，尽快向导完成处理模型时，它将打开**浏览**窗口来帮助你浏览结果。 查看器的内容取决于您建立的模型的类型。 有关详细信息，请参阅[浏览预测模型](browsing-a-forecasting-model.md)。  
  
    -   **启用钻取**。 选择此选项可以查看已完成模型中的基础数据。 此选项仅在建立决策树模型时可用。  
  
    -   **使用临时模型**。 如果您选择此选项，模型将不会被保存到服务器。 在您关闭 Excel 时，临时模型将被删除。  
  
### <a name="requirements"></a>要求  
 您的数据中应至少包括一个可用作时序的列。 此列中的值应当唯一且连续，也就是说，没有间隔。 在运行此向导之前，请按时序列以升序顺序对数据进行排序。  
  
 如果您的数据中不包括时间或日期列，可以指定任意数值序列或由向导创建一个数值序列。 如果您选择由向导创建序列排序列，请确保在启动向导之前按您所希望的方式对其他列进行了排序。  
  
## <a name="see-also"></a>请参阅  
 [创建数据挖掘模型](creating-a-data-mining-model.md)   
 [预测&#40;的 Excel 表分析工具&#41;](forecast-table-analysis-tools-for-excel.md)   
 [浏览预测模型](browsing-a-forecasting-model.md)  
  
  