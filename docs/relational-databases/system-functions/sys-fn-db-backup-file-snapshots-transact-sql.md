---
title: sys.fn_db_backup_file_snapshots (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
author: rothja
ms.author: jroth
ms.openlocfilehash: 5159b72cb91cfdcf21129c6216cab4cf0e8d4dea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120273"
---
# <a name="sysfndbbackupfilesnapshots-transact-sql"></a>sys.fn_db_backup_file_snapshots (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  返回与数据库文件相关联的 Azure 快照。 如果找不到指定的数据库或数据库文件不存储在 Microsoft Azure Blob 存储服务，则不返回任何行。 结合使用此系统函数**sys.sp_delete_backup_file_snapshot**系统存储过程来识别和删除孤立的备份快照。 有关详细信息，请参阅 [Azure 中数据库文件的文件快照备份](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>参数  
 *Database_name*  
 正在查询的数据库的名称。 如果为 NULL，则当前数据库作用域中执行此函数。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|file_id|**int**|数据库文件 ID。 不可为 null。|  
|snapshot_time|nvarchar(260) |REST API 会返回作为它的快照的时间戳。 如果不存在任何快照，则返回 NULL。|  
|snapshot_url|**nvarchar(360)**|指向文件快照的完整 URL。 返回为 NULL，如果没有快照存在。|  
  
## <a name="permissions"></a>权限  
 需要对数据库拥有 VIEW DATABASE STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [sp_delete_backup_file_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup (Transact-SQL)](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
