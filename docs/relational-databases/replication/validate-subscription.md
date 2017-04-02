---
title: "验证单个订阅 | Microsoft Docs"
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
  - "sql13.rep.validate.validateandresynch.f1"
helpviewer_keywords: 
  - "“验证单个订阅”对话框"
ms.assetid: 74bdf5e1-b886-4284-b5fb-332bf79ae083
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# 验证单个订阅
  可以使用 **“验证单个订阅”** 对话框，指定在下次运行订阅的合并代理时应对针对合并发布的订阅进行验证。 验证的结果显示在复制监视器中。 有关详细信息，请参阅 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  
  
 它也是用户可以通过右键单击中的发布来验证对合并发布的所有订阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，然后单击 **都验证所有订阅**。  
  
## 选项  
 **上次尝试验证的日期**  
 最后一个包含订阅验证（无论验证是否成功）的合并代理会话的日期。  
  
 **上次成功验证的日期**  
 最后一个包含成功订阅验证的合并代理会话的日期。  
  
 **验证此订阅**  
 选择此选项可验证订阅。  
  
 **选项**  
 单击以访问 **订阅验证选项** 对话框中，允许您指定是否使用行计数验证还是使用二进制校验和验证。  
  
## 另请参阅  
 [验证已复制的数据](../../relational-databases/replication/validate-replicated-data.md)  
  
  