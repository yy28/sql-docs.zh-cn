---
title: "订阅类型 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7e590134637b10236f71e8468b42c9228badfd4
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="subscription-type"></a>订阅类型
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  合并复制提供了两种订阅类型：服务器和客户端（以前的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本分别称为全局和本地）。 使用服务器订阅的订阅服务器可以：  
  
-   将数据重新发布到其他订阅服务器。  
  
-   作为备用同步伙伴。  
  
-   按照您设置的优先级解决冲突。  
  
 大多数订阅服务器不需要此功能，可以使用客户端订阅。 客户端订阅仍然允许进行冲突检测和解决，但不为订阅服务器分配优先级：第一个将更改提交到发布服务器的订阅服务器将在该更改引起的任意冲突中获胜。  
  
> [!NOTE]  
>  创建订阅之后，不能更改订阅类型。  
  
## <a name="options"></a>“常规”  
 **订阅属性**  
 对于每个订阅服务器，请从 **“订阅类型”** 列的下拉列表框中选择 **“客户端”** 或 **“服务器”** 。 对于使用服务器订阅的订阅服务器，请在 **“冲突解决的优先级”** 列中输入 0 和 99.99 之间的数字（数字越大，订阅服务器的优先级越高）。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
