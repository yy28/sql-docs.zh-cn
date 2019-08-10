---
title: 创建数据源视图 (数据挖掘基础教程) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c1e68a88-0f82-415d-becc-78d180d4f845
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ac7730e8437eaed304ed69c40e45fc93ee9b5531
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68888649"
---
# <a name="creating-a-data-source-view-basic-data-mining-tutorial"></a>创建数据源视图（数据挖掘基础教程）
  数据源视图是在某个数据源的基础上生成的，并且定义可在您的挖掘结构中使用的数据的子集。 您还可以使用数据源视图来添加列、创建计算列和聚合以及添加命名视图。 通过数据源视图，可以选择与项目相关的数据，建立表之间的关系，以及修改数据的结构，而不必修改原始的数据源。 有关详细信息，请参阅 [多维模型中的数据源视图](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)。  
  
### <a name="to-create-a-data-source-view"></a>创建数据源视图  
  
1.  在**解决方案资源管理器**中, 右键单击 "**数据源视图**", 然后选择 "**新建数据源视图**"。  
  
2.  在“欢迎使用数据源视图向导”页中，单击“下一步”。  
  
3.  在 "**选择数据源**" 页的 "**关系数据源**" 下, 选择在上一个任务中创建的艾德公司 DW 2012 数据源。 单击“下一步”。  
  
    > [!NOTE]  
    >  如果要创建数据源, 请右键单击 "**数据源**", 然后单击 "**新建数据源**" 以启动 "数据源向导"。  
  
4.  在 "**选择表和视图**" 页上, 选择下列对象, 然后单击右箭头将它们包含在新的数据源视图中:  
  
    -   **ProspectiveBuyer (dbo)** -预期自行车购买者的表  
  
    -   **vTargetMail (dbo)** -有关过去自行车购买者的历史数据的视图  
  
5.  单击“下一步”。  
  
6.  在 "**完成向导**" 页上, 默认情况下将数据源视图命名为 "艾德作品 DW 2012"。 将名称更改为`Targeted Mailing`, 然后单击 "**完成**"。  
  
     新数据源视图将在 "目标" " **dsv [设计]** " 选项卡中打开。  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [创建数据源&#40;数据挖掘基础教程&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一课  
 [第 2 课：生成目标邮件结构&#40;数据挖掘基础教程&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [定义数据源视图 (Analysis Services)](https://docs.microsoft.com/analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services)  
  
  
