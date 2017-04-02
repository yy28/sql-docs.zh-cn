---
title: "清除合并元数据（复制 Transact-SQL 编程） | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "元数据 [SQL Server 复制]"
  - "sp_mergemetadataretentioncleanup"
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 清除合并元数据（复制 Transact-SQL 编程）
  合并代理基于发布的保持设置定期清除合并复制元数据。 在发布服务器和订阅服务器中的将出现这种情况 [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), ，[MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), ，[MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), ，[MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md), ，和 [MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) 系统表。 还可以使用复制存储过程以编程方式清除这些表中的数据。  
  
### 手动清除合并元数据  
  
1.  在发布服务器上对发布数据库中，执行 [sp_mergemetadataretentioncleanup](../../../relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql.md)。  
  
2.  （可选）便笺中删除的行数步骤 1 从 [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), ，[MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), ，和 [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) 系统表中，返回分别在 **@num_genhistory_rows**, ，**@num_contents_rows**, ，和 **@num_tombstone_rows** 输出参数。  
  
3.  在订阅服务器中重复步骤 1 和 2 来清除订阅数据库的元数据。  
  
## 另请参阅  
 [订阅过期和停用](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  