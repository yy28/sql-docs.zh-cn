---
title: 对结构数据 （数据挖掘基础教程） 中使用钻取 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a693979c-0564-4d6d-b35d-cbbc8f350469
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 68d5d29a4aed7380bd7a53c65d140aac24912392
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745538"
---
# <a name="using-drillthrough-on-structure-data-basic-data-mining-tutorial"></a>对结构数据使用钻取（数据挖掘基础教程）
  作为其广告活动，一部分[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]发送邮寄给潜在的客户在 34 至 40 时代人口统计。 市场部已决定还要向五年多以前从 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 购买自行车的客户发送电子邮件。 在本课中，您将标识拥有旧自行车的客户并检索其联系信息。 模型中不包括此信息，但结构中包括此信息。 若要检索联系信息，您需要首先确保已对结构启用了钻取，然后使用钻取来显示目标客户的姓名和地址。  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>对挖掘模型启用钻取  
  
1.  在中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，然后在**挖掘模型**选项卡上的数据挖掘设计器中，右键单击**TM_Decision_Tree**模型并选择**属性**。  
  
2.  在“属性”窗口中，单击 **AllowDrillthrough**，再选择 **True**。  
  
3.  在挖掘模型选项卡中，右键单击该模型，并选择**过程模型**。  
  
 有关详细信息，请参阅[钻取查询&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>查看挖掘模型的钻取数据  
  
1.  在数据挖掘设计器中，单击 **“挖掘模型查看器”** 选项卡。  
  
2.  选择**TM_Decision_Tree**模型从**挖掘模型**列表。  
  
3.  更改**背景**值设为`1`。 这样做之后，您将只显示与购买了自行车的客户相关的模型部分。  
  
4.  从 **“查看器”** 列表中，选择“Microsoft 树查看器”。 这将强制使用新的筛选条件刷新查看器。 然后，找到**Age > = 34 和 < 41**节点，右键单击该节点。  
  
5.  选择 **“钻取”** ，然后选择 **“模型和结构列”** 以打开 **“钻取”** 窗口。  
  
6.  滚动到 **Structure.Date First Purchase** 列以查看旧自行车的购买日期。  
  
7.  若要将数据复制到剪贴板，请右键单击表中的任何行，并选择“全部复制”  。  
  
 恭喜您！您已经完成了数据挖掘基础教程。 既然您已经熟练掌握了数据挖掘工具，我们建议您同时完成数据挖掘中级教程，中级教程将演示如何创建用于预测、市场篮分析以及顺序分析和聚类分析的模型。  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [创建预测（数据挖掘基础教程）](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [使用预测查询生成器创建预测查询](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
