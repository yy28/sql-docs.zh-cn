---
title: 创建预测结构和模型（数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5f55cbf6-0db4-4cb4-a0f5-e27441873d4f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6e631a8983705d4f58e4b193823c9a255284f346
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63204809"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>创建预测结构和模型（数据挖掘中级教程）
  现在您将使用数据挖掘向导，基于刚创建的数据源视图创建新的挖掘结构和挖掘模型。 在本任务中，您将指定挖掘模型应使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法。  
  
### <a name="to-create-a-forecasting-mining-structure"></a>创建预测挖掘结构  
  
1.  在的解决方案资源管理器[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，右键单击 "**挖掘结构**"，然后选择 "**新建挖掘结构**"。  
  
2.  在 **“欢迎使用数据挖掘向导”** 页上，单击 **“下一步”**。  
  
3.  在 "**选择定义方法**" 页上，验证是否选择了 "**从现有关系数据库或数据仓库**"，然后单击 "**下一步**"。  
  
4.  在 "**创建数据挖掘结构**" 页上，在 "**要使用何种数据挖掘技术？**" 下，选择 " **Microsoft 时序**"，然后单击 "**下一步**"。  
  
5.  在 "**选择数据源视图**" 页上的 "**可用数据源视图**" 下，选择**salesbyregion.dsv**。  
  
6.  单击“下一步”。   
  
7.  在 "**指定表类型**" 页上，确保选中 "vTimeSeries" 表的 "**事例**" 列中的复选框，然后单击 "**下一步**"。  
  
8.  在 "**指定定型数据**" 页上，选中 ModelRegion 和 ReportingDate 列的**键**列中的复选框。  
  
     ReportingDate 默认情况下应处于选中状态，因为您在创建数据源视图时已经将该列指定为逻辑主键。 通过将 ModelRegion 添加为第二个键，您将指示此算法为该字段中列出的每个模型和地区组合创建一个单独的时序。  
  
9. 选中 "数量" 列的 "**输入**" 和 "**可预测**" 列中的复选框，然后单击 "**下一步**"。  
  
     通过选择 "**可预测**"，您可以指示要对此列中的数据创建预测。 但是，由于您希望预测基于以前的数据，还必须添加该列作为输入。  
  
10. 在 "**指定列的内容和数据类型**" 页上，查看所选内容。  
  
     将 ModelRegion 列指定为**键**列，并将 ReportingDate 列自动指定为**key Time**列。 您只能拥有一种类型的键。  
  
11. 单击“下一步”。   
  
12. 在 "**完成向导**" 页的 "**挖掘结构名称**" 中`Forecasting`，键入。  
  
    > [!NOTE]  
    >  用来启用钻取的选项对于时序模型不可用。  
  
13. 在 "**挖掘模型名称**" `Forecasting`中，键入，然后单击 "**完成**"。  
  
     此时将打开数据挖掘设计器`Forecasting` ，显示您刚创建的挖掘结构。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [&#40;中级数据挖掘教程修改预测结构&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘设计器](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 时序算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
