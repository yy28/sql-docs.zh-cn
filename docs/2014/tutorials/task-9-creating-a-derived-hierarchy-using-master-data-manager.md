---
title: 任务 9： 创建的派生层次结构，使用主数据管理器 |Microsoft 文档
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 35584d33afac7a2a8f74abd013288a974cade512
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138545"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>任务 9：使用主数据管理器创建派生层次结构
  在本任务中，您将使用主数据管理器创建一个派生层次结构。 此派生层次结构派生自之间的基于域的属性关系**供应商**和**状态**实体。  
  
1.  切换到的主页面**主数据管理器**通过单击**SQL Server 2012 Master Data Services**页顶部。  
  
2.  单击**系统管理**中**管理任务**部分。  
  
3.  将鼠标悬停**管理**菜单栏上，然后单击**派生层次结构**。  
  
     ![管理菜单的派生层次结构选择](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "管理菜单-选择的派生层次结构")  
  
4.  单击**添加派生层次结构 （+）** 工具栏上的按钮。  
  
     ![添加派生层次结构按钮](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "添加派生层次结构按钮")  
  
5.  类型**SuppliersInState**为**派生层次结构名称**。  
  
6.  单击**保存**工具栏上的按钮。  
  
     ![保存派生层次结构按钮](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "保存派生层次结构按钮")  
  
7.  拖动**供应商**从**可用级别： SuppliersInState**到**当前级别： SuppliersInState**。  
  
     ![Avialble 实体和层次结构，以当前级别](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "Avialble 实体和层次结构，以当前级别")  
  
8.  拖动**状态**从**可用级别： SuppliersInState**到**当前级别： SuppliersInState**。 屏幕应具有**当前级别**如下图中所示。  
  
     ![当前级别和派生层次结构的预览](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "当前级别和预览的派生层次结构")  
  
9. 在**预览**窗口中，展开**NY {纽约}** 和在前面的图中所示，你应看到处于该状态的一个供应商。  
  
10. 切换到的主页面**主数据管理器**通过单击**SQL Server 2012 Master Data Services**页顶部。  
  
11. 单击 **“资源管理器”**。  
  
12. 将鼠标悬停**层次结构**单击**派生： SuppliersInState**。  
  
     ![层次结构的派生： SuppliersInState 菜单](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "层次结构的派生： SuppliersInState 菜单")  
  
13. 单击任何**状态**中的节点**树视图**，你应看到处于该状态在右窗格中的供应商。  
  
     ![派生层次结构资源管理器中的](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "派生层次结构在资源管理器")  
  
## <a name="next-step"></a>下一步  
 [第 5 课：使用 SSIS 自动执行清理和匹配](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  