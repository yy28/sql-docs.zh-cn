---
title: 任务2：使用 MDS Add-in for Excel 将供应商数据上载到 MDS |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 57a5044ccee040ef1eba95925c689f48739c259f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484661"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>任务 2：使用用于 Excel 的 MDS 外接程序将供应商数据上载到 MDS
  在此任务中，将使用**MDS Add-in for Excel**将清理和供应商数据发布到**MDS** 。 您在上一课中创建的**供应商**模型中创建一个名为 "**供应商**" 的实体。 该实体对于 Excel 文件中的每一列具有一个属性。 供应商实体的代码和名称属性与 Excel 中的 "**供应商**名称" 和 "**供应商名称**" 列相对应。  
  
1.  在**Excel**中打开**清理并匹配的 "供应商"。**  
  
2.  按**CTRL + A**以选择整个数据。 在电子表格中选择整个数据很**重要**。  
  
3.  单击菜单栏上的 "**主数据**"。  
  
4.  单击功能区上的 "**创建实体**" 按钮。  
  
     ![Excel -“主数据”选项卡 -“创建实体”按钮](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel -“主数据”选项卡 -“创建实体”按钮")  
  
5.  在 "**管理连接**" 对话框中，如果在 "**现有连接**" 下看不到**本地 MDS 服务器**的连接，请执行以下操作：  
  
    1.  选择 "**创建新连接**"，然后单击 "**新建**按钮"。  
  
    2.  在 "**添加新连接**" 对话框中，键入 "**本地 MDS server** **说明**" 和**http://localhost/MDS** " **Mds 服务器地址**"，然后单击 **"确定"** 以关闭对话框。  
  
6.  在 "**管理连接**" 对话框中，选择 "**本地 MDS 服务器**" （http://localhost/MDS)，然后单击 "**测试**" 以测试连接。 在消息框中单击 **"确定"** 。  
  
7.  单击 "**连接**" 以连接到 MDS 服务器。  
  
8.  在 "**创建实体**" 对话框中，选择**模型**的 "**供应商**"。  
  
9. 确保为 "**版本**" 选择**VERSION_1** 。  
  
10. 为 "**新实体名称**" 输入 "**供应商**"。  
  
11. 为**包含唯一标识符**字段的列选择 "**供应商**" （也可以自动生成代码）。 你实质上是将**Excel**中的 "**供应商**" 列映射到**供应商**实体的 "**代码**" 属性。  
  
12. 为**包含 "名称"** 字段的列选择 "**供应商名称**"。 你实质上是将**Excel**中的 "**供应商名称**" 列映射到**供应商**实体的**name**属性。 在 MDS 中，**代码**和**名称**属性是实体的必需属性。  
  
     ![“创建实体”对话框](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "“创建实体”对话框")  
  
13. 单击 **"确定"** 以在 MDS 上创建实体，将主数据发布到实体，并关闭 "**创建实体**" 对话框。  
  
14. 现在，你应该会看到一个名为 "**供应商**" 的新工作表，该工作表是实体的名称，添加到 Excel 电子表格，然后在工作表的顶部，你应看到该工作表已连接到 MDS 服务器。 请注意，原始工作表（标题为**Sheet1**）仍然存在。  
  
     ![Excel -“供应商”和“Sheet1”选项卡](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel -“供应商”和“Sheet1”选项卡")  
  
     ![Excel - 显示 MDS 连接详细信息](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - 显示 MDS 连接详细信息")  
  
15. 使**Excel**保持打开状态。  
  
## <a name="next-task"></a>下一个任务  
 [任务 3：在主数据管理器中验证数据](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
