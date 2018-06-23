---
title: 计划策略 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 59417a54-55f1-4468-ba41-368aa852c2d4
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 99c6e3a4eacfea76ff16ea266d38f2087c088f33
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024236"
---
# <a name="schedule-the-policies"></a>计划策略
  在此任务中，您将计划在前一个任务中导入的最佳实践策略。  
  
### <a name="to-schedule-the-best-practices-policies"></a>计划最佳实践策略  
  
1.  在对象资源管理器，展开**管理**，展开**策略管理**，展开**策略**，右键单击最佳实践策略，，然后单击**属性**。  
  
    > [!NOTE]  
    >  作为替代方法，以轻松地了解哪些策略相关联的最佳做法和进行排序最佳实践类别中，展开**管理**，展开**策略管理**，然后单击**策略**。 在“视图”菜单中，单击“对象资源管理器详细信息”。 在**对象资源管理器详细信息**窗格中，单击**类别**标题以按类别排序策略。 最佳实践策略都具有前缀**Microsoft 最佳实践**。 右键单击你想要配置，，然后单击策略**属性**。  
  
2.  上**常规**页**打开策略**对话框中，在**评估模式**列表中，单击**准时**。  
  
3.  旁边**计划**框中，单击**选取**指定现有的计划，或单击**新建**创建新计划。  
  
4.  已配置了计划后，你可以选择**已启用**要启用计划的策略的页的顶部附近的复选框。  
  
5.  对于要计划的每种策略，重复步骤 1 到 4。  
  
    > [!NOTE]  
    >  若要在运行计划的策略之后查看评估结果，请打开目标实例上的“策略历史记录”日志。 要打开的日志，请右键单击**策略管理**，然后单击**查看历史记录**。  
  
## <a name="summary"></a>“摘要”  
 您配置了要在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的单个实例上运行的计划的策略。 如果您想要将计划的策略部署到多个实例上，则继续执行本教程中的下一个任务。  
  
## <a name="next-steps"></a>后续步骤  
 [将计划的策略部署到多个实例](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
  