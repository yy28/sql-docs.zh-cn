---
title: 任务 1 （先决条件）： 删除 MDS 中的供应商数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 6f0a4287-7fd4-4f18-b7e4-a5191a9d4a3c
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 74862c1db4ad3c34afc759ba94f36ba5fb896e7e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227697"
---
# <a name="task-1-prerequisite-removing-supplier-data-in-mds"></a>任务 1（先决条件）：删除 MDS 中的供应商数据
  在本任务中，您将删除在 MDS 中存储的供应商数据。 使用手动将数据上载**MDS Excel 外接程序**上一课中。 您在本课中创建的 SSIS 包将自动为您将数据上载到 MDS。 因此，在测试该 SSIS 包之前，您需要从 MDS 删除供应商数据，删除派生的层次结构，删除供应商和状态实体，并且创建不含数据的供应商实体。  
  
1.  启动**主数据管理器**通过导航到**http://localhost/MDS**或网站和应用程序时指定配置 MDS。 如果保持**主数据管理器**打开，请单击**SQL Server 2012 Master Data Services**顶部以切换到**主页**。  
  
2.  单击**系统管理**中**管理任务**部分。  
  
3.  将鼠标悬停**管理**单击菜单上**派生层次结构**。 您需要删除派生层次结构**SuppliersInState**删除中的实体之前**供应商**模型。  
  
4.  选择**SuppliersInState**从**派生层次结构**列表中，单击**X （删除）** 工具栏上的按钮。  
  
5.  单击**确定**以确认删除。  
  
6.  将鼠标悬停**管理**单击菜单上**实体**。  
  
7.  单击**供应商**然后单击**删除 (X)** 工具栏来删除该实体上的按钮。 单击**确定**消息框上。  
  
8.  重复上述步骤以便删除**状态**实体。  
  
9. 不要关闭**主数据管理器**。  
  
10. 切换到 Excel 窗口具有**Cleansed and Matched Suppliers.xls**文件打开。 切换到**Sheet1**底部选项卡。  
  
11. 仅选择**第一行使用标头**。 不要选择任何其他行。 您要基于 Excel 列创建实体，但不想上载任何数据。 因此，您仅选择第一行和标题。  
  
12. 单击**主数据**菜单栏上。  
  
13. 单击**创建实体**从功能区。  
  
14. 在中**管理连接**对话框中，如果您看不到连接**本地 MDS 服务器**下**现有连接**，执行以下操作：  
  
    1.  选择**创建新的连接**，然后单击**新建**按钮。  
  
    2.  在添加新连接对话框中，键入**本地 MDS 服务器**有关**说明**并**http://localhost/MDS**对于**MDS 服务器地址**，然后单击**确定**以关闭对话框。  
  
15. 在中**管理连接**对话框中，选择**本地 MDS 服务器**(http://localhost/MDS)，单击**测试**对连接进行测试。 单击**确定**消息框上。  
  
16. 单击**Connect**建立到 MDS 服务器。  
  
17. 在中**创建实体**对话框框中，执行以下操作：  
  
    1.  确认**范围**设置为 **$1: $1**。  
  
    2.  选择**供应商**有关**模型**。  
  
    3.  选择**VERSION_1**有关**版本**。  
  
    4.  类型**供应商**有关**新实体名称**。  
  
    5.  选择**SupplierID**有关**代码**。  
  
    6.  选择**供应商名称**有关**名称**。  
  
    7.  单击**确定**创建实体并关闭对话框。  
  
18. 关闭**Excel**并**不保存**文件。  
  
19. 在中**主数据管理器**，刷新 internet 浏览器并确认**供应商**实体显示在列表中。  
  
20. 切换到**主页**通过单击**SQL Server 2012 Master Data Services**顶部。  
  
21. 确认**供应商**模型用于**模型**并**VERSION_1**为选择**版本**。  
  
22. 单击 **“资源管理器”**。 请注意，**供应商**实体的所有属性创建具有**没有值**。  
  
## <a name="next-step"></a>下一步  
 [任务 2&#40;可选&#41;： 创建 MDS 订阅视图使用主数据管理器](../../2014/tutorials/task-2-optional-creating-a-mds-subscription-view-using-master-data-manager.md)  
  
  
