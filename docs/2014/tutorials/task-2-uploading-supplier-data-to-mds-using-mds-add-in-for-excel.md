---
title: 任务 2：使用 Excel 的 MDS 外接程序将供应商数据上载到 MDS |微软文档
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
ms.openlocfilehash: 4e3cd4cecd88bcad83c6e9f2a59ecd5f225fb02a
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487691"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>任务 2：使用用于 Excel 的 MDS 外接程序将供应商数据上传到 MDS
  在此任务中，使用 Excel 的**MDS 外接程序**将清理和供应商数据发布到**MDS。** 在上一课中创建的**供应商**模型中创建名为 **"供应商**"的实体。 该实体对于 Excel 文件中的每一列具有一个属性。 供应商实体的代码和名称属性对应于 Excel 中的**供应商 ID**和**供应商名称**列。  
  
1.  在**Excel**中打开**清洁和匹配供应商.xls。**  
  
2.  按**CTRL+A**选择整个数据。 请务必选择**important**电子表格中的整个数据。  
  
3.  单击菜单栏上的 **"主数据**"。  
  
4.  单击功能区上的 **"创建实体"** 按钮。  
  
     ![Excel -“主数据”选项卡 -“创建实体”按钮](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel -“主数据”选项卡 -“创建实体”按钮")  
  
5.  在 **"管理连接"** 对话框中，如果在**现有连接**下看不到与**本地 MDS 服务器**的连接，则执行以下操作：  
  
    1.  选择 **"创建新连接**"，然后单击 **"新建"** 按钮。  
  
    2.  在 **"添加新连接**"对话框中，键入 **"本地 MDS 服务器****说明"** 和 **"http：/\/本地主机/MDS MDS**用于**MDS 服务器地址**"，然后单击"**确定"** 以关闭该对话框。  
  
6.  在 **"管理连接"** 对话框中，选择 **"本地 MDS 服务器**" （）`http://localhost/MDS`"，单击 **"测试**"以测试连接。 单击消息框上的 **"确定**"。  
  
7.  单击"**连接**"以连接到 MDS 服务器。  
  
8.  在 **"创建实体"** 对话框中，选择**模型**的**供应商**。  
  
9. 确保为**版本**选择了**VERSION_1。**  
  
10. 输入 **"新实体名称**的**供应商**"。  
  
11. 为**包含唯一标识符字段的列**选择 **"供应商 ID"（** 您也可以自动生成代码）。 您实质上是将**Excel**中的**供应商 ID**列映射到**供应商**实体**的代码**属性。  
  
12. 为**包含名称字段的列**选择 **"供应商名称**"。 您实质上是将**Excel**中的 **"供应商名称**"列映射到**供应商**实体**的名称**属性。 **代码**和**名称**属性是 MDS 中实体的必填属性。  
  
     ![“创建实体”对话框](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "“创建实体”对话框")  
  
13. 单击 **"确定"** 在 MDS 上创建实体，将主数据发布到实体，并关闭 **"创建实体"** 对话框。  
  
14. 现在，您应该看到一个名为 **"供应商**"的新工作表 ，该工作表是实体的名称，添加到 Excel 电子表格中，在工作表顶部应看到工作表已连接到 MDS 服务器。 请注意，原始工作表（标题为工作表**1）** 仍然存在。  
  
     ![Excel -“供应商”和“Sheet1”选项卡](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel -“供应商”和“Sheet1”选项卡")  
  
     ![Excel - 显示 MDS 连接详细信息](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - 显示 MDS 连接详细信息")  
  
15. 保持**Excel**打开。  
  
## <a name="next-task"></a>下一个任务  
 [任务 3：在主数据管理器中验证数据](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
