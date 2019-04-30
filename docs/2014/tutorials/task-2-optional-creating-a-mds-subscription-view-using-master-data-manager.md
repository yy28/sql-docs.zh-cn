---
title: 任务 2（可选）：创建 MDS 订阅视图使用主数据管理器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4596485b4eebeba66028d03f5a54b3ee2461205b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198881"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>任务 2（可选）：使用主数据管理器创建 MDS 订阅视图
  在此任务中，创建订阅视图以公开**供应商**中的实体**供应商**模型对其他应用程序。 在当前版本的教程中，您将不使用此视图。  
  
1.  切换到的主页**主数据管理器**([http://localhost/MDS](http://localhost/MDS)) 通过单击**SQL Server 2012 Master Data Services**顶部。  
  
2.  单击**集成管理**。  
  
3.  单击**创建视图**菜单栏上。  
  
     ![添加新的订阅视图按钮](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "添加新的订阅视图按钮")  
  
4.  单击 **+ （加）** 创建订阅视图工具栏上的图标。  
  
5.  在中**创建订阅视图**窗格中，键入**供应商**有关**订阅视图名称**。  
  
6.  选择**供应商**有关**模型**。  
  
7.  选择**VERSION_1**有关**版本**。  
  
8.  选择**供应商**有关**实体**。  
  
9. 选择**叶成员**有关**格式**。  
  
     ![保存订阅视图按钮](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "保存订阅查看按钮")  
  
10. 单击**保存**在工具栏上，若要保存订阅视图。 此操作将在名为 SQL Server 中创建视图**供应商**。 您可以使用 SQL Server Management Studio (SSMS) 确认这一点。  
  
## <a name="next-step"></a>下一步  
 [任务 3&#40;可选&#41;:查看订阅视图](task-3-optional-reviewing-the-subscription-views.md)  
  
  
