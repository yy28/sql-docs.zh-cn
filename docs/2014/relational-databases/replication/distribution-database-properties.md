---
title: 分发数据库属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distdbproperties.f1
helpviewer_keywords:
- Distribution Database Properties dialog box
ms.assetid: 0f404ab9-1237-4936-8df5-888baab6a245
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 89b8381de605ab3736afc6ac8e3a7da0d53bf9e6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796879"
---
# <a name="distribution-database-properties"></a>分发数据库属性
  可以使用 **“分发数据库属性”** 对话框查看数据库的多个属性，以及为数据库设置事务保持期和历史记录保持期。  
  
## <a name="options"></a>选项  
 **名称**  
 分发数据库的名称，默认值为“distribution”（只读）。  
  
 **文件位置**  
 数据库文件和日志文件的位置（只读）。  
  
 **事务保持期**  
 也称为分发保持期。 为事务复制存储的事务时间长度。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)。  
  
 **历史记录保持期**  
 为所有类型的复制存储的历史记录元数据的时间长度。  
  
 **队列读取器代理安全性**  
 队列读取器代理由带有排队更新订阅的事务复制使用。 如果在新建发布向导的 **“发布类型”** 页上选择 **“带有更新订阅的事务发布”** ，将自动创建队列读取器代理。 单击“安全设置…”可以更改运行代理并连接到分发服务器时所使用的帐户。  
  
 还可以在此页上选择 **“创建队列读取器代理”** （如果已创建该代理，此选项将被禁用），来创建队列读取器代理。  
  
 下面两点说明了队列读取器代理的其他连接信息：  
  
-   使用 **“发布服务器属性”** 对话框中指定的凭据，该代理可以连接到发布服务器。该对话框可以在 **“分发服务器属性”** 对话框的 **“发布服务器”** 页中找到。  
  
-   使用在新建订阅向导中为分发代理指定的凭据，该代理可以连接到订阅服务器。  
  
 有关详细信息，请参阅\\ [Replication Agent Security Model](security/replication-agent-security-model.md)。  
  
## <a name="see-also"></a>请参阅  
 [“配置分发”](configure-distribution.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [ssSDSFull](create-a-push-subscription.md)   
 [查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)  
  
  
