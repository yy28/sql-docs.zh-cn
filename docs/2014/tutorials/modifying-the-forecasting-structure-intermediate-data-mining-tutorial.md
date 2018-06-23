---
title: 修改预测结构 （数据挖掘中级教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4252f9885070067278a24db266ce58714366e69b
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312125"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>修改预测结构（数据挖掘中级教程）
  您在上一个任务中创建的挖掘结构包含单个预测模型。 在处理和浏览该模型之前，您必须对其结构稍加更改并修改它的一个属性。  
  
## <a name="modifying-the-mining-structure"></a>修改挖掘结构  
 你可以通过更改挖掘结构**挖掘结构**数据挖掘设计器选项卡。 您在使用数据挖掘向导创建该模型时，使用了以下三个列：ReportingDate、ModelRegion 和 Quantity。 但是，**预测**表还包含可用于预测的销售额量列。 通过使用**挖掘结构**选项卡上，你可以将此列的数据源视图添加到挖掘结构。  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>将“金额”列添加到“预测”挖掘结构  
  
1.  上**挖掘结构**数据挖掘设计器选项卡，请在**数据源视图**窗格中，选择量列 vTimeSeries 表中。  
  
2.  将从量列拖动**数据源视图**到中的列列表窗格中**预测**结构。  
  
     中现在包含量列**预测**挖掘结构。  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>修改挖掘模型中的列  
 由于向结构中添加了新列，所以必须定义模型使用该列的方式。 你可以指定将如何在使用列**挖掘模型**数据挖掘设计器选项卡。  
  
 **挖掘模型**选项卡列出挖掘结构中包含的列**结构**网格中，并列出挖掘模型包含同名的列中的列的列模型，在这种情况下**预测**。 单击列名称以进行修改。 在**预测**挖掘模型量列用作输入列，并且还可用于预测未来的销售。 因此，必须设置该列的属性，以便可同时将其用作输入列和可预测列。  
  
> [!NOTE]  
>  在**挖掘模型**选项卡上，你还可以创建新模型基于相同的结构，并可以调整每个模型的算法和列属性。 但是，必须先处理模型，然后这些更改才能生效。  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>定义“金额”列的使用方式  
  
1.  在**预测**列上的网格**挖掘模型**选项卡上，单击量行中的单元格。  
  
2.  选择**预测**从列表中。  
  
     现在，Amount 列既是输入列，又是可预测列。  
  
 此外可以更改单个列的属性，通过选择列并打开**属性**窗口。 若要打开**属性**窗口中，右键单击列名称，然后选择**属性**。 如果在单个模型的列中更改属性，则只能更改该模型的属性。 但是，当你更改中的属性时，才**结构**列中，此更改将影响与结构关联的每个模型。 无论何时对模型或结构进行更改，都必须对它们进行重新处理才能查看效果。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [自定义和处理预测模型&#40;中间数据挖掘教程&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [挖掘结构&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [挖掘模型&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  