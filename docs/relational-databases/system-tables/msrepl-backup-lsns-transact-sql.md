---
title: MSrepl_backup_lsns (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_backup_lsns_TSQL
- MSrepl_backup_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_backup_Isns system table
ms.assetid: de06c349-82a8-48c6-b602-b5d6938514f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b35c095b2c00b4293062086b9a79f92b1fb4e77b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52757909"
---
# <a name="msreplbackuplsns-transact-sql"></a>MSrepl_backup_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_backup_lsns**表包含事务日志序列号 (LSN) 为支持分发数据库的 'sync with backup 选项。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|发布服务器数据库的 ID。|  
|**valid_xact_id**|**varbinary(16)**|发送到发布服务器用以标记日志截断点的事务 ID。 仅当分发数据库处于 sync with backup 模式下使用。 包含已备份分发数据库中最新复制事务的 ID。 它将被发送到发布服务器以标记日志读取器所做的日志截断点。|  
|**valid_xact_seqno**|**varbinary(16)**|发送到发布服务器用以标记日志截断点的事务序列号。 仅当分发数据库处于“sync with backup”模式时使用。 它是已备份分发数据库中最新复制事务的日志序列号。 它将被发送到发布服务器以标记日志读取器所做的日志截断点。|  
|**next_xact_id**|**varbinary(16)**|备份操作使用的临时日志序列号。|  
|**nextx_xact_seqno**|**varbinary(16)**|备份操作使用的临时日志序列号。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
