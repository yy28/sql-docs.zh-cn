---
title: "订阅类型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subscriptiontype.f1"
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 订阅类型
  合并复制提供了两种订阅类型︰ 服务器和客户端 (引用在以前版本的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全局和本地，分别)。 使用服务器订阅的订阅服务器可以：  
  
-   将数据重新发布到其他订阅服务器。  
  
-   作为备用同步伙伴。  
  
-   按照您设置的优先级解决冲突。  
  
 大多数订阅服务器不需要此功能，可以使用客户端订阅。 客户端订阅仍然允许进行冲突检测和解决，但不为订阅服务器分配优先级：第一个将更改提交到发布服务器的订阅服务器将在该更改引起的任意冲突中获胜。  
  
> [!NOTE]  
>  创建订阅之后，不能更改订阅类型。  
  
## 选项  
 **订阅属性**  
 对于每个订阅服务器上，选择 **客户端** 或 **服务器** 从下拉列表框中 **订阅类型** 列。 对于具有服务器订阅的订阅服务器，输入一个数字介于 0 和 99.99 中的之间 **冲突解决的优先级** 列 （数字越大，以使订阅服务器的优先级就越高）。  
  
## 另请参阅  
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [创建推送订阅](../../relational-databases/replication/create-a-push-subscription.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  