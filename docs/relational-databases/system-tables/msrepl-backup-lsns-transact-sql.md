---
title: "MSrepl_backup_lsns (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSrepl_backup_lsns_TSQL
- MSrepl_backup_lsns
dev_langs: TSQL
helpviewer_keywords: MSrepl_backup_Isns system table
ms.assetid: de06c349-82a8-48c6-b602-b5d6938514f6
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e7d73641645963ed6a136cc2fe5028abc63642a2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="msreplbackuplsns-transact-sql"></a>MSrepl_backup_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_backup_lsns**表包含事务日志序列号 (LSN) 以支持分发数据库的 'sync with backup 选项。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|发布服务器数据库的 ID。|  
|**valid_xact_id**|**varbinary(16)**|发送到发布服务器用以标记日志截断点的事务 ID。 仅当分发数据库处于 'sync with backup 模式下使用。 包含已备份分发数据库中最新复制事务的 ID。 它将被发送到发布服务器以标记日志读取器所做的日志截断点。|  
|**valid_xact_seqno**|**varbinary(16)**|发送到发布服务器用以标记日志截断点的事务序列号。 仅当分发数据库处于“sync with backup”模式时使用。 它是已备份分发数据库中最新复制事务的日志序列号。 它将被发送到发布服务器以标记日志读取器所做的日志截断点。|  
|**next_xact_id**|**varbinary(16)**|备份操作使用的临时日志序列号。|  
|**nextx_xact_seqno**|**varbinary(16)**|备份操作使用的临时日志序列号。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
