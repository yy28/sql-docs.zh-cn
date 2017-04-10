---
title: "合并复制的项目选项 | Microsoft Docs"
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
  - "合并复制 [SQL Server 复制], 项目选项"
  - "项目 [SQL Server 复制], 合并复制选项"
ms.assetid: 670abd41-d204-4cd7-a371-7664e603a0ce
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 合并复制的项目选项
  有许多用于合并表项目的选项，可以使用这些选项自定义复制行为以满足应用程序的需要。 使用合并复制可执行以下操作：  
  
-   使用行筛选器、联接筛选器和列筛选器。 通过筛选表项目，可以为要发布的数据创建分区。 有关详细信息，请参阅 [筛选已发布数据](../../../relational-databases/replication/publish/filter-published-data.md)。  
  
-   指定是否将订阅服务器上的更改上载到发布服务器。 对于其中部分或全部数据在订阅服务器上应为只读的应用程序，仅用于下载的项目提供性能收益。 有关详细信息，请参阅 [对 Download-Only 项目优化合并复制性能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
-   指定复制触发器和系统表不能跟踪一个或多个项目的删除操作。 此选项在许多应用方案中都非常有用。 其中包括那些使用不需要复制的批处理删除操作的应用方案。 有关详细信息，请参阅 [使用条件性删除跟踪优化合并复制性能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)。  
  
-   指定项目的处理顺序以确保项目按照应用程序要求的顺序处理。 有关详细信息，请参阅 [指定处理顺序的合并项目](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)。  
  
-   指定应将一组相关记录作为一个单元进行处理（默认情况下，合并复制逐行处理对表的更改）。 有关详细信息，请参阅 [通过逻辑记录对相关行组更改](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
-   在一个拓扑中的多个节点上更改相同数据的情况下使用冲突检测和解决方法。 有关详细信息，请参阅 [Detect and Resolve Merge Replication Conflicts](../../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md)。  
  
-   指定架构选项（例如，是否将约束和触发器复制到订阅服务器）。 有关详细信息，请参阅 [指定架构选项](../../../relational-databases/replication/publish/specify-schema-options.md)。  
  
-   使用业务逻辑处理程序来对同步期间出现的许多情况进行响应。 这些情况包括发生数据更改、冲突和错误。 有关详细信息，请参阅 [执行合并同步期间业务逻辑](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)。  
  
## 另请参阅  
 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  