---
title: "指定合并订阅类型和冲突解决优先级 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "02/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "合并复制冲突解决 [SQL Server 复制]，合并订阅解决程序"
  - "冲突解决 [SQL Server 复制], 合并复制"
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 指定合并订阅类型和冲突解决优先级 (SQL Server Management Studio)
  可以在新建订阅向导的 **“订阅类型”** 页上指定合并订阅类型和冲突解决优先级。 有关使用此向导的详细信息，请参阅 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) 和 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
 在创建订阅，但是优先级可以更改服务器订阅类型订阅类型不能修改 **订阅属性-\< 发布服务器>: \< 发布数据库>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 和 [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
### 指定合并订阅类型和冲突解决优先级  
  
1.  在新建订阅向导的 **“订阅类型”** 页上，为 **“订阅类型”** 选项选择 **“客户端”** 或 **“服务器”** 。  
  
2.  如果您选择一种订阅类型的 **服务器**, ，还可输入的值 (0.00 到 99.99) **冲突解决的优先级** 选项。  
  
### 修改冲突解决优先级  
  
1.  在 **订阅属性-\< 发布服务器>: \< 发布数据库>** 在发布服务器上，输入的值 (0.00 到 99.99) **优先级** 选项。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 另请参阅  
 [高级合并复制冲突的检测和解决](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  