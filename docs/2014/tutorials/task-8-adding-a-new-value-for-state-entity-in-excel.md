---
title: 任务 8： 为在 Excel 中的 State 实体添加新值 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4f4e79915ba28beb7cd28920faff2f79e6b339d6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163768"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>任务 8：在 Excel 中为 State 实体添加新值
  在本任务中，您将在 Excel 中为 State 实体添加值，并且将更改发布到 MDS 服务器。  
  
1.  添加**工作表**Excel 通过单击底部的新选项卡中。  
  
     ![Excel-新工作表选项卡](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel 的新工作表选项卡")  
  
2.  在中**Excel**，单击**主数据**菜单上，选项卡，然后单击**显示资源管理器**功能区上。  
  
3.  在中**主数据资源管理器**，选择**供应商**有关**模型**。 你应看到两个实体：**供应商**并**状态**实体列表中。  
  
4.  双击**状态**列表中。 所有成员**状态**从 MDS 实体应显示在工作表中。  
  
5.  现在，使用以下值的结尾处添加一个行：**北卡罗来纳**有关**名称**并**NC**有关**代码**。 颜色编码可以将任何新的/更新的记录与其他记录区分开来。  
  
     ![Excel-将北卡罗来纳州添加到状态](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel-将北卡罗来纳州添加到状态")  
  
6.  单击**发布**在功能区中，若要将更改发布到 MDS。  
  
     ![Excel-发布主数据选项卡上的按钮](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel-发布主数据选项卡上的按钮")  
  
7.  上**发布并添加批注**对话框框中，注意**对所有更改使用相同的批注**处于选中状态。 您可以在此处为所有更改输入单个批注。  
  
8.  选择**审阅更改并分别提供批注**选项来提供每次更改 （在此情况下，只有一个） 的批注。  
  
     ![Excel-发布并添加批注对话框的](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "Excel-发布并添加批注对话框的")  
  
9. 单击**发布**将数据发布到 MDS。  
  
10. 请注意，**颜色编码**行的**北卡罗来纳州**作为**状态**现已与其他记录相同。  
  
11. **可选：** 确认新成员 (NC) 已添加到**状态**使用的实体**资源管理器**中**主数据管理器**。  
  
12. 在 Excel 中，右键单击**状态**工作表的底部，然后单击**删除**以删除该工作表。 删除该工作表不会从 MDS 服务器中删除任何数据。  
  
## <a name="next-step"></a>下一步  
 [任务 9：使用主数据管理器创建派生层次结构](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  
