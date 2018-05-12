---
title: 修改度量值 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 91de9fa781025b79f8aa47ff4e75067fe1045e88
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-3-1---modifying-measures"></a>Lesson 3-1-修改度量值
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

可以使用“FormatString”属性定义控制如何向用户显示度量值的格式设置。 在此任务中，您将为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集中的货币和百分比度量值指定格式设置属性。  
  
### <a name="to-modify-the-measures-of-the-cube"></a>修改多维数据集的度量值  
  
1.  切换到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程多维数据集的多维数据集设计器的“多维数据集结构”选项卡，然后在“度量值”窗格中展开“Internet Sales”度量值组，右键单击“订单数量”，然后单击“属性”。  
  
2.  在“属性”窗口中，单击“自动隐藏”图钉图标使“属性”窗口保持打开状态。  
  
    当“属性”窗口处于打开状态时，同时更改多维数据集中多个项的属性将更加容易。  
  
3.  在“属性”窗口中单击“FormatString”列表，然后键入 **#,#**。  
  
4.  在“多维数据集结构”选项卡的工具栏上，单击左侧的“显示度量值网格”图标。  
  
    通过网格视图，您可以同时选择多个度量值。  
  
5.  选择下列度量值之一： 可以通过在按住 Ctrl 键的同时单击各个度量值的方式来选择多个度量值：  
  
    -   **Unit Price**  
  
    -   **Extended Amount**  
  
    -   **Discount Amount**  
  
    -   **Product Standard Cost**  
  
    -   **Total Product Cost**  
  
    -   **Sales Amount**  
  
    -   **税额**  
  
    -   **Freight**  
  
6.  在“属性”窗口的“FormatString”列表中，选择“Currency”。  
  
7.  在“属性”窗口顶部（标题栏正下方）的下拉列表中，选择“Unit Price Discount Pct”度量值，然后在“FormatString”列表中选择“Percent”。  
  
8.  在“属性”窗口中，将“Unit Price Discount Pct”度量值的“名称”属性更改为“Unit Price Discount Percentage”。  
  
9. 在“度量值”窗格中，单击“Tax Amt”，然后将此度量值的名称更改为“Tax Amount”。  
  
10. 在“属性”窗口中，单击“自动隐藏”图标隐藏“属性”窗口，然后在“多维数据集结构”选项卡的工具栏上单击“显示度量值树”。  
  
11. 在“文件”  菜单上，单击“全部保存” 。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[修改客户维度](../analysis-services/lesson-3-2-modifying-the-customer-dimension.md)  
  
## <a name="see-also"></a>另请参阅  
[定义数据库维度](../analysis-services/multidimensional-models/define-database-dimensions.md)  
[配置度量值属性](../analysis-services/multidimensional-models/configure-measure-properties.md)  
  
  
  
