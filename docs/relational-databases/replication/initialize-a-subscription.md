---
title: "初始化订阅 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "快照复制 [SQL Server], 初始化订阅"
  - "事务复制, 初始化订阅"
  - "初始化订阅 [SQL Server 复制]"
  - "订阅 [SQL Server 复制], 初始化"
  - "初始化订阅 [SQL Server 复制], 关于初始化订阅"
  - "合并复制 [SQL Server 复制], 初始化订阅"
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# 初始化订阅
  必须初始化复制拓扑中的订阅服务器，以使其具有来自它们所订阅的发布中各项目的架构副本以及全部所需复制对象（如存储过程、触发器和元数据表）。 另外，订阅服务器通常接收初始数据集。 默认的初始化方法使用完整的快照，其中包含架构、复制对象和数据；但没有完整的快照也可以初始化发布。  
  
 有关详细信息，请参阅 [Initialize a Subscription with a Snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md) 和 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
  