---
title: 计划策略 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 59417a54-55f1-4468-ba41-368aa852c2d4
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8becd7ad30acf1ea2a63feae4760091aede70c06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033499"
---
# <a name="schedule-the-policies"></a>计划策略
  在此任务中，您将计划在前一个任务中导入的最佳实践策略。  
  
### <a name="to-schedule-the-best-practices-policies"></a>计划最佳实践策略  
  
1.  在对象资源管理器，展开**管理**，展开**策略管理**，展开**策略**，右键单击某个最佳实践策略，并单击**属性**。  
  
    > [!NOTE]  
    >  或者，若要轻松地查看哪些策略相关联的最佳做法和进行排序最佳实践类别中，依次展开**管理**，展开**策略管理**，然后单击**策略**。 在“视图”  菜单中，单击“对象资源管理器详细信息”  。 在中**对象资源管理器详细信息**窗格中，单击**类别**标题以按类别对策略进行排序。 最佳实践策略具有前缀**Microsoft 最佳实践**。 右键单击你想要配置，然后单击的策略**属性**。  
  
2.  上**常规**页**打开策略**对话框中，在**评估模式**列表中，单击**按计划**。  
  
3.  下一步**计划**框中，单击**选取**若要指定现有的计划，或单击**新建**创建新计划。  
  
4.  配置计划后，可以选择**已启用**要启用计划的策略的页的顶部附近的复选框。  
  
5.  对于要计划的每种策略，重复步骤 1 到 4。  
  
    > [!NOTE]  
    >  若要在运行计划的策略之后查看评估结果，请打开目标实例上的“策略历史记录”日志。 若要打开日志，请右键单击**策略管理**，然后单击**查看历史记录**。  
  
## <a name="summary"></a>总结  
 您配置了要在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的单个实例上运行的计划的策略。 如果您想要将计划的策略部署到多个实例上，则继续执行本教程中的下一个任务。  
  
## <a name="next-steps"></a>后续步骤  
 [将计划的策略部署到多个实例](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
  
