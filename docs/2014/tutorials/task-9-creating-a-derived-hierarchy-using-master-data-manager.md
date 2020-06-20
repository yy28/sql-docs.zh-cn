---
title: 任务9：使用主数据管理器创建派生层次结构 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 56e3d832fccbab849d0646c761964aee9266181e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006211"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>任务 9：使用主数据管理器创建派生层次结构
  在本任务中，您将使用主数据管理器创建一个派生层次结构。 此派生层次结构从**供应商**和**状态**实体之间的基于域的属性关系中派生。  
  
1.  单击页面顶部**SQL Server 2012 Master Data Services** ，切换到**主数据管理器**的主页。  
  
2.  单击 "**管理任务**" 部分中的 "**系统管理**"。  
  
3.  将鼠标悬停在菜单栏上的 "**管理**" 上，然后单击 "**派生层次结构**"。  
  
     ![“管理”菜单 - 已选择派生层次结构](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "“管理”菜单 - 已选择派生层次结构")  
  
4.  单击工具栏上的 "**添加派生层次结构（+）** " 按钮。  
  
     ![“添加派生层次结构”按钮](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "“添加派生层次结构”按钮")  
  
5.  为**派生层次结构名称**键入**SuppliersInState** 。  
  
6.  单击工具栏上的 "**保存**" 按钮。  
  
     ![“保存派生层次结构”按钮](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "“保存派生层次结构”按钮")  
  
7.  从可用级别拖动**供应商** **： SuppliersInState**到**当前级别： SuppliersInState**。  
  
     ![当前级别的可用实体和层次结构](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "当前级别的可用实体和层次结构")  
  
8.  将**状态**从 "**可用级别： SuppliersInState** " 拖到 "**当前级别： SuppliersInState**"。 屏幕应具有**当前级别**，如下图所示。  
  
     ![当前级别和派生层次结构预览](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "当前级别和派生层次结构预览")  
  
9. 在 "**预览**" 窗口中，展开 " **NY {纽约}** "，你应看到一个处于该状态的供应商，如上图所示。  
  
10. 单击页面顶部**SQL Server 2012 Master Data Services** ，切换到**主数据管理器**的主页。  
  
11. 单击 **“资源管理器”**。  
  
12. 将鼠标悬停在**层次结构**上，然后单击 "**派生： SuppliersInState**"。  
  
     ![层次结构 - Derived:SuppliersInState 菜单](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "层次结构 - Derived:SuppliersInState 菜单")  
  
13. 单击**树视图**中的任何 "**状态**" 节点，你应会在右窗格中看到该状态的供应商。  
  
     ![资源管理器中的派生层次结构](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "资源管理器中的派生层次结构")  
  
## <a name="next-step"></a>后续步骤  
 [第 5 课：使用 SSIS 自动执行清理和匹配](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  
