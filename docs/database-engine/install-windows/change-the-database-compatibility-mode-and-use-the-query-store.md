---
title: "更改数据库兼容性模式和使用查询存储 | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6fa6e9e16be729fba7334b26b130c8e22525e479
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="change-the-database-compatibility-mode-and-use-the-query-store"></a>更改数据库兼容性模式和使用 Query Store
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，某些更改仅在[数据库兼容级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)更改后才会启用。 执行此操作的原因如下：  
  
- 由于升级是单向操作（不可能降级文件格式），将新功能的启用分离为数据库内的单独操作有一定作用。 可以将一项设置还原到之前的数据库兼容级别。  新的模式可以减少中断期间必然发生的事件的数量。  
  
- 更改查询处理器可能会产生复杂的影响。 即使对系统进行的是“较好的”更改（对大多数工作负荷而言可能是非常好的更改），也可能对其他工作负荷的重要查询造成不可接受的回归。 通过从升级过程中分离此逻辑，查询存储等功能可在生产服务器中快速缓解计划选择回归或甚至完全将其规避。  
  
> [!IMPORTANT]  
> 如果升级前用户数据库的兼容级别为 100 或更高，升级后将保持相应级别。 如果升级前用户数据库的兼容级别为 90，则在升级后的数据库中，兼容级别将设置为 100，该级别为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持的最低兼容级别。 升级后，tempdb、model、msdb 和 Resource 数据库的兼容性级别将设置为当前兼容性级别。
> master 系统数据库保留它在升级之前的兼容性级别。 
  
用于启用新查询处理器功能的升级过程与产品的发布后服务模式相关。  这些修补程序中的一部分发布在[跟踪标志 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199) 下。  需要修补程序的客户可以选择加入这些修补程序而不会导致其他客户的意外回归。 查询处理器修补程序的发布后服务模式记录于 [此处](http://support.microsoft.com/kb/974006)。 从 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 开始，转换到新的兼容级别意味着不再需要跟踪标志 4199 ，因为在最新的兼容级别中这些修复程序现在默认处于启用状态。 因此，作为升级过程的一部分，验证升级过程完成后未启用 4199 是很重要的。  

> [!NOTE]
> 但是，仍需要跟踪标志 4199 才能启用 RTM 之后发布的任何适用的新查询处理器修补程序。
  
[查询存储使用方案中的“在升级到新版 SQL Server 期间保持性能稳定”部分](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade)中介绍了将查询处理器升级到最新版本的建议工作流，如下所示。  
  
![query-store-usage-5](../../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5") 
 
## <a name="see-also"></a>另请参阅  
 [查看或更改数据库的兼容级别](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)  
 [Query Store 使用方案](../../relational-databases/performance/query-store-usage-scenarios.md) 
  
