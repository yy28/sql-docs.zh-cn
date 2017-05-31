---
title: "分发数据库属性 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.configdistwizard.distdbproperties.f1
helpviewer_keywords:
- Distribution Database Properties dialog box
ms.assetid: 0f404ab9-1237-4936-8df5-888baab6a245
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7e086caef0d106066a3f8a9f42d1bbd51d473826
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="distribution-database-properties"></a>分发数据库属性
  可以使用 **“分发数据库属性”** 对话框查看数据库的多个属性，以及为数据库设置事务保持期和历史记录保持期。  
  
## <a name="options"></a>选项  
 **名称**  
 分发数据库的名称，默认值为“distribution”（只读）。  
  
 **文件位置**  
 数据库文件和日志文件的位置（只读）。  
  
 **事务保持期**  
 也称为分发保持期。 为事务复制存储的事务时间长度。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 **历史记录保持期**  
 为所有类型的复制存储的历史记录元数据的时间长度。  
  
 **队列读取器代理安全性**  
 队列读取器代理由带有排队更新订阅的事务复制使用。 如果在新建发布向导的 **“发布类型”** 页上选择 **“带有更新订阅的事务发布”** ，将自动创建队列读取器代理。 单击 **“安全设置…”** 可以更改运行代理并连接到分发服务器时所使用的帐户。  
  
 还可以在此页上选择 **“创建队列读取器代理”** （如果已创建该代理，此选项将被禁用），来创建队列读取器代理。  
  
 下面两点说明了队列读取器代理的其他连接信息：  
  
-   使用 **“发布服务器属性”** 对话框中指定的凭据，该代理可以连接到发布服务器。该对话框可以在 **“分发服务器属性”** 对话框的 **“发布服务器”** 页中找到。  
  
-   使用在新建订阅向导中为分发代理指定的凭据，该代理可以连接到订阅服务器。  
  
 有关详细信息，请参阅  [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## <a name="see-also"></a>另请参阅  
 [配置分发](../../relational-databases/replication/configure-distribution.md)   
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  
