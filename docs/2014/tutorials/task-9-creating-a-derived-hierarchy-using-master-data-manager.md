---
title: 任务 9： 创建派生层次结构使用主数据管理器 |Microsoft Docs
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
ms.topic: conceptual
ms.assetid: 3bd2ec05-933f-4947-b1fe-c9226961eb7d
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 22aba36efffe3b4e15d358e6077bb6b58e7aa328
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273583"
---
# <a name="task-9-creating-a-derived-hierarchy-using-master-data-manager"></a>任务 9：使用主数据管理器创建派生层次结构
  在本任务中，您将使用主数据管理器创建一个派生层次结构。 此派生层次结构派生自之间的基于域的属性关系**供应商**并**状态**实体。  
  
1.  切换到的主页**主数据管理器**通过单击**SQL Server 2012 Master Data Services**页的顶部。  
  
2.  单击**系统管理**中**管理任务**部分。  
  
3.  将鼠标悬停**管理**上的菜单栏中，然后单击**派生层次结构**。  
  
     ![管理菜单的所选的派生层次结构](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-01.jpg "管理菜单的所选的派生层次结构")  
  
4.  单击**添加派生层次结构 （+）** 工具栏上的按钮。  
  
     ![添加派生层次结构按钮](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-02.jpg "添加派生层次结构按钮")  
  
5.  类型**SuppliersInState**有关**派生层次结构名称**。  
  
6.  单击**保存**工具栏上的按钮。  
  
     ![保存派生层次结构按钮](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-03.jpg "保存派生层次结构按钮")  
  
7.  拖动**供应商**从**可用级别： SuppliersInState**到**当前级别： SuppliersInState**。  
  
     ![可用实体和层次结构，以当前级别](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-04.jpg "可用实体和层次结构，以当前级别")  
  
8.  拖动**状态**从**可用级别： SuppliersInState**到**当前级别： SuppliersInState**。 屏幕应具有**当前级别**，如下图中所示。  
  
     ![当前级别和派生层次结构的预览版](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-05.jpg "当前级别和派生层次结构预览")  
  
9. 在中**预览版**窗口中，展开**NY {New York}** ，您应看到处于该状态的一个供应商，如上图中所示。  
  
10. 切换到的主页**主数据管理器**通过单击**SQL Server 2012 Master Data Services**页的顶部。  
  
11. 单击 **“资源管理器”**。  
  
12. 将鼠标悬停**层次结构**然后单击**派生： SuppliersInState**。  
  
     ![层次结构-Derived: SuppliersInState 菜单](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-06.jpg "层次结构-Derived: SuppliersInState 菜单")  
  
13. 单击任意**状态**中的节点**树视图**，应会看到该州的供应商在右窗格中。  
  
     ![派生层次结构资源管理器中的](../../2014/tutorials/media/et-creatingaderivedhierarchyusingmdm-07.jpg "派生层次结构在资源管理器")  
  
## <a name="next-step"></a>下一步  
 [第 5 课：使用 SSIS 自动执行清理和匹配](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)  
  
  
