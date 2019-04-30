---
title: 修改预测结构 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a86ddf0a715fc3a2313f555e898b3bd94cf66d8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301300"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>修改预测结构（数据挖掘中级教程）
  您在上一个任务中创建的挖掘结构包含单个预测模型。 在处理和浏览该模型之前，您必须对其结构稍加更改并修改它的一个属性。  
  
## <a name="modifying-the-mining-structure"></a>修改挖掘结构  
 可以通过更改挖掘结构**挖掘结构**数据挖掘设计器选项卡。 当使用数据挖掘向导创建该模型时，您在使用三个列：ReportingDate、 ModelRegion 和 Quantity。 但是， **Forecasting**表还包含一个 Amount 列，可用于预测的销售额。 通过使用**挖掘结构**选项卡上，您可以将该列从数据源视图添加到挖掘结构。  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>将“金额”列添加到“预测”挖掘结构  
  
1.  上**挖掘结构**数据挖掘设计器选项卡，在**数据源视图**窗格中，选择 vTimeSeries 表中的 Amount 列。  
  
2.  将 Amount 列从**数据源视图**窗格中的列列表**Forecasting**结构。  
  
     Amount 列现在包含在**Forecasting**挖掘结构。  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>修改挖掘模型中的列  
 由于向结构中添加了新列，所以必须定义模型使用该列的方式。 您可以指定列上的使用方式**挖掘模型**数据挖掘设计器选项卡。  
  
 **挖掘模型**选项卡列出了挖掘结构中包含的列**结构**的网格中，并列出了挖掘模型包含同名的列中的列的列模型，在这种情况下**Forecasting**。 单击列名称以进行修改。 在中**Forecasting**挖掘模型的 Amount 列既用作输入列和又用于预测未来的销售额。 因此，必须设置该列的属性，以便可同时将其用作输入列和可预测列。  
  
> [!NOTE]  
>  在中**挖掘模型**选项卡上，您还可以创建新模型基于相同的结构，并可以调整每个模型的算法和列属性。 但是，必须先处理模型，然后这些更改才能生效。  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>定义“金额”列的使用方式  
  
1.  在中**Forecasting**上的网格的列**挖掘模型**选项卡上，单击 Amount 行中的单元格。  
  
2.  选择**Predict**从列表中。  
  
     现在，Amount 列既是输入列，又是可预测列。  
  
 您还可以通过以下方式更改各个列的属性选择列并打开**属性**窗口。 若要打开**属性**窗口中，右键单击列名称，然后选择**属性**。 如果在单个模型的列中更改属性，则只能更改该模型的属性。 但是，当更改中的属性**结构**列中，此更改将影响与结构关联的每个模型。 无论何时对模型或结构进行更改，都必须对它们进行重新处理才能查看效果。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [自定义和处理预测模型&#40;数据挖掘中级教程&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [挖掘结构 &#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [挖掘模型（Analysis Services - 数据挖掘）](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
