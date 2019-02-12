---
title: 创建预测结构和模型 （数据挖掘中级教程） |Microsoft Docs
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
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56015248"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>创建预测结构和模型（数据挖掘中级教程）
  现在您将使用数据挖掘向导，基于刚创建的数据源视图创建新的挖掘结构和挖掘模型。 在本任务中，您将指定挖掘模型应使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法。  
  
### <a name="to-create-a-forecasting-mining-structure"></a>创建预测挖掘结构  
  
1.  在解决方案资源管理器中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，右键单击**挖掘结构**，然后选择**新建挖掘结构**。  
  
2.  在 **“欢迎使用数据挖掘向导”** 页上，单击 **“下一步”**。  
  
3.  上**选择定义方法**页上，确认**从现有关系数据库或数据仓库**已选择，然后单击**下一步**。  
  
4.  上**创建数据挖掘结构**页面上，在**想要使用何种数据挖掘技术？**，选择**Microsoft 时序**，然后单击**下一步**。  
  
5.  上**选择数据源视图**页面上，在**可用数据源视图**，选择**SalesByRegion**。  
  
6.  单击“下一步” 。  
  
7.  上**指定表类型**页上，确保中的复选框**用例**vTimeSeries 表的列已选中，然后单击**下一步**。  
  
8.  上**指定定型数据**页上，选择中的复选框**密钥**ModelRegion 和 ReportingDate 列的列。  
  
     ReportingDate 默认情况下应处于选中状态，因为您在创建数据源视图时已经将该列指定为逻辑主键。 通过将 ModelRegion 添加为第二个键，您将指示此算法为该字段中列出的每个模型和地区组合创建一个单独的时序。  
  
9. 选择中的复选框**输入**并**可预测**列的数量，列，再单击**下一步**。  
  
     通过选择**可预测**，指示你想要在此列中的数据，来创建预测。 但是，由于您希望预测基于以前的数据，还必须添加该列作为输入。  
  
10. 在页上**指定列内容和数据类型**，检查所做选择。  
  
     ModelRegion 列被指定为**键**列，ReportingDate 列将自动指定为**Key Time**列。 您只能拥有一种类型的键。  
  
11. 单击“下一步” 。  
  
12. 上**完成向导**页上，对于**挖掘结构名称**，类型`Forecasting`。  
  
    > [!NOTE]  
    >  用来启用钻取的选项对于时序模型不可用。  
  
13. 在中**挖掘模型名称**，类型`Forecasting`，然后单击**完成**。  
  
     数据挖掘设计器将打开以显示`Forecasting`刚创建的挖掘结构。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [修改预测结构&#40;数据挖掘中级教程&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘设计器](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft 时序算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
