---
title: 任务 2： 将供应商数据上载到 MDS 外接程序用于 Excel 的 MDS |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1831fc9ea79027e24d752d05e3b50d3a58d6e06f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016275"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>任务 2：使用用于 Excel 的 MDS 外接程序将供应商数据上载到 MDS
  在此任务中，你已清理和供应商将数据发布到**MDS**使用**MDS add-in for Excel**。 创建名为实体**供应商**中**供应商**你在上一课中创建的模型。 该实体对于 Excel 文件中的每一列具有一个属性。 供应商实体的代码和名称属性对应于**供应商 Id**和**供应商名称**在 Excel 中的列。  
  
1.  打开**清理和匹配 Suppliers.xls**中**Excel**。  
  
2.  按**CTRL + A**来选择整个数据。 它是**重要**电子表格中选择整个数据。  
  
3.  单击**主数据**菜单栏上。  
  
4.  单击**创建实体**功能区上的按钮。  
  
     ![Excel-Master 数据选项卡-创建实体按钮](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel-Master 数据选项卡-创建实体按钮")  
  
5.  在**管理连接**对话框中，如果你看不到连接**本地 MDS 服务器**下**现有连接**，执行以下操作：  
  
    1.  选择**创建新的连接**，然后单击**新建**按钮。  
  
    2.  在**添加新连接**对话框中，键入**本地 MDS 服务器**为**说明**和**http://localhost/MDS**为**MDS 服务器地址**，然后单击**确定**以关闭对话框。  
  
6.  在**管理连接**对话框中，选择**本地 MDS 服务器**(http://localhost/MDS)，单击**测试**对连接进行测试。 单击**确定**消息框上。  
  
7.  单击**连接**连接到 MDS 服务器。  
  
8.  在**创建实体**对话框中，选择**供应商**为**模型**。  
  
9. 确保**VERSION_1**为选择**版本**。  
  
10. 输入**供应商**为**新的实体名称**。  
  
11. 选择**供应商 Id**为**包含的唯一标识符的列**（你还可以生成一个代码自动） 的字段。 实质上映射**供应商 Id**中的列**Excel**到**代码**属性**供应商**实体。  
  
12. 选择**供应商名称**为**包含名称的列**字段。 实质上映射**供应商名称**中的列**Excel**到**名称**属性**供应商**实体。 **代码**和**名称**属性是实体在 MDS 中的必选属性。  
  
     ![创建实体对话框](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "创建实体对话框")  
  
13. 单击**确定**若要创建 MDS 实体，将主数据发布到该实体，并关闭**创建实体**对话框。  
  
14. 现在，你应看到标题为的新工作表**供应商**，它是实体，添加到 Excel 电子表格的名称，并且在工作表的顶部，你应看到该工作表中已连接到 MDS 服务器。 请注意，原始工作表 (标题为**Sheet1**) 仍存在。  
  
     ![Excel-供应商和 Sheet1 选项卡](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel-供应商和 Sheet1 选项卡")  
  
     ![Excel-显示 MDS 连接详细信息](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel-显示 MDS 连接详细信息")  
  
15. 保留**Excel**打开。  
  
## <a name="next-task"></a>下一个任务  
 [任务 3：在主数据管理器中验证数据](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  