---
title: "初始化订阅 | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.initializesubscriptions.f1"
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 初始化订阅
  必须先初始化订阅服务器，然后才能接收复制的数据。 订阅服务器可以没有初始的数据集，但对于复制的每个对象以及复制所需的任何元数据表和过程，必须要具有相应的架构。  
  
## 选项  
 **订阅属性**  
 选中复选框在 **初始化** 每个订阅服务器所需初始数据集的列。 如果该复选框为清除状态，将只初始化复制元数据和过程。 有关初始化的订阅不使用快照的详细信息，请参阅 [初始化事务订阅不使用快照](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
 选择 **立即** 从下拉列表框中 **初始化时间** 列可以具有合并代理或分发代理程序传输快照文件应用于订阅服务器上完成此向导后。 如果选择 **“首先同步”** ，代理则会在下次计划运行的时候传输文件。  **“立即”** 选项不可用于对 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]的请求订阅。 在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]的实例上不能运行合并代理和分发代理，因此必须通过其他方法初始化订阅。  
  
> [!NOTE]  
>  该向导可能会提示您连接到分发服务器，以启动分发代理或合并代理的相应作业。  
  
## 另请参阅  
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [创建推送订阅](../../relational-databases/replication/create-a-push-subscription.md)   
 [初始化订阅](../../relational-databases/replication/initialize-a-subscription.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  