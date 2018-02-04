---
title: sys.dm_db_rda_migration_status (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_migration_status
- sys.dm_db_rda_migration_status_TSQL
- dm_db_rda_migration_status
- dm_db_rda_migration_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_rda_migration_status dynamic management view
ms.assetid: faf3901c-a0e0-4e0c-8b1b-86d9f15f34dd
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c3b4687e98a7fb917390e7ca8811c50bf543744c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="stretch-database---sysdmdbrdamigrationstatus"></a>Stretch Database-sys.dm_db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  为每个已启用延伸的表上的本地实例迁移的数据的每个批中对应一行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 通过其开始时间和结束时间，批处理进行标识。  
  
 **sys.dm_db_rda_migration_status**范围限定为当前数据库上下文。 请确保你想要查看迁移状态为其启用延伸的表的数据库上下文中。  
  
 在[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]的输出**sys.dm_db_rda_migration_status**最多 200 行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|从中迁移了行的表的 ID。|  
|**database_id**|**int**|从中迁移了行的数据库 ID。|  
|**migrated_rows**|**bigint**|在此批次中迁移的行数。|  
|**start_time_utc**|**datetime**|批处理所开始的 UTC 时间。|  
|**end_time_utc**|**datetime**|批处理完成时的 UTC 时间。|  
|**error_number**|**int**|如果批处理失败，发生的错误; 错误号否则，为 null。|  
|**error_severity**|**int**|如果批处理失败，出现; 错误的严重级别否则，为 null。|  
|**error_state**|**int**|如果批处理失败，发生的错误; 的状态否则，为 null。<br /><br /> **Error_state**指示的条件或发生错误的位置。|  
  
## <a name="see-also"></a>另请参阅  
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
