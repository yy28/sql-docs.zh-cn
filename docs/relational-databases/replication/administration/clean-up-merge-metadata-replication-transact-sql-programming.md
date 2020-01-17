---
title: 清除合并元数据（复制 SP）
description: 使用复制存储过程以编程方式清除合并复制表中的数据
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server replication]
- sp_mergemetadataretentioncleanup
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 50a5b71edd908c3c676f036e7f61197835e49360
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322084"
---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>清除合并元数据（复制 Transact-SQL 编程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  合并代理基于发布的保持设置定期清除合并复制元数据。 在发布服务器和订阅服务器的 [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)、 [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md)、 [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)、 [MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)和 [MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) 系统表中将定期清除元数据。 还可以使用复制存储过程以编程方式清除这些表中的数据。  
  
### <a name="to-manually-clean-up-merge-metadata"></a>手动清除合并元数据  
  
1.  在发布服务器的发布数据库中，执行 [sp_mergemetadataretentioncleanup](../../../relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql.md)。  
  
2.  （可选）请记录步骤 1 中从 [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)、[MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md) 和 [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) 系统表中删除的行数，它们分别在 `@num_genhistory_rows`、`@num_contents_rows` 和 `@num_tombstone_rows` 输出参数中返回。  
  
3.  在订阅服务器中重复步骤 1 和 2 来清除订阅数据库的元数据。  
  
## <a name="see-also"></a>另请参阅  
 [订阅过期和停用](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
