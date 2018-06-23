---
title: 任务 1 （先决条件）： 在 MDS 中删除供应商数据 |Microsoft 文档
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
ms.assetid: 6f0a4287-7fd4-4f18-b7e4-a5191a9d4a3c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1189c064ec1a55da1c77837d1533855266ed4274
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138766"
---
# <a name="task-1-prerequisite-removing-supplier-data-in-mds"></a>任务 1（先决条件）：删除 MDS 中的供应商数据
  在本任务中，您将删除在 MDS 中存储的供应商数据。 使用手动将数据上载**MDS Excel 外接程序**在上一课中。 您在本课中创建的 SSIS 包将自动为您将数据上载到 MDS。 因此，在测试该 SSIS 包之前，您需要从 MDS 删除供应商数据，删除派生的层次结构，删除供应商和状态实体，并且创建不含数据的供应商实体。  
  
1.  启动**主数据管理器**通过导航到**http://localhost/MDS**或的网站和应用程序时指定配置 MDS。 如果您将保存**主数据管理器**打开，请单击**SQL Server 2012 Master Data Services**在顶部切换到**主页**。  
  
2.  单击**系统管理**中**管理任务**部分。  
  
3.  将鼠标悬停**管理**上菜单并单击**派生层次结构**。 你需要删除派生层次结构**SuppliersInState**之前删除中的实体**供应商**模型。  
  
4.  选择**SuppliersInState**从**派生层次结构**列表，然后单击**X (Delete)** 工具栏上的按钮。  
  
5.  单击**确定**以确认删除。  
  
6.  将鼠标悬停**管理**上菜单并单击**实体**。  
  
7.  单击**供应商**单击**删除 (X)** 工具栏删除该实体上的按钮。 单击**确定**消息框上。  
  
8.  重复上述步骤以删除**状态**实体。  
  
9. 请不要关闭**主数据管理器**。  
  
10. 切换到 Excel 窗口具有**Cleansed 和匹配 Suppliers.xls**文件打开。 切换到**Sheet1**底部的选项卡。  
  
11. 仅选择**第一行使用标头**。 不要选择任何其他行。 您要基于 Excel 列创建实体，但不想上载任何数据。 因此，您仅选择第一行和标题。  
  
12. 单击**主数据**菜单栏上。  
  
13. 单击**创建实体**从功能区。  
  
14. 在**管理连接**对话框中，如果你看不到连接**本地 MDS 服务器**下**现有连接**，执行以下操作：  
  
    1.  选择**创建新的连接**，然后单击**新建**按钮。  
  
    2.  在添加新连接对话框中，键入**本地 MDS 服务器**为**说明**和**http://localhost/MDS**为**MDS 服务器地址**，单击**确定**以关闭对话框。  
  
15. 在**管理连接**对话框中，选择**本地 MDS 服务器**(http://localhost/MDS)，单击**测试**对连接进行测试。 单击**确定**消息框上。  
  
16. 单击**连接**要与 MDS 服务器建立连接。  
  
17. 在**创建实体**对话框框中，执行以下操作：  
  
    1.  确认**范围**设置为 **$1: $1**。  
  
    2.  选择**供应商**为**模型**。  
  
    3.  选择**VERSION_1**为**版本**。  
  
    4.  类型**供应商**为**新的实体名称**。  
  
    5.  选择**供应商 Id**为**代码**。  
  
    6.  选择**供应商名称**为**名称**。  
  
    7.  单击**确定**以创建实体并关闭对话框。  
  
18. 关闭**Excel**和**不保存**文件。  
  
19. 在**主数据管理器**，请刷新 internet 浏览器并确认**供应商**实体显示在列表中。  
  
20. 切换到**主页**通过单击**SQL Server 2012 Master Data Services**顶部。  
  
21. 确认**供应商**为选择模型**模型**和**VERSION_1**为选择**版本**。  
  
22. 单击 **“资源管理器”**。 请注意，**供应商**与创建具有所有属性的实体**没有值**。  
  
## <a name="next-step"></a>下一步  
 [任务 2&#40;可选&#41;： 创建 MDS 订阅视图使用主数据管理器](../../2014/tutorials/task-2-optional-creating-a-mds-subscription-view-using-master-data-manager.md)  
  
  