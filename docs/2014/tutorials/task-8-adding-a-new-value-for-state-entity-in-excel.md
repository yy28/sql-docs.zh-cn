---
title: 任务8：在 Excel 中为 State 实体添加新值 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a763d76b-06a3-4d51-9614-01fc9fb1c158
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 831d0b504a65d485413772ee3711e689e29ee2a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489700"
---
# <a name="task-8-adding-a-new-value-for-state-entity-in-excel"></a>任务 8：在 Excel 中为 State 实体添加新值
  在本任务中，您将在 Excel 中为 State 实体添加值，并且将更改发布到 MDS 服务器。  
  
1.  单击底部的 "新建" 选项卡，在 Excel 中添加**工作表**。  
  
     ![Excel -“新建工作表”选项卡](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-01.jpg "Excel -“新建工作表”选项卡")  
  
2.  在**Excel**中，单击菜单上的 "**主数据**" 选项卡，然后单击功能区上的 "**显示资源管理器**"。  
  
3.  在**主数据资源管理器**中，选择 "**模型****供应商**"。 应会在实体列表中看到两个实体：**供应商**和**状态**。  
  
4.  双击列表中的 "**状态**"。 来自 MDS 的**状态**实体的所有成员应显示在工作表中。  
  
5.  现在，在末尾添加具有以下值的行：**北卡罗来纳**for **Name**和**NC** for **Code**。 颜色编码可以将任何新的/更新的记录与其他记录区分开来。  
  
     ![Excel - 将北卡罗来纳州添加到“州/省”](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-02.jpg "Excel - 将北卡罗来纳州添加到“州/省”")  
  
6.  在功能区上单击 "**发布**"，将更改发布到 MDS。  
  
     ![Excel -“主数据”选项卡上的“发布”按钮](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-03.jpg "Excel -“主数据”选项卡上的“发布”按钮")  
  
7.  请注意，在 "**发布并添加批注**" 对话框上，选择 "对**所有更改使用相同的批注**"。 您可以在此处为所有更改输入单个批注。  
  
8.  选择 "**查看更改并单独提供批注**" 选项以提供每个更改的批注（在此示例中，只有一个）。  
  
     ![Excel -“发布并添加批注”对话框](../../2014/tutorials/media/et-addinganewvalueforstateentityinexcel-04.jpg "Excel -“发布并添加批注”对话框")  
  
9. 单击 "**发布**" 以将数据发布到 MDS。  
  
10. 请注意，将**北卡罗莱纳州**的行的**颜色编码**为 "**状态**" 与其他记录相同。  
  
11. **可选：** 使用**主数据管理器**中的 "**资源管理器**" 验证新成员（NC）已添加到**State**实体。  
  
12. 在 Excel 中，右键单击底部的**状态**工作表，然后单击 "**删除**" 以删除该工作表。 删除该工作表不会从 MDS 服务器中删除任何数据。  
  
## <a name="next-step"></a>下一步  
 [任务 9：使用主数据管理器创建派生层次结构](../../2014/tutorials/task-9-creating-a-derived-hierarchy-using-master-data-manager.md)  
  
  
