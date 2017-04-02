---
title: "可更新订阅 | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.updatablesubscriptions.f1"
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 可更新订阅
  使用事务复制，复制的数据应被视为是只读的;但是，您可以修改复制的数据在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过使用可更新订阅的订阅服务器。 如果需要在订阅服务器上修改数据，请根据您的要求选择下列选项之一。  
  
|可更新订阅类型|要求|  
|---------------------------------|------------------|  
|立即更新|必须连接发布服务器和订阅服务器才能更新订阅服务器上的数据。|  
|排队更新|不必连接发布服务器和订阅服务器即可更新订阅服务器上的数据。 可以在脱机状态下进行更新，之后还可以在发布服务器与订阅服务器之间同步更新。|  
  
## 选项  
 **复制订阅服务器更改**  
 选中复选框在 **复制** 应该能够进行更新每个订阅服务器的列。 有关可进行更新，这些订阅者从下拉列表框中选择相应的选项 **在发布服务器提交** 列︰  
  
-   对于立即更新订阅，请选择 **“同时提交更改”** 。  
  
-   对于排队更新订阅，请选择 **“对更改进行排队并在可能时提交”** 。  
  
## 另请参阅  
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [创建推送订阅](../../relational-databases/replication/create-a-push-subscription.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)   
 [事务复制的可更新订阅](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  