---
title: 任务 2（可选）：使用主数据管理器创建 MDS 订阅视图 |微软文档
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
ms.openlocfilehash: cc923792adc3fefb5ebaab9e225169648394c71f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484707"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>任务 2（可选）：使用主数据管理器创建 MDS 订阅视图
  在此任务中，您将创建一个订阅视图，以将**供应商模型中的供应商**实体公开给其他应用程序。 **Supplier** 在当前版本的教程中，您将不使用此视图。  
  
1.  单击顶部的**SQL Server 2012 主数据服务**，切换到**主数据管理器**（`http://localhost/MDS`） 的主页。  
  
2.  单击**集成管理**。  
  
3.  单击菜单栏上的 **"创建视图**"。  
  
     ![“添加新的订阅视图”按钮](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "“添加新的订阅视图”按钮")  
  
4.  单击工具栏上的 **+（加号）** 图标以创建订阅视图。  
  
5.  在 **"创建订阅视图"** 窗格中，键入**订阅视图名称****的供应商**。  
  
6.  为**模型**选择**供应商**。  
  
7.  选择**版本****VERSION_1。**  
  
8.  为**实体**选择**供应商**。  
  
9. 为 **"格式****"选择"叶"成员**。  
  
     ![“保存订阅视图”按钮](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "“保存订阅视图”按钮")  
  
10. 单击工具栏上的 **"保存**"以保存订阅视图。 此操作在 SQL Server 中创建名为 **"供应商"的**视图。 您可以使用 SQL Server Management Studio (SSMS) 确认这一点。  
  
## <a name="next-step"></a>下一步  
 [任务 3 &#40;可选&#41;：查看订阅视图](task-3-optional-reviewing-the-subscription-views.md)  
  
  
