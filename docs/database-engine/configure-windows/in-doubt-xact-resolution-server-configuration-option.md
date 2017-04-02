---
title: "in-doubt xact resolution 服务器配置选项 | Microsoft Docs"
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
  - "分布式事务 [SQL Server], 未解析的事务"
  - "未解析的事务"
  - "in-doubt xact resolution 选项"
ms.assetid: 3426fd32-cad2-4f2f-8ca9-e0296cc12703
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# in-doubt xact resolution 服务器配置选项
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 **in-doubt xact resolution** 选项可以控制 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC) 无法解决的默认事务结果。 事务无法解决可能与 MS DTC 停止工作或恢复时的未知事务结果有关。  
  
 下表列出了解决有疑问的事务可能出现的结果值。  
  
|结果值|说明|  
|-------------------|-----------------|  
|0|没有假设。 如果 MS DTC 无法解决任何有疑问的事务，恢复就会失败。|  
|1|假设提交。 假设已提交任何 MS DTC 有疑问的事务。|  
|2|假设中止。 假设已中止任何 MS DTC 有疑问的事务。|  
  
 若要尽可能减少扩展的停止工作时间，管理员可以选择将此选项配置为假设提交或假设中止，如以下示例所示。  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 2 -– presume abort  
GO  
RECONFIGURE  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 另外，管理员也可能希望保留默认值（没有假设）并允许恢复失败，以便了解 DTC 故障，如以下示例所示。  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 1 -– presume commit  
GO  
reconfigure  
GO  
ALTER DATABASE pubs SET ONLINE –- run recovery again  
GO  
sp_configure 'in-doubt xact resolution', 0 –- back to no assumptions  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 **in-doubt xact resolution** 选项是一个高级选项。 如果使用 **sp_configure** 系统存储过程来更改该设置，则仅当 **show advanced options** 设置为 1 时才可以更改 **in-doubt xact resolution**。 该设置将立即生效，无需重新启动服务器。  
  
> [!NOTE]  
>  在任何分布式事务所涉及的所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中，使此选项的配置始终保持一致，有助于避免数据的不一致。  
  
## 另请参阅  
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  