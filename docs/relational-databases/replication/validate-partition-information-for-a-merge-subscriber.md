---
title: "验证合并订阅服务器的分区信息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "合并复制数据验证 [SQL Server 复制], 分区"
  - "参数化筛选器 [SQL Server 复制], 验证分区信息"
  - "验证分区信息"
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 验证合并订阅服务器的分区信息
  在为合并发布定义参数化行筛选器时，将使用引用订阅服务器信息（如订阅服务器的登录名）的函数。 默认情况下，每次同步前和快照应用于订阅服务器时，复制都将根据此函数验证订阅服务器信息。 验证过程确保每个订阅服务器的数据都进行了正确的分区。 验证行为由控制 **validate_subscriber_info** 发布属性，可以使用更改 [sp_changemergepublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 或在 **订阅选项** 页 **发布属性** 对话框。 有关更改发布属性的详细信息，请参阅 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
## 分区验证的工作机制  
 当发布进行筛选，例如，使用函数 **suser_sname （)**, ，合并代理将初始快照应用于基于对有效的数据的每个订阅服务器 **suser_sname （)** 表达式。  
  
 如果验证已启用，则当订阅服务器重新连接到发布服务器进行下次同步处理时，合并代理将验证订阅服务器上的信息，并确保每个订阅服务器的分区与初始快照中所接收的相同。 针对每个后续合并或快照应用程序，合并代理将验证每个订阅服务器的分区。  
  
 如果合并代理检测到在筛选表达式中使用的函数返回了一个不同于其在初始快照中返回的值，则合并或快照应用程序将失败，而且此订阅服务器的订阅可能需要重新初始化。 可能需要重新初始化以避免出现问题（如果更改了订阅服务器的合并设置，则可能引发这些问题），不过，将订阅服务器上的信息更改回初始快照时使用的值（如登录名）可能也足以避免出现问题。  
  
 合并代理验证分区时，除了对筛选表达式使用的所有函数返回的值验证分区之外，代理还会检查快照的生成是否先于令其无效的更改，如元数据清除操作或架构更改。 如果分区快照太旧，合并代理将返回一个错误，并且必须根据当前常规快照为此订阅服务器重新生成分区快照。  
  
## 另请参阅  
 [管理和 #40;复制和 #41;](../../relational-databases/replication/administration/administration-replication.md)   
 [复制管理最佳实践](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [重新初始化订阅](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [验证已复制的数据](../../relational-databases/replication/validate-replicated-data.md)  
  
  