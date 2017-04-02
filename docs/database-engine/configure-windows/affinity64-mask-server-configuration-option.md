---
title: "affinity64 mask 服务器配置选项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "处理器关联 [SQL Server]"
  - "affinity64 mask 选项"
  - "绑定处理器 [SQL Server]"
ms.assetid: 75ed08c7-f85c-4e15-9ee1-e7bc545d3293
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# affinity64 mask 服务器配置选项
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  affinity64 mask 将处理器绑定到特定的线程，这与 affinity mask 选项相似。 使用 affinity mask 可以绑定前 32 个处理器，而使用 affinity64 mask 可以绑定计算机上余下的处理器。 此选项仅出现在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 64 位版本中。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] 转为使用 [ALTER SERVER CONFIGURATION (Transact-SQL) ](../../t-sql/statements/alter-server-configuration-transact-sql.md)。  
  
## 另请参阅  
 [affinity mask 服务器配置选项](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  