---
title: 任务 8： 添加新值在 Excel 中的状态实体 |Microsoft 文档
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
ms.topic: article
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: db2eaccd4d9b344cbc1b7c25b6fec940ff9c77a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127426"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>任务 8：在 Excel 中为 State 实体添加新值
  在本任务中，您将在 Excel 中为 State 实体添加值，并且将更改发布到 MDS 服务器。  
  
1.  添加**工作表**在通过单击新选项卡底部的 Excel 中。  
  
     ![Excel-新工作表选项卡](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel-新工作表选项卡")  
  
2.  在**Excel**，单击**主数据**的菜单上，选项卡，然后单击**显示资源管理器**功能区上。  
  
3.  在**主数据资源管理器**，选择**供应商**为**模型**。 你应该会看到两个实体：**供应商**和**状态**实体列表中。  
  
4.  双击**状态**列表中。 所有成员**状态**从 MDS 实体应显示在工作表。  
  
5.  现在，使用以下值的结尾处添加行：**北卡罗来纳**为**名称**和**NC**为**代码**。 颜色编码可以将任何新的/更新的记录与其他记录区分开来。  
  
     ![Excel-将北卡罗来纳添加到状态](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel-将北卡罗来纳添加到状态")  
  
6.  单击**发布**将更改发布到 MDS 功能区上。  
  
     ![Excel-发布 Master 数据选项卡上的按钮](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel-发布 Master 数据选项卡上的按钮")  
  
7.  上**发布并添加批注**对话框框中，请注意，**使用相同的批注的所有更改**选择。 您可以在此处为所有更改输入单个批注。  
  
8.  选择**查看更改并分别提供批注**选项，以提供针对每项更改 （在此情况下，只有一个） 的批注。  
  
     ![Excel-发布并添加批注对话框](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "Excel-发布并添加批注对话框")  
  
9. 单击**发布**将数据发布到 MDS。  
  
10. 请注意，**颜色编码**对于有行**北卡罗来纳**作为**状态**现已与其他记录相同。  
  
11. **可选：** 验证是否 (NC) 的新成员添加到**状态**实体使用**资源管理器**中**主数据管理器**。  
  
12. 在 Excel 中，右键单击**状态**底部，然后单击在工作表中**删除**来删除工作表。 删除该工作表不会从 MDS 服务器中删除任何数据。  
  
## <a name="next-step"></a>下一步  
 [任务 9：使用主数据管理器创建派生层次结构](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  