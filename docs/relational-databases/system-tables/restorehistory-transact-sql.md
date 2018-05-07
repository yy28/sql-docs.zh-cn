---
title: restorehistory (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- restorehistory
- restorehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorehistory system table
ms.assetid: 9140ecc1-d912-4d76-ae70-e2a857da6d44
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 72f788cf3248ba87bfa4ded7efed219ef3043cf5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="restorehistory-transact-sql"></a>restorehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个还原操作在表中占一行。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|标识每个还原操作的唯一标识号。 标识，主键。|  
|**restore_date**|**datetime**|完成还原操作的日期和时间。 可以为 NULL。|  
|**destination_database_name**|**nvarchar(128)**|还原操作的目标数据库的名称。 可以为 NULL。|  
|**user_name**|**nvarchar(128)**|执行还原操作的用户的名称。 可以为 NULL。|  
|**backup_set_id**|**int**|标识被还原的备份集的唯一标识号。 引用**backupset(backup_set_id)**。|  
|**restore_type**|**char(1)**|还原操作的类型：<br /><br /> D = 数据库<br /><br /> F = 文件<br /><br /> G = 文件组<br /><br /> I = 差异<br /><br /> L = 日志<br /><br /> V = 仅验证<br /><br /> 可以为 NULL。|  
|**replace**|**bit**|指示还原操作是否指定了 REPLACE 选项：<br /><br /> 1 = 已指定<br /><br /> 0 = 不指定<br /><br /> 可以为 NULL。<br /><br /> 将数据库恢复到数据库快照时，0 是唯一的选项。|  
|**recovery**|**bit**|指示还原操作指定的是 RECOVERY 选项还是 NORECOVERY 选项：<br /><br /> 1 = RECOVERY<br /><br /> 可以为 NULL。<br /><br /> 当数据库还原到数据库快照时，1 是唯一的选项。<br /><br /> 0 = NORECOVERY|  
|**restart**|**bit**|指示还原操作是否指定了 RESTART 选项：<br /><br /> 1 = 已指定<br /><br /> 0 = 不指定<br /><br /> 可以为 NULL。<br /><br /> 将数据库恢复到数据库快照时，0 是唯一的选项。|  
|**stop_at**|**datetime**|数据库要恢复到的时间点。 可以为 NULL。|  
|**device_count**|**tinyint**|还原操作涉及的设备数。 此数目可以小于备份使用的介质簇数。 可以为 NULL。<br /><br /> 将数据库恢复到数据库快照时，此数目将始终为 1。|  
|**stop_at_mark_name**|**nvarchar(128)**|指示恢复到包含命名标记的事务。 可以为 NULL。<br /><br /> 将数据库恢复到数据库快照时，此值为 NULL。|  
|**stop_before**|**bit**|指示恢复中是否包含命名标记的事务：<br /><br /> 0 = 在标记的事务前停止恢复。<br /><br /> 1 = 恢复包括标记的事务。<br /><br /> 可以为 NULL。<br /><br /> 将数据库恢复到数据库快照时，此值为 NULL。|  
  
## <a name="remarks"></a>注释  
 若要减少在此表，其他备份和历史记录表中的行数，执行[sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)存储过程。  
  
## <a name="see-also"></a>另请参阅  
 [备份和还原表&#40;Transact SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefile &#40;Transact SQL&#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [restorefilegroup &#40;Transact SQL&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [系统表 (Transact-SQL)](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
