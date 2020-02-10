---
title: 任务2（可选）：使用主数据管理器创建 MDS 订阅视图 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e6cbed42d059714dde1c82dbb50edf8ccc1dd65b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484726"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>任务 2（可选）：使用主数据管理器创建 MDS 订阅视图
  在此任务中，您将创建一个订阅视图，以便向其他应用程序公开**供应商**模型中的**供应商**实体。 在当前版本的教程中，您将不使用此视图。  
  
1.  单击顶部**SQL Server 2012 Master Data Services** ， **** 切换到[http://localhost/MDS](http://localhost/MDS)主数据管理器（）的主页。  
  
2.  单击 "**集成管理**"。  
  
3.  单击菜单栏上的 "**创建视图**"。  
  
     ![“添加新的订阅视图”按钮](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "“添加新的订阅视图”按钮")  
  
4.  单击工具栏上的 " **+" （加号）** 图标可创建订阅视图。  
  
5.  在 "**创建订阅视图**" 窗格中，键入 "**供应商**" 作为**订阅视图名称**。  
  
6.  选择**模型**的**供应商**。  
  
7.  为 "**版本**" 选择**VERSION_1** 。  
  
8.  选择**实体**的**供应商**。  
  
9. 选择**格式**的**叶成员**。  
  
     ![“保存订阅视图”按钮](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "“保存订阅视图”按钮")  
  
10. 单击工具栏上的 "**保存**" 以保存订阅视图。 此操作在 SQL Server 名为 "**供应商**" 中创建视图。 您可以使用 SQL Server Management Studio (SSMS) 确认这一点。  
  
## <a name="next-step"></a>下一步  
 [任务 3 &#40;可选&#41;：查看订阅视图](task-3-optional-reviewing-the-subscription-views.md)  
  
  
