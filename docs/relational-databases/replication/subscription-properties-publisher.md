---
title: "订阅属性 - 发布服务器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subproperties.publisher.f1"
helpviewer_keywords: 
  - "“订阅属性”对话框"
ms.assetid: d4b2bc8b-0431-4331-8305-8992c96d0d34
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 订阅属性 - 发布服务器
  使用发布服务器上的 **“订阅属性”** 对话框可以查看和设置推送订阅的属性。 您还可以查看请求订阅的某些属性，订阅服务器上的 **“订阅属性”** 对话框可以显示其他属性，并允许修改属性。  
  
 **“订阅属性”** 对话框中的每一个属性都包含相应的说明。 单击一个属性可以查看该属性的说明（显示于对话框的底部）。 本主题提供许多属性的其他相关信息，大多数属性只能在发布服务器上针对推送订阅显示。 属性分为以下类别：  
  
-   适用于所有订阅的属性。  
  
-   适用于事务订阅的属性。  
  
-   适用于合并订阅的属性。  
  
 如果某个选项显示为只读，则只能在创建订阅时对其进行设置。 若要设置在新建订阅向导中不可用的选项，请使用存储过程创建订阅。 有关详细信息，请参阅 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) 和 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
## 用于所有订阅的选项  
 **安全性**  
 单击 **代理进程帐户** 行，然后单击属性按钮 (**...**) 若要更改分发代理或合并代理运行在分发服务器的帐户。 若要更改在其下的分发代理或合并代理将其连接到订阅服务器上的帐户，请单击 **订阅服务器连接**, ，然后单击属性按钮 (**...**)。  
  
 有关每个代理所需权限的详细信息，请参阅 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## 用于事务订阅的选项  
 **防止事务循环**  
 确定分发代理是否将在订阅服务器上发起的事务发送回订阅服务器。 此选项用于双向事务复制。 有关详细信息，请参阅 [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md)。  
  
 **可更新订阅**  
 确定是否将订阅服务器更改复制回发布服务器。 使用排队更新或立即更新可以复制更改。 **“订阅服务器更新方法”** 选项用于确定要使用的方法。 有关详细信息，请参阅 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
## 用于合并订阅的选项  
 **分区定义(HOST_NAME)**  
 以确定订阅服务器应接收的数据的同步期间合并复制的发布使用参数化筛选器，用于计算两个系统函数 （和 / 或如果筛选器引用了这两个函数） 之一︰ **suser_sname （)** 或 **host_name （)**。 默认情况下， **host_name （)** 返回在其合并代理正在运行，但您可以替代此值在新建订阅向导中的计算机的名称。 有关详细信息参数化筛选器和覆盖 **host_name （)**, ，请参阅 [参数化行筛选器](../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
 **订阅类型** 和 **优先级**  
 显示订阅是客户端订阅还是服务器订阅（在创建订阅后不能更改）。 服务器订阅可以将数据重新发布到其他订阅服务器，并可以为服务器订阅分配冲突解决优先级。  
  
 如果在新建订阅向导中选择了服务器订阅类型，则会为该订阅服务器分配一个在冲突解决过程中使用的优先级。  
  
 **交互式解决冲突**  
 确定是否使用交互式冲突解决程序用户界面解决合并同步过程中的冲突。 这需要将 **“使用 Windows 同步管理器”** 的值设置为 **“启用”**。 有关详细信息，请参阅 [Interactive Conflict Resolution](../../relational-databases/replication/merge/interactive-conflict-resolution.md)。  
  
## 另请参阅  
 [查看和修改请求订阅属性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [查看和修改推送订阅属性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  