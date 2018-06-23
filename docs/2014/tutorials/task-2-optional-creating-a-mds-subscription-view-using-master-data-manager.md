---
title: 任务 2 （可选）： 创建 MDS 订阅视图使用主数据管理器 |Microsoft 文档
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
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4883d4f5c7bef05de9625c2fcb7bac235c0306e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137659"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>任务 2（可选）：使用主数据管理器创建 MDS 订阅视图
  在此任务中，创建订阅视图，以便公开**供应商**中的实体**供应商**模型对其他应用程序。 在当前版本的教程中，您将不使用此视图。  
  
1.  切换到的主页面**主数据管理器**([http://localhost/MDS](http://localhost/MDS)) 通过单击**SQL Server 2012 Master Data Services**顶部。  
  
2.  单击**集成管理**。  
  
3.  单击**创建视图**菜单栏上。  
  
     ![添加一个新的订阅视图按钮](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "添加一个新的订阅视图按钮")  
  
4.  单击 **+ （加）** 创建订阅视图工具栏上的图标。  
  
5.  在**创建订阅视图**窗格中，键入**供应商**为**订阅视图名称**。  
  
6.  选择**供应商**为**模型**。  
  
7.  选择**VERSION_1**为**版本**。  
  
8.  选择**供应商**为**实体**。  
  
9. 选择**叶成员**为**格式**。  
  
     ![保存订阅视图按钮](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "保存订阅视图按钮")  
  
10. 单击**保存**在工具栏上，若要保存订阅视图。 此操作在名为的 SQL Server 中创建视图**供应商**。 您可以使用 SQL Server Management Studio (SSMS) 确认这一点。  
  
## <a name="next-step"></a>下一步  
 [任务 3&#40;可选&#41;： 查看订阅视图](task-3-optional-reviewing-the-subscription-views.md)  
  
  