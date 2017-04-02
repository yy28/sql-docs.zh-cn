---
title: "双向事务复制 | Microsoft Docs"
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
  - "双向复制"
  - "事务复制, 双向复制"
  - "双向事务复制"
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# 双向事务复制
  双向事务复制是一种特定的事务复制拓扑，它允许两台服务器相互交换更改：每台服务器均发布数据，然后从另一台服务器订阅包含相同数据的发布。  **@Loopback_detection** 参数 [sp_addsubscription & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 设置为 TRUE 以确保更改只发送到订阅服务器上，并且不会导致将更改发回发布服务器。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更高版本中，对等事务复制，也支持此拓扑，但双向复制可提高的性能。  
  
## 另请参阅  
 [对等事务复制](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  