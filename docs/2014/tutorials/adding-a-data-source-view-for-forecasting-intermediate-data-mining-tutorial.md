---
title: 添加数据源视图来进行预测 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 2665040a-1291-4064-ba01-f458637dda57
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b91be4b60c65a246b56a2d08142ce6937d80cea0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162577"
---
# <a name="adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial"></a>为 Forecasting 添加数据源视图（数据挖掘中级教程）
  在本任务中，添加将用于预测方案的数据源视图。 预测模型要求数据包含一个可用于标识时序中的步长的列。 如果计划分析多个数据序列，则所有序列的结束日期或时间步长必须相同。  
  
### <a name="to-add-a-data-source-view"></a>添加数据源视图  
  
1.  在解决方案资源管理器中右键单击**数据源视图**，然后选择**新数据源视图**。  
  
2.  在“欢迎使用数据源视图向导”页中，单击“下一步”。  
  
3.  上**选择数据源**页面上，在**关系数据源**，选择[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]数据源。 单击“下一步” 。  
  
    > [!NOTE]  
    >  如果没有此数据源，您可以发现创建中的数据源的步骤[数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)。  
  
4.  上**选择表和视图**页上，选择表 vTimeSeries (dbo)，然后单击右箭头以将其添加到数据源视图。  
  
5.  单击“下一步” 。  
  
6.  上**完成向导**页上，默认情况下，数据源视图命名为[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]。 将名称更改为**SalesByRegion**，然后单击**完成**。  
  
     数据源视图设计器将打开并**SalesByRegion**数据源视图将显示。  
  
## <a name="working-with-the-data-source-view"></a>使用数据源视图  
 创建数据源视图之后，可以通过以下方法浏览数据：  
  
-   右键单击设计器中的 vTimeSeries 表并选择**浏览数据**以在网格中打开所选的表。  
  
-   单击**抽样选项**，然后使用**数据浏览选项**对话框可以更改采样方法。 单击**刷新**将使用新的选项设置对表中的数据加载。 例如，可以指定要输出在示例中，或选择前 n 行的行数。  
  
-   右键单击表 vTimeSeries 并选择**属性**为表分配新名称。 您还可以从数据源视图中选择单个列，并修改列属性。  
  
-   在数据源视图设计区域内的任意位置单击，创建一个新查询并向其分配名称，创建各表之间的关系，或者更改设计区域的布局。  
  
-   右键单击某个表，然后选择**新建命名计算**以创建派生的列，包括聚合。 还可以在此视图中从数据源添加新的表和视图。  
  
 在下一个任务中，您将浏览时序数据并确定最适合用作时序标识符的列。 您还将了解如何处理时序数据中的空白。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [了解模型的要求某一时序的&#40;数据挖掘中级教程&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 时序算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
