---
title: 任务 2： 将供应商数据上载到 MDS 外接程序用于 Excel 的 MDS |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 36e50a34f708bc13da489591d73ca0521cdb5a6b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101207"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>任务 2：使用用于 Excel 的 MDS 外接程序将供应商数据上载到 MDS
  在本任务中，将发布到的已清理和供应商数据**MDS**使用**MDS 外接程序 excel**。 创建名为实体**供应商**中**供应商**在上一课中创建的模型。 该实体对于 Excel 文件中的每一列具有一个属性。 Supplier 实体的 Code 和 Name 属性分别对应于**SupplierID**并**Supplier Name** Excel 中的列。  
  
1.  打开**清理和匹配 Suppliers.xls**中**Excel**。  
  
2.  按**CTRL + A**以选择整个数据。 它是**重要**电子表格中选择整个数据。  
  
3.  单击**主数据**菜单栏上。  
  
4.  单击**创建实体**功能区上的按钮。  
  
     ![Excel-Master 数据选项卡-创建实体按钮](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel 的 Master 数据选项卡的创建实体按钮")  
  
5.  在中**管理连接**对话框中，如果您看不到连接**本地 MDS 服务器**下**现有连接**，执行以下操作：  
  
    1.  选择**创建新的连接**，然后单击**新建**按钮。  
  
    2.  在**添加新连接**对话框中，键入**本地 MDS 服务器**有关**说明**并**http://localhost/MDS**为**MDS 服务器地址**，然后单击**确定**以关闭对话框。  
  
6.  在中**管理连接**对话框中，选择**本地 MDS 服务器**(http://localhost/MDS)，单击**测试**对连接进行测试。 单击**确定**消息框上。  
  
7.  单击**Connect**连接到 MDS 服务器。  
  
8.  在中**创建实体**对话框中，选择**供应商**有关**模型**。  
  
9. 絋粄**VERSION_1**选择了**版本**。  
  
10. 输入**供应商**有关**新实体名称**。  
  
11. 选择**SupplierID**有关**包含的唯一标识符的列**（您还可以代码自动生成） 的字段。 您实质上映射**SupplierID**中的列**Excel**到**代码**属性的**供应商**实体。  
  
12. 选择**Supplier Name**有关**包含名称的列**字段。 您实质上映射**Supplier Name**中的列**Excel**到**名称**属性的**供应商**实体。 **代码**并**名称**属性是 MDS 中的实体的必需属性。  
  
     ![创建实体对话框](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "创建实体对话框")  
  
13. 单击**确定**若要在 MDS 上创建该实体，将主数据发布到实体，并关闭**创建实体**对话框。  
  
14. 现在，应看到一个标题为的新工作表**供应商**，这是添加到 Excel 电子表格的实体的名称应在工作表的顶部看到，工作表连接到 MDS 服务器。 请注意，原始工作表 (标题为**Sheet1**) 仍然存在。  
  
     ![Excel-供应商和 Sheet1 选项卡](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel-供应商和 Sheet1 选项卡")  
  
     ![Excel-显示 MDS 连接详细信息](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel-显示 MDS 连接详细信息")  
  
15. 保持**Excel**打开。  
  
## <a name="next-task"></a>下一个任务  
 [任务 3：在主数据管理器中验证数据](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
