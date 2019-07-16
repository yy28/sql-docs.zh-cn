---
title: sys.dm_db_rda_migration_status (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 21e5230e4f3efd86fe90382202f0b21a0187a214
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937064"
---
# <a name="stretch-database---sysdmdbrdamigrationstatus"></a>Stretch Database-sys.dm_db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  每个批的已迁移数据的本地实例上的每个已启用延伸的表中对应一行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 批处理通过其开始时间和结束时间进行标识。  
  
 **sys.dm_db_rda_migration_status**的范围限定为当前数据库上下文。 请确保您在想要查看迁移状态的 Stretch 启用表的数据库上下文。  
  
 在中[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]的输出**sys.dm_db_rda_migration_status**限制为 200 行。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|从中迁移了行的表的 ID。|  
|**database_id**|**int**|从中迁移了行的数据库的 ID。|  
|**migrated_rows**|**bigint**|在此批中迁移的行数。|  
|**start_time_utc**|**datetime**|批处理开始的 UTC 时间。|  
|**end_time_utc**|**datetime**|批处理完成时的 UTC 时间。|  
|**error_number**|**int**|如果批失败，出现，则该错误的错误号否则，为 null。|  
|**error_severity**|**int**|如果批失败，发生错误的严重级别否则，为 null。|  
|**error_state**|**int**|如果批失败，出现，则该错误的状态否则，为 null。<br /><br /> **Error_state**指示条件或发生错误的位置。|  
  
## <a name="see-also"></a>请参阅  
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
