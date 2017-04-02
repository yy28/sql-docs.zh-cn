---
title: "用条件性删除跟踪优化合并复制的性能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "条件性删除跟踪 [SQL Server 复制]"
  - "合并复制 [SQL Server 复制], 条件性删除跟踪"
  - "项目 [SQL Server 复制], 条件性删除跟踪"
ms.assetid: 58f120a3-ea3a-4e97-93f0-0eb4e580ecf2
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 用条件性删除跟踪优化合并复制的性能
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 通过使用合并复制，可以指定复制触发器和系统表跟踪不应删除一个或多个项目的操作。 如果为某项目指定了此选项，删除就不会从发布服务器或任何订阅服务器进行跟踪或复制。 此选项可用于支持许多应用程序方案，并为不需要或不希望复制删除的情况提供性能优化。 性能可以通过三种方式增强：不存储将删除的元数据、同步期间不枚举删除和不在订阅服务器上复制和应用删除。  
  
> [!NOTE]  
>  若要使用仅下载项目，发布的兼容级别必须至少为 90RTM。  
  
 此选项可以在创建发布时指定，也可以在应用程序要求复制某些删除而不复制另一些删除（如批删除）时打开和关闭此选项。 下列示例说明了在应用程序中可能使用此选项的几种情况：  
  
-   移动销售组的应用程序通常都有一些表，如 **SalesOrderHeader**、 **SalesOrderDetail** 和 **Product**。 订单在订阅服务器上输入，然后复制到发布服务器上，发布服务器通常向订单履行系统提供数据。 许多移动员工用的手持设备存储量通常都很有限：因此发布服务器接收到订单后就可以在订阅服务器上将其删除。 删除不会传播到发布服务器，因为订单在系统中仍是活动的。  
  
     这种情况下，不会对 **SalesOrderHeader** 和 **SalesOrderDetail** 表中的删除进行跟踪。 但会对 **Product** 表中的删除进行跟踪，因为如果某产品在发布服务器上删除，则删除应发送到订阅服务器以保持产品列表最新。  
  
-   应用程序可以在表中存储历史数据，比如 **TransactionHistory**表，该表会定期清除超过一年的历史记录。 对表可以进行筛选，以使订阅服务器只接收当月的事务数据。 在清除旧数据的发布服务器上的月度批量删除与订阅服务器无关，但默认情况下还会对这些删除进行跟踪和枚举。  
  
     在这种情况下，执行批处理前，可以停止系统中的活动，而应用程序也可以禁用对删除的跟踪。 处理完成后，跟踪可以重新启用。  
  
> [!IMPORTANT]  
>  如果其他活动在发布服务器上继续运行，则必须确保在禁用对删除的跟踪时不发生任何将传播到订阅服务器的删除。  
  
 **指定不应跟踪删除**  
  
-   复制 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 编程︰ [指定，将删除应不会跟踪为合并项目 & #40;复制 TRANSACT-SQL 编程 & #41;](../../../relational-databases/replication/publish/specify that deletes should not be tracked for merge articles.md)  
  
## 另请参阅  
 [合并复制的项目选项](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [使用仅下载项目优化合并复制的性能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)  
  
  